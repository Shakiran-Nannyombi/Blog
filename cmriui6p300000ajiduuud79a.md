---
title: "When Being Right Still Means Redoing the Work "
seoTitle: "When Being Right Still Means Redoing the Work"
seoDescription: "Follow week 5 of my internship journey: restructuring multi-step wizards, fixing Next.js CI build bugs, and resolving team branch-merge friction."
datePublished: 2026-07-13T06:32:41.326Z
cuid: cmriui6p300000ajiduuud79a
slug: when-being-right-still-means-redoing-the-work
cover: https://cdn.hashnode.com/uploads/covers/697b5c79519035959f5d9078/fbd7c54d-c956-4d3c-9ec0-fdb7fec584ac.png
ogImage: https://cdn.hashnode.com/uploads/og-images/697b5c79519035959f5d9078/72b2d1e5-f9d6-4b8d-b692-095146f89a25.png
tags: internships, github, ui-design, frontend-development, manager, nextjs, teamwork

---

Hey everyone! 👋

Welcome back to week five of my software engineering internship journey. Last week, we built Stage 3 challenge UIs and turned a plain dashboard into a home hub. This week was less about inventing a brand-new funnel stage and more about tightening the candidate experience: public landing, onboarding flow, profile/settings clarity, home-page hierarchy, and one very real lesson about how teams merge work.

Let’s get into it.

## **Building a Landing Page With One Clear Job**

A big focus this week was the public candidate landing page. We added a video hero, a dedicated landing footer, and auth-page background treatment so sign-in and sign-up felt connected to the same visual language.

Early on, the hero box had too much copy. The headline and supporting sentence were competing in the same tinted panel. On a full Chrome tab, it looked okay; in a narrower preview pane, it overflowed because we had forced single-line wrapping past the `sm` breakpoint. That was a useful reminder: responsive is not only phone vs desktop. Split views and embedded browsers count too.

We simplified the first [viewport](https://www.lenovo.com/us/en/glossary/viewport/?srsltid=AfmBOoocUQGlRQSARmkfZ9TPVOZlsBTgrG1RQxbUB0JHxkFsEqJppiQv) to one hero line “Welcome to the future of talent discovery,” and moved the supporting line into the content section as a subheading. Same story, cleaner hierarchy.

## **Turning Registration Into a Multi-Step Wizard**

Stage 1 registration was getting heavy as one long form. This week I broke it into a multi-step wizard layout with sub-step resume support, clearer graduation year selection drop-downs, and client-side CGPA validation rules. To keep candidates from feeling overwhelmed, I split our reflective essay sections across separate progression frames instead of throwing them all into one dense block.

The goal was simple: make onboarding match how candidates actually move personal details, then education, then essays, without losing draft progress or file assets mid-flow.

## **Separating Profile Editing From Account Security**

Another cleanup I’m proud of: *profile vs My Account.*

Editing moved into profile tabs (personal info, documents, essays, personality). My Account stayed focused on account security through Clerk’s UserProfile. That sounds like a small information-architecture change, but it removed a lot of confusion.

Alongside that, we:

*   **Improved Document Cards:** Added clearer upload/replace wording and active verification status chips.
    
*   **Aligned Settings Page Width:** Matched layout container padding perfectly with other core funnel pages.
    
*   **Fixed Footer/Scroll Behavior:** Fixed sticky/scroll parameters so short pages still feel grounded without locking the viewport frame.
    
*   **Polished Account Security UI:** Wrapped Clerk’s panel components so they didn't feel nested inside another awkward container.
    

## **Fixing Home Hub Hierarchy (Without a Full Redesign)**

Midweek we revisited `/home`. The layout wasn’t “wrong” — it was crowded. The welcome banner, next-step card, and sidebar widgets all carried similar visual weight, so the eye didn’t know where to land.

We made one rule: **Your Next Step is #1.**

That meant:

*   A high-contrast hero `ActionCard` as the primary CTA.
    
*   Moving “Great job…” into a real page heading and subheading at the top.
    
*   Demoting the welcome strip and removing duplicate stage pills.
    
*   Grouping our automated Guidelines PDF generation, Assessment Prep, and Quick Links under one unified Resource hub.
    
*   Keeping the vertical Recruitment Funnel as the single detailed progress tracker.
    

We also removed the redundant “Your next step / Pick up where you left off…” heading. When the greeting already tells you Stage 2 is waiting, that label is just noise. Crucially, I resolved a stale-state issue where the dashboard failed to update after test submissions by syncing the candidate context right upon submission and forcing data refreshes on the `/home` route mount.

## **Branch Hygiene, Merge Friction, and Learning When to Adjust**

Not all of the week was pixels.

I had landing and auth work on a feature branch that inadvertently included notification and scenario-assessment changes. Another teammate had already been working in that notifications space. When it came time to merge, my manager’s position was clear: he wasn’t going to merge a PR that overlapped someone else’s ownership area even though the landing/auth work was ready on its own.

My first instinct was to argue the packaging: keep the unrelated UI changes, let notifications be rewritten separately. From a pure diff perspective, that still felt fair. But arguing the point wasn’t going to unblock the merge. The decision wasn’t only about whether my reasoning was correct; it was about ownership boundaries and how the team ships.

So I calmed down, rewrote the branch history via Git to isolate only landing and auth, squashed local linting bugs, and left notifications alone. Annoying in the moment, redoing scope you already built always is, but it was the fastest path to shipping what could ship.

Separately, CI failed on `next build` with [`RESEND_API_KEY`](https://resend.com/) `environment variable is not set`, while my local build passed. Local `.env.local` Had the key; GitHub Actions did not. Worse, the Resend client threw at module import time, and Next evaluates API route modules during build. The fix was lazy client creation—deferring Resend initialization until send time. Secrets belong at runtime, not during “collecting page data.”

## **What I Learned: Hierarchy and Humility**

Week 5 taught me two related lessons.

First: **polish is often subtraction.** One hero headline beats two paragraphs. One primary CTA beats three equal-weight cards. A PR with one clear surface area beats a kitchen-sink branch.

Second: **in a team, being “right” about a technical boundary doesn’t always decide the outcome.** Sometimes a manager’s call is about risk, ownership, and clarity more than your preferred commit packaging. You can disagree privately, then still choose the move that unblocks the product. That adjustment is part of the job. I’m at peace with that now.

## **Moving Forward**

> Next up: finish PR review and merge for the remaining UI work, keep verifying challenge submit → home progression sync, and continue tightening Stage 4 / complete-page messaging so the story stays coherent from landing → onboarding → assessments → next step.

See you in Week 6!

**💬 Let's Connect!**

*When a PR gets blocked over ownership overlap, do you defend keeping the whole branch or splitting it and shipping what you can? Curious how other teams handle that.*