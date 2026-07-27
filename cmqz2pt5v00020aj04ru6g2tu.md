---
title: "Architecting a Monorepo: Week 3"
seoTitle: "/architecting-a-monorepo"
seoDescription: "Building a Monorepo: Onboarding Flows & Custom Auth"
datePublished: 2026-06-29T10:27:10.439Z
cuid: cmqz2pt5v00020aj04ru6g2tu
slug: architecting-a-monorepo-week-3
cover: https://cdn.hashnode.com/uploads/covers/697b5c79519035959f5d9078/a137bcd8-e2e7-4321-935b-a1ee6814daad.png
ogImage: https://cdn.hashnode.com/uploads/og-images/697b5c79519035959f5d9078/a8733616-2a53-4837-b0c7-2217690542cc.png
tags: internships, architecture, ui-design, frontend-development, uiux-design, ui-ux-designer, architecture-design

---

Hey everyone! 👋 Welcome back to week three of my software engineering internship journey. If you’ve been following along, we spent last week wrestling with data dictionaries, setting up Material UI in Figma using Stitch, and surviving our first client review.

This week, we completely crossed the boundary from layout design blueprints into active development. We spun up our monorepo architecture and got our hands dirty with real code. From building complex, multi-step user forms to completely refactoring security frameworks, it was a week filled with massive engineering milestones.

*Let’s talk about how we laid down the foundational code for our platform!*

## **1\. Building the Three-Step Candidate Onboarding Flow**

My biggest development milestone this week was building the three-step candidate onboarding flow from scratch. The system requires candidates to move through three distinct phases: **Registration & Profile, Essay Questions, and a Personality Assessment.**

Building multi-step forms on the web is notoriously tricky because users frequently refresh their browsers or drop off midway. To create a seamless user experience, I engineered a [**per-user draft persistence**](https://learning.sap.com/courses/building-transactional-apps-with-the-abap-restful-application-programming-model/understanding-the-draft-concept) system with **step-resume logic**. If a candidate accidentally reloads or closes the page, the system securely retains their progress and lets them pick up exactly where they left off without losing their data.

## **2\. Harnessing the Power of a Monorepo**

As our codebase grew, we quickly realized that copy-pasting code between different application modules would turn into a developer's nightmare. To solve this, we migrated our shared UI components into independent, reusable [**monorepo**](https://monorepo.tools/) **packages**.

I worked on abstracting our core layout elements, including the global application shell, landing page layouts, logo assets, system loading states, and the interactive candidate user menu into a single shared package. Now, both our candidate portal and admin dashboard can import these elements natively.

### **The Whiteboard Battle: Shifting to RPC**

While setting up our monorepo, our team ran into a massive architectural debate. We had originally planned a traditional REST API structure, but our manager pushed to switch the backend integration layer to an [**RPC**](https://en.wikipedia.org/wiki/Remote_procedure_call) **(Remote Procedure Call)** mechanism inside the monorepo workspace.

Initially, there was friction because it was a paradigm we had never used before. We literally crowded around a physical whiteboard today, watching our manager draw out system flows and defend the change. Once we systematically weighed the trade-offs, the clarity became obvious: using an RPC layer inside a single monorepo allows our frontend to directly import backend types, offering end-to-end type safety and eliminating silent runtime endpoint errors.

## **3\. Overhauling Authentication & The Dashboard Hub**

Security was another heavy focus this week. We decided to move away from a generic, third-party catch-all authentication system and replace it with **completely customized sign-in and sign-up flows**.

This involved configuring complex OAuth callback handlers and engineering robust Single Sign-On (SSO) error recovery mechanisms to ensure users never get stuck if a social login fails. Once authenticated, candidates land on a freshly implemented **Dashboard Home Hub**. I wired up strict **gated routing logic** that locks down the dashboard, ensuring candidates cannot access core portal metrics until their initial 3-step onboarding profiles are fully verified and complete.

## ***Overcoming Technical Friction (Bugs & Branching)***

You can't write that much code without breaking things! I spent a chunk of my time squashing bugs, including fixing multiline text field rendering errors and resolving a pesky bug where a step-two form reload would wipe out inputs.

I also ran into development environment quirks where certain library icon imports triggered [hot-module reloading](https://www.sanity.io/glossary/hot-module-replacement) (HMR) chunk errors. I had to pivot and replace them with custom inline SVG code to stabilize the local development cache.

To keep our deployment pipeline clean, I split my massive workspace changes into three cleanly stacked git branches—covering the shell refactor, UI fixes, and personality-step integration—pushing them as distinct pull requests for code review.

## **Moving Forward**

We started the week setting up directories, and we are ending it with a fully functional, gated monorepo ecosystem. The architecture is stable, our layout bugs are squashed, and our team branches are ready for review.

> **Next stop:** Wiring our live personality test questionnaire modules directly into the onboarding flows, transitioning client-side local storage persistence over to backend profile endpoints, and prepping for our upcoming feature branch staging merge. See you in Week 4!

**💬 Let's Connect!**

*For the frontend engineers out there: how do you prefer to manage state persistence in multi-step onboarding forms? Do you lean toward local state caching or live database synchronization? Let's talk in the comments!*