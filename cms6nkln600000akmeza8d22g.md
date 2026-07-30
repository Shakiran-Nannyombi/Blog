---
title: "From Idea to Production: Building a Spider-Man Tic-Tac-Toe Game with Kiro"
seoTitle: "Building Tic-Tac-Toe with Kiro AI IDE"
seoDescription: "Learn how I built a Tic-Tac-Toe game with Kiro using spec-driven development and explored AI-assisted software engineering."
datePublished: 2026-07-29T22:25:04.956Z
cuid: cms6nkln600000akmeza8d22g
slug: building-tic-tac-toe-game-with-kiro
canonical: https://builder.aws.com/content/3HCAlCbFSX0Hti7Ywnx1bGITKxz/building-a-tic-tac-toe-game-with-kiro
cover: https://cdn.hashnode.com/uploads/covers/697b5c79519035959f5d9078/c2cb2a29-7023-4ee5-bc35-d96507b89bfc.jpg
ogImage: https://cdn.hashnode.com/uploads/og-images/697b5c79519035959f5d9078/005b69df-30a1-4e30-9059-8fa5c6f6d19e.jpg
tags: ai, software-development, software-architecture, requirements, ai-agents, spiderman, kiro

---

> *"Most AI tools help you write code. Kiro helps you build software."*

Over the past few years, AI coding assistants have become part of nearly every developer's workflow. We ask them to generate functions, explain errors, scaffold applications, or even debug complex issues—and they do it remarkably well.

But as software engineers, we know that writing code is only one part of building software.

Before the first line of code is written, we define requirements, think about architecture, break work into manageable tasks, review trade-offs, and iterate until we have something we're proud to ship.

That's what makes software engineering different from simply generating code.

Recently, I had the opportunity to explore this idea while hosting my first **Kiro Workshop** for the **AWS Builder Group – Makerere University**. Instead of introducing another AI coding assistant, I wanted students to experience a workflow where AI supports the entire software development lifecycle—from planning to production—not just code generation. Kiro is designed around this spec-driven approach, turning prompts into structured requirements, implementation plans, and code. ([Amazon Web Services, Inc.](https://aws.amazon.com/documentation-overview/kiro/?utm_source=chatgpt.com))

## Why Kiro?

When I first heard about Kiro, I was curious because it described itself as an **AI-powered IDE for software engineering**, not simply an AI code generator.

Instead of asking an AI to build an application with one enormous prompt, Kiro encourages developers to work through a structured development process.

That process includes:

*   Writing clear requirements
    
*   Designing the solution
    
*   Breaking work into manageable tasks
    
*   Implementing features incrementally
    
*   Refining and testing as the project evolves
    

As someone who mentors student developers, that immediately resonated with me.

Many beginners jump straight into writing code. Kiro encourages you to slow down and think first.

And that's a habit worth learning.

## Choosing the Right Project

Every workshop needs a project that's simple enough to finish in one session while still demonstrating meaningful engineering concepts.

I chose **Tic-Tac-Toe**. Not because it's complicated. Because it's deceptively simple.

A Tic-Tac-Toe application introduces:

*   State management
    
*   User interaction
    
*   Game logic
    
*   Win detection
    
*   UI updates
    
*   Component organization
    

Small enough for beginners.

Interesting enough to demonstrate real software engineering.

## Starting With Requirements

One feature that immediately stood out to me was **Specs**.

Instead of opening a blank file and asking AI to generate everything, I started by defining exactly what the application should do.

Our requirements included:

*   A responsive 3×3 game board
    
*   Two alternating players
    
*   Winner detection
    
*   Draw detection
    
*   Restart functionality
    

At first, this felt slower than simply prompting an AI.

But after a few minutes, I realized something.

I wasn't writing prompts anymore.

I was writing software requirements.

That simple mindset shift changed the rest of the development process.

![](https://cdn.hashnode.com/uploads/covers/697b5c79519035959f5d9078/843a579e-3cfd-4603-a9eb-198840b3fb5a.png align="center")

## From Requirements to an Implementation Plan

Once the requirements were complete, Kiro generated a structured implementation plan.

Instead of giving me hundreds of lines of code, it produced a task list that could be completed one feature at a time.

Seeing the project broken into logical steps reminded me of working with an actual engineering backlog.

Rather than asking:

> "Can you build Tic-Tac-Toe?"

I could work through tasks like:

*   Initialize the project
    
*   Create type definitions
    
*   Implement board utilities
    
*   Build the game logic
    
*   Detect winners
    
*   Design the interface
    
*   Add polish and testing
    

For beginners, this is incredibly valuable because it transforms a large project into small, achievable milestones.

![](https://cdn.hashnode.com/uploads/covers/697b5c79519035959f5d9078/c9e54db7-efb0-4e57-9f39-3937c611c217.png align="center")

## Building Feature by Feature

Instead of generating an entire application in one conversation, I let Kiro guide the implementation one feature at a time.

One example was implementing the game logic responsible for handling each player's move.

```ts
const makeMove = (index: number) => {
  if (board[index] || winner.value) return

  board[index] = currentPlayer.value

  if (checkWinner()) {
    winner.value = currentPlayer.value
    return
  }

  currentPlayer.value =
    currentPlayer.value === "X" ? "O" : "X"
}
```

The code itself isn't particularly complex.

What mattered more was that every piece of functionality could be traced back to a requirement and an implementation task.

That structure made development feel much more intentional.

## More Than Just Code Generation

Throughout the workshop, we explored several Kiro features.

### Specs

Probably my favorite feature.

Instead of relying entirely on prompts, Specs encourage developers to think about requirements before implementation.

### Steering

Steering helps maintain consistency across an entire project by giving Kiro project-specific guidance.

Rather than repeating the same instructions over and over, you define them once.

### Hooks

Hooks automate repetitive development tasks.

Although we only explored them briefly during the workshop, I immediately saw their potential for larger projects.

### Model Context Protocol (MCP)

MCP extends Kiro beyond code generation by allowing it to connect with external tools and services.

It's one feature I'm particularly excited to explore in future workshops.

## What Surprised Me Most

Before using Kiro, I assumed it would behave like every other AI coding assistant.

Instead, I found myself thinking less about prompts and more about software engineering.

The workflow encouraged me to:

*   Define the problem clearly.
    
*   Plan before implementing.
    
*   Build incrementally.
    
*   Review progress continuously.
    

That mindset was probably the biggest takeaway from the workshop.

## One Area I'd Love to See Improved

No tool is perfect, and constructive feedback is part of helping products evolve.

While preparing for the workshop, I occasionally ran into situations where an agent appeared to get stuck repeating the same task without making meaningful progress.

During these periods, credits on the free tier continued to be consumed.

For students experimenting with AI-assisted development, every credit matters.

I'd love to see future improvements such as:

*   Better stalled-task detection.
    
*   More transparent progress indicators.
    
*   Easier recovery from looping tasks.
    
*   Smarter handling of long-running agent operations.
    

These improvements would make Kiro even more approachable for students who are just getting started.

## The Workshop

The workshop brought together **28 student developers** from our community.

Together we:

*   Learned Spec-Driven Development.
    
*   Built a complete web application.
    
*   Explored Kiro's workflow.
    
*   Introduced our new AWS Builder Group core team.
    
*   Discussed the future of AI-assisted software engineering.
    

Watching students realize that AI can improve the engineering process, not just generate code, was easily my favorite part of the session.

## Final Thoughts

This workshop reminded me that AI won't replace software engineers.

It will change how we practice software engineering.

The developers who stand out won't simply be the ones who can write the best prompts. They'll be the ones who can define problems clearly, design maintainable systems, evaluate AI-generated solutions, and build software that lasts.

Kiro encourages exactly that mindset.

And that's why I'm excited to keep exploring it with our student community.

## Resources

**Workshop Recording** [https://youtu.be/WR1aQBMB338](https://youtu.be/WR1aQBMB338)

**Presentation Slides** [https://canva.link/dtlm0ydr9ak1afg](https://canva.link/dtlm0ydr9ak1afg)

**Live Demo** [https://kiro-tic-tac-toe-workshop.vercel.app/](https://kiro-tic-tac-toe-workshop.vercel.app/)

**GitHub Repository** [https://github.com/awsclubmuk/kiro-tic-tac-toe-workshop](https://github.com/awsclubmuk/kiro-tic-tac-toe-workshop)

**Meetup Event** [https://www.meetup.com/aws-sbg-at-makerere-university/events/315856984/](https://www.meetup.com/aws-sbg-at-makerere-university/events/315856984/)

Thank you for reading

ev\_Kiran