---
title: "REST Brain vs Procedure Brain"
seoTitle: "When your backend isn't a separate API server"
seoDescription: "What happens when your backend isn't a separate server? Reflections on procedural RPC, monorepos, and architecture tradeoffs."
datePublished: 2026-06-24T14:46:07.788Z
cuid: cmqs6rkhx00000aj65hcw4xcq
slug: rest-brain-vs-procedure-brain
cover: https://cdn.hashnode.com/uploads/covers/697b5c79519035959f5d9078/35083f26-2d1a-4d9c-84aa-0d5e3f687305.png
ogImage: https://cdn.hashnode.com/uploads/og-images/697b5c79519035959f5d9078/afbc780e-9a85-42f9-9f51-4f2bdd81d579.png
tags: web-development, backend, architecture, webdev, typescript, infrastructure, monorepo, rpc, monolithic-architecture, architecture-design

---

Today we had a proper argument about architecture.

Not a shouting match, the kind where everyone cares about the product, nobody is trying to “win,” and yet you still walk away feeling like you’re speaking different languages. We sat with the pros and cons of our API design, wrote them down, and for the first time, the choice actually made sense to me, even though it isn’t the architecture most tutorials teach.

I’m writing this while it’s fresh. It’s a lesson reflection, not a hot take.

## **The setup**

I’m working on **Talent Funnel** — a monorepo with separate web apps for candidates and admins, shared packages, Clerk for auth, Firestore for data, and a multi-stage recruitment workflow.

When I joined the codebase, I assumed the backend would look familiar:

```c
Frontend  →  HTTP  →  API server  →  database
```

REST-shaped. Endpoints. Maybe Next.js API routes. A box on the diagram labeled “backend” is deployed separately from the UI.

That’s **REST brain** — the default mental model from tutorials, coursework, and most first jobs.

## **What the codebase actually does**

The team went a different direction: **procedural RPC**, running **in-process** inside the monorepo.

Instead of `POST /api/candidates`, the frontend calls typed procedures through a shared client:

```c
await api.candidate.create({ name, email, source })
```

That isn’t a network request. A registry looks up `candidate.create`, Zod validates the input, a handler runs the business logic, and a typed result comes back. Same process. Same repo. No separate API server in the middle.

```c
apps/admin / apps/candidate
        ↓
   @funnel/api-client
        ↓
   procedure registry
        ↓
   src/procedures/*
```

Procedures follow a `domain.action` pattern — `candidate.create`, `application.submit`, and so on. UI code is supposed to go through one boundary: the API client. No importing the database or auth modules directly from components.

My first reaction wasn’t “interesting tradeoff.” It was: *I’ve never seen this before. What even is this?*

## **The argument that changed my mind**

Today, we finally talked it through properly.

One side laid out the case for procedures: consistency across two frontends, shared validation, typed contracts, less infrastructure early on, and one obvious home for business logic. The other side pushed on what felt off: no HTTP boundary, no separately deployable backend, handlers in the same process as the app, registration through side-effect imports that feel “magical” until you trace them.

We walked through the alternatives the team had already evaluated:

| **Approach** | **Why wasn’t it the default pick** |
| --- | --- |
| **REST** | Easy to drift (`/create-candidate` vs `addCandidate`), weaker typing without codegen, separate server to operate |
| **tRPC** | Strong DX, but adds framework coupling |
| **GraphQL** | Powerful, but heavy for this domain right now |
| **In-process procedures** | Unfamiliar, but fits a monorepo that needs discipline |

That table helped. The conversation got calmer when we stopped debating vibes and started comparing tradeoffs.

**Pros that landed:**

*   **One pattern everywhere** — define a procedure, validate with Zod, implement a handler, expose it on the client.
    
*   **A real boundary, just not a network one** — UI doesn’t touch Firestore or services directly; it calls `api.*`.
    
*   **Type safety that feels natural** — real functions on the client, not stringly-typed `fetch` wrappers.
    
*   **Less overhead while the product is still finding shape** — no separate API service to run before you need it.
    

**Cons we were honest about:**

*   **Unfamiliar** — the learning curve may cost more than runtime performance.
    
*   **No natural scaling seam** — you can’t scale “just the API tier” without later wrapping procedures in HTTP or a queue.
    
*   **Same-process work** — heavy logic in a handler is your problem; the pattern doesn’t imply a worker.
    
*   **The boundary must be enforced** — review and discipline matter, because shortcuts are always possible.
    

What shifted for me wasn’t “procedures are better.” It was understanding **the problem they solved**: not distributed-system elegance on day one, but **keeping two frontends in one repo from inventing five different ways to do the same thing**.

## **REST brain vs. procedure brain**

The friction was two instincts talking past each other.

**REST brain** asks:

*   Where is the server?
    
*   What’s the endpoint?
    
*   How do we scale the backend independently?
    
*   Where’s the network line on the diagram?
    

**Procedure brain** asks:

*   What’s the one allowed way for UI to request work?
    
*   Where does validation live?
    
*   How do we keep business logic out of components?
    
*   How do two apps share behavior without copying it?
    

Neither set of questions is wrong. They’re tuned for different contexts.

For a monorepo with multiple frontends, early product shape, and a team that needs consistency without extra ops procedure, Brain is a coherent bet.

For a public platform that needs independent scaling, strict service ownership, and third-party API consumers, REST brain (or a real wire protocol) may win later.

The decision record essentially says: choose a typed use-case layer now; add an HTTP wrapper later if scale demands it. That’s a deliberate trade, not a shortcut.

## **Lessons I’m keeping**

### 1\. Architecture fights are often vocabulary fights.

We said “RPC” and “API” and meant different things. Once someone called it a typed use-case layer with one client entry point, I could place it next to application services, commands, and actions. The pattern wasn’t alien — the label was.

### 2\. “I’ve never seen this” is a signal, not a verdict.

Discomfort is information. It doesn’t automatically mean the design is wrong. It means you need the context: monorepo, multiple apps, early stage, consistency over distribution.

### 3\. Pros and cons build trust.

An architecture with only upsides in the room is suspicious. Naming limits made the choice easier to accept.

### 5\. Mental models update on real code, not diagrams.

I had one picture of how backends work. This project added another: the backend isn’t always a separate box. Sometimes it’s a discipline layer inside the app, and that can be right until the product outgrows it.

### 6\. Written decisions end circular meetings.

An ADR and architecture doc exist for a reason. When the record matches the code, onboarding and debate both get shorter.

## **If you hit the same wall**

When the architecture doesn’t match the tutorial playbook, three questions helped me:

*   What familiar pattern is this closest to?
    
*   What boundary are we protecting?
    
*   What are we *not* optimizing for yet?
    

If you’re proposing something unfamiliar, name it in plain English first — not “RPC,” but *shared procedures, validated at the door, called through one client, living in the same repo*. Show one vertical slice. Let people trace the call.

> We didn’t remove the backend. We agreed on what it **is** in this phase: not a separate service, but named procedures behind a typed client — a contract the monorepo shares.
> 
> I still have REST brain reflexes. That’s fine. The skill is carrying more than one model and knowing which fits the repo and the moment.
> 
> That’s the discovery for this one.