---
title: "Engineering the Frontend Funnel"
seoTitle: "Engineering the Frontend Funnel: Dashboards & Hubs"
seoDescription: "Follow week 4 of my internship building technical assessment funnels, local storage checklists, rich dashboard home hubs, and responsive layouts.
"
datePublished: 2026-07-13T05:45:29.428Z
cuid: cmristhl900010bhzck4i7fcy
slug: engineering-the-frontend-funnel
cover: https://cdn.hashnode.com/uploads/covers/697b5c79519035959f5d9078/791a8e39-7ac3-4578-85d2-25932bde587f.png
ogImage: https://cdn.hashnode.com/uploads/og-images/697b5c79519035959f5d9078/8a11dd92-2c33-4475-9a07-6cc01ef51196.png
tags: internships, frontend, web-development, ui-design, frontend-development, material-ui

---

Hey everyone! 👋

Welcome back to week four of my software engineering internship journey. Last week was an absolute whirlwind of monorepo setups, custom auth overwrites, and intense whiteboard debates over switching to type-safe RPC systems.

This week, we took that newly established architecture and went all-in on frontend feature development. We built the complete end-to-end user interface for our technical assessment funnel, completely overhauled the user landing experience, and added a layer of visual polish to make our app feel alive and seamless.

> Let’s dive into how we engineered the complete candidate experience this week!

## **1\. Building the Stage 3 Technical Assessment Funnel UI**

My main focus this week was building the complete interface flow for Stage 3 of our talent funnel: the **Technical Assessment**. This is where candidates view their challenge briefing, select their project path, submit their public repository code links, and complete a final debrief text questionnaire.

### I spent a lot of time aligning these views with our core design system layout rules:

*   **Two-Column Grids:** Splitting information structurally so complex instructions are on one side, and input fields are on the other.
    
*   **Interactive Submission Checklist:** I built a smart step validator that tracks whether a candidate has pushed their code, made their repo public, written a README, and included a live link. This checklist utilizes `localStorage` persistence so their checked states survive unexpected browser refreshes.
    
*   **Input Clamping & Validation:** For the final debrief fields, I built real-time text validators with a strict 1,000-word limit. It features a reactive, live word-counter that actively clamps inputs the moment a candidate tries to type past the allowance.
    

## **2\. Upgrading the Dashboard to a Data-Rich Home Hub**

At the start of the week, our candidate landing space was just a plain, empty dashboard viewport. We completely dismantled it and replaced it with a much richer **Home Hub UI module**.

Now, when an authenticated user logs in, they are greeted by a dynamic welcome hero banner featuring a sleek linear gradient background, an automated visual funnel progress bar tracking their application state, and distinct stage pills. Right below that, I implemented contextual "Your Next Step" action cards, an assessment preparation widget, quick-resource links, and an exploration grid to join our talent community.

### **Squashing the Stale State Bug**

While building the hub, we hit a sneaky state synchronization bug. When a candidate finished submitting an assessment, the browser redirected them to the home page, but the progress bar and cards would display stale, outdated data until they manually refreshed the browser.

To fix this, I synced our global candidate tracking context directly into the API submission paths. Now, the app hooks automatically pull fresh data packets the exact millisecond the user lands on the `/home` route, keeping the progression indicators instantly in sync.

### **3\. Character Placement, Global Footers, and Loading Overlays**

To give the application character, we integrated our brand's mascot asset into the UI using complex screen constraints.

*   **Adaptive Layouts:** I mapped out the avatar placement so it renders smoothly within authentication fields and the assessment debrief page exclusively on large desktop resolutions, hiding it dynamically on smaller mobile screens to keep the workspace clean.
    
*   **Root Layout Cleanups:** To optimize performance, I abstracted the `CandidateMinimalFooter` component out of individual page wrappers and pushed it straight to the application's root layout folder. This instantly removed redundant code duplicates and fixed footer rendering glitches.
    
*   **Full-Viewport Loader:** I refactored the standard `PageLoading` Element into a centered, full-viewport screen overlay. Now, when data is being fetched, the loader sits in the geometric center of the screen, hiding unstyled content and preventing the footer from awkwardly jumping up before the elements render.
    

### **What I Learned: The Visual-Data Equilibrium**

Week 4 proved to me that as a software engineer, you can’t just write robust backend logic and throw it into an unpolished UI. The real magic happens when your backend APIs match seamlessly with micro-interactions on the screen—like a progress bar that shifts instantly on click, a local storage checklist that remembers user input, or a text box that gently prevents you from typing over a word limit.

Paying attention to global layouts and caching states turns a clunky web form into a premium, fluid desktop application.

## **Moving Forward**

The frontend foundations are completely solid, our dashboard is fully responsive, and our state persistence layers are working cleanly.

> **Next stop:** Wiring our live challenge submissions completely end-to-end to backend endpoints, polishing the post-assessment success pages, enforcing server-side word validation rules, and tackling our final feature staging branch merge conflict cleanups. See you in Week 4!

## **💬 Let's Connect!**

*When you're building multi-step application funnels, do you prefer using local client-side states (like localStorage) to save drafts, or do you stream every input click instantly to a live server? Let's talk layout strategies in the comments!*