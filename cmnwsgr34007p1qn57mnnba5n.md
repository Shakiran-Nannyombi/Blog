---
title: "How Backboard.io Transformed My Multi-Agent AI System"
seoTitle: "How Backboard.io Gave My AI Agent Memory"
seoDescription: "I integrated Backboard.io into my AI system to add memory, context, and personalization across sessions and conversations."
datePublished: 2026-04-13T06:05:32.322Z
cuid: cmnwsgr34007p1qn57mnnba5n
slug: how-backboard-io-added-memory-to-my-ai-agent
cover: https://cdn.hashnode.com/uploads/covers/697b5c79519035959f5d9078/d3ce5544-315c-404c-9039-963a30c9c917.png
ogImage: https://cdn.hashnode.com/uploads/og-images/697b5c79519035959f5d9078/c6a7d357-5f95-404e-bc45-d0ee0561ab95.png
tags: hackathon, ai, javascript, machine-learning, backend, apis, developer-tools, backend-developments, apis-testing, ai-agents, AI

---

I built **Londoolink AI** to help users stay on top of their day by generating personalized briefings from emails, calendar events, Notion pages, and social media.

It worked well and pulled together useful insights, but it had one major flaw.

It forgot everything.

Every time a user came back, it was like starting over. Preferences were lost, conversations had no context, and the experience felt repetitive. The system was smart, but it didn’t feel intelligent.

That changed when I integrated **Backboard.io**.

You can view the project here: [https://londoolink-ai.vercel.app/](https://londoolink-ai.vercel.app/)

* * *

## 1\. The Problem: No Memory

Before the integration, users had to:

*   Repeat their preferences every day
    
*   Re-explain what mattered to them
    
*   Ask the same follow-up questions again
    

Even though the system could analyze data well, it didn’t learn from users over time.

## 2\. The Shift to a Stateful System

I first came across [**Backboard.io**](http://Backboard.io) **through an email** after submitting my project to an **Auth0 Hackathon on Devpost**. The team had reached out, sharing more about the platform and how it enables AI systems to become stateful through persistent memory, threads, and tool-calling.

That sparked my curiosity, so I explored it further during **MLH Global Hack Week: API**, where I got to understand more about how it actually works in practice.

What stood out was simple but powerful:

Instead of building memory from scratch, Backboard provides it out of the box.

* * *

## 3\. What Changed

### *Persistent Memory*

Now, users can store preferences like:

*   Preferring meetings in the morning
    
*   Prioritizing certain emails
    

And the system remembers them.

**Here’s a simplified version of how I store preferences:**

This function saves a new piece of memory (like a user preference) for a specific assistant using Backboard’s API.

```python
class BackboardService:
    def add_memory(self, assistant_id, content):
        response = requests.post(
            f"{self.base_url}/assistants/{assistant_id}/memories",
            headers=self.headers,
            json={"content": content}
        )
        return response.json()
```

**Retrieving preferences:**

This function searches stored memories and returns anything related to user preferences so the assistant can personalize responses.

```python
def get_preferences(self, assistant_id):
    response = requests.post(
        f"{self.base_url}/assistants/{assistant_id}/memories/search",
        headers=self.headers,
        json={"query": "user preferences"}
    )
    return response.json().get("memories", [])
```

### *Better Document Retrieval*

I moved from a local setup to a cloud-based system.

This function uploads documents (like notes or data sources) to the cloud so they can be retrieved and used by the AI system later.

```python
def add_document(self, content, metadata):
    return requests.post(
        f"{self.base_url}/documents",
        headers=self.headers,
        json={
            "content": content,
            "metadata": metadata
        }
    )
```

This improved both scalability and search quality.

### *Threaded Conversations*

Now users can ask follow-up questions with full context.

This function creates a conversation thread tied to a specific user so all messages stay connected.

```python
def create_thread(self, user_id):
    response = requests.post(
        f"{self.base_url}/threads",
        headers=self.headers,
        json={"metadata": {"user_id": user_id}}
    )
    return response.json()["thread_id"]
```

Adding messages to a thread:

This appends a new message (from a user or an assistant) to an existing conversation thread to maintain context.

```python
def add_message(self, thread_id, role, content):
    requests.post(
        f"{self.base_url}/threads/{thread_id}/messages",
        headers=self.headers,
        json={"role": role, "content": content}
    )
```

## 4\. How It All Comes Together

In my main agent:

This is the full flow:

*   Get or create an assistant
    
*   Fetch stored user preferences
    
*   Generate a personalized briefing
    
*   Create a conversation thread for follow-ups
    

```python
def create_briefing(self, user_id):
    assistant_id = self.get_or_create_assistant(user_id)

    preferences = self.get_preferences(assistant_id)

    briefing = self.generate_briefing(
        data_sources,
        user_preferences=preferences
    )

    thread_id = self.create_thread(user_id)

    return {
        "briefing": briefing,
        "thread_id": thread_id
    }
```

## 5\. Challenges Along the Way

One issue I ran into was handling API responses.

The API sometimes returned **201 instead of 200**, so I updated my handler:

```python
if response.status_code in (200, 201):
    return response.json()
```

I also had to handle endpoint inconsistencies like `/memory` vs `/memories`, and made response parsing more flexible.

## 6\. The Impact

| Before Backboard | After Backboard |
| --- | --- |
| No memory | Remembers user preferences |
| Generic outputs | Personalized results |
| No conversation continuity | Context-aware conversations |

## 7\. Key Takeaways

*   Memory makes AI feel like an assistant, not just a tool
    
*   A simple service layer keeps integrations clean
    
*   Small API details matter more than you think
    

## 8\. Shoutout 🙌

I learned more about **Backboard.io** during the ongoing **MLH Global Hack Week: API Week 2026**, a week-long online hackathon by **Major League Hacking (MLH)** focused on APIs, building, and learning through live sessions and community challenges.

Big shoutout to the MLH community and organizers for creating an environment where developers can explore tools like this while building real-world projects and learning by doing.

## 9\. Final Thoughts

This integration changed my system from something that generates results into something that understands users over time.

If you’re building AI applications, adding memory is one of the most impactful upgrades you can make.