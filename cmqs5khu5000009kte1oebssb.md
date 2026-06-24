---
title: "Deep Dives & Data Architecture: Translating Requirements into Design (Week 2)"
seoTitle: "Software Engineering Internship Journey: Week 2 Blueprints"
seoDescription: "Follow my internship week 2 journey, building clean data dictionaries, mapping out cloud pricing, and using Stitch to scaffold UI mockups.
"
datePublished: 2026-06-24T14:12:38.128Z
cuid: cmqs5khu5000009kte1oebssb
slug: deep-dives-data-architecture-translating-requirements-into-design-week-2
cover: https://cdn.hashnode.com/uploads/covers/697b5c79519035959f5d9078/41e92db8-bfa6-4052-b465-57fb8afb3001.png
ogImage: https://cdn.hashnode.com/uploads/og-images/697b5c79519035959f5d9078/1ecd9af3-de98-4edb-8b00-155f2926bb1c.png
tags: internships, software-engineering, material-ui, intern, figma, dataarchitecture

---

If you caught my last post, you know Week 1 was all about surviving the transition from independent solo projects to peer-led team planning.

This week, the training wheels completely came off. We moved from high-level summaries into concrete data architecture, defined our product’s absolute visual identity, and stepped into our very first high-stakes client feedback meeting.

Grab a coffee, it’s time to talk about turning abstract requirements into actual blueprints!

## **1\. The Heavy Lifting: Domain Analysis & The Data Dictionary**

Before you can build a clean user interface, you have to map out exactly how your system structures information under the hood.

First, our team compiled a comprehensive [**Domain Analysis Document**](https://www.site.uottawa.ca/~laganier/seg2500/domain). This was critical because it forced us to thoroughly understand the industrial context and core terminology of automated talent pipelines before guessing what the database should look like.

From there, we transitioned into writing the [**Data Dictionary Specification**](https://www.geeksforgeeks.org/software-engineering/data-dictionaries-in-software-engineering/). I spent hours structuring core entities like `AdminUser`, `CandidateUser`, and `CandidateProfile`. To make things highly performant, we made a strategic choice: instead of creating dozens of isolated tables, we designed a master hub where the candidate's test responses, project links, and human interview evaluations are stored directly as nested JSON data arrays.

## 2\. The Real-World Reality: The Infrastructure Pricing Document

In school, you write code and run it locally for free. In production, every database write, cloud file upload, and user authentication costs real money.

To tackle this constraint, we drafted a detailed **Infrastructure Pricing Document**. We had to research and calculate estimated hosting, cloud object storage, and third-party API costs. Balancing complex architectural needs while keeping infrastructure budget estimations accurate was an intense tightrope walk, but it taught me that solid software engineering is always bound by business reality.

## 3\. Figma From Scratch: Customizing Material UI (MUI)

Once the data and numbers were locked in, it was finally time to jump into Figma to define our global [design system](https://www.figma.com/blog/design-systems-101-what-is-a-design-system/) using **Material Design 3 (M3/MUI)** rules.

I’m going to be completely transparent here: **doing this for the first time was incredibly challenging and a bit confusing.** Staring at an empty digital canvas while trying to synchronize background design assets and font tokens between automated plugins and my local Figma workspace gave me a massive headache.

But I found an incredible shortcut that saved my week: **Stitch****.**

Instead of building every text field, button, and dashboard element block by block, I leveraged Stitch to quickly scaffold my interface layouts. By feeding our core design parameters and actual database fields into Stitch, it pulled real pre-built Material UI component assets straight onto the canvas.

I extracted our brand colors straight from our logo pixels, setting up a striking theme palette across those components:

*   **Primary Cyan Blue (**`#00A3E0`**)** for core actions.
    
*   **Secondary Charcoal (**`#5E5E5E`**)** for structural borders.
    
*   **Tertiary Magenta (**`#C9289D`**)** exclusively for system warning alerts and test countdown timers.
    

I paired these colors with a bold, high-tech typography scale—using **Orbitron** for powerful headings and **Inter** for dense, readable data grids. Thanks to the head-start from Stitch and official MUI assets, I transformed an empty screen into an interactive prototype in record time.

## 4\. The Client Meeting: Facing the Ultimate Test

By the end of the week, I had wired these design tokens into fully interactive, clickable frames to simulate live application workflows. Then came the big moment: **the stakeholder review session.**

Presenting my first-ever [high-fidelity prototypes](https://www.figma.com/resource-library/high-fidelity-prototyping/) to real clients was nerve-wracking, but the interactive presentation mode worked beautifully. We walked them through the candidate onboarding views and admin matrix screens, receiving invaluable feedback.

This meeting proved to me that planning on paper isn't enough ([low-fidelity prototypes](https://www.figma.com/resource-library/low-fidelity-prototyping/)). Truly understanding the client's perspective, knowing your technical constraints, and seeing how they react to the system flow is the most critical phase before writing a single line of frontend code.

## What’s Coming Next?

We survived the client review, and now we have an explicit list of layout refinements to make. We are officially closing out the blueprint phase and moving toward the code!

> **Next stop:** Implementing our client's visual feedback, mapping out a full Entity-Relationship (ER) database schema, agreeing on repo structure, and spinning up our Next.js frontend & backend staging environment. See you in Week 3!

**💬 Let's Chat!**

*For the frontend devs and UI designers: have you ever used tools like Stitch to scaffold your prototypes, or do you prefer drawing everything by hand? Let's discuss in the comments!*