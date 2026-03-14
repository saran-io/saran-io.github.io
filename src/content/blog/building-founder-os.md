---
title: "Building FounderOS - Agents"
description: "SSharing the journey is part of the process — here's why I decided to document everything I build."
date: 2026-03-15
tags: ["building", "founder", "mindset","FounderOS",]
draft: false
---

I was spending 3 hours a day on work that shouldn't require a human.

Not hard work. Not strategic work. The other kind — the kind that feels productive while you're doing it but doesn't actually move anything forward.

Research tabs I'd open and forget. Tweets I'd draft, delete, redraft. Follow-up emails I'd push to tomorrow. NDAs I'd spend 40 minutes on for a 2-hour project. Daily task lists I'd write on paper, lose, rewrite.

I'm Saranraj. I run Tekvo — a small tech company in Tamil Nadu. I don't have a team of 20. I don't have an EA. I have a laptop, a Telegram, and more context-switching than any single person should manage.

At some point I started tracking where my time actually went. The result was uncomfortable.


## The Honest Time Audit


Here's what a typical founder day looked like for me before I fixed it:

Morning (45 min): Scan tech news. Open 12 tabs. Read 3. Close the rest. Write a summary of what I learned in a notes app I'll never open again.

Mid-morning (30 min): Think about posting on X. Stare at a blank draft. Write something. Decide it's not good enough. Close it.

Afternoon (40 min): Someone asks me for an NDA. Pull up a template from 2 years ago. Edit the names. Wonder if the clauses are still right. Send it anyway.

Evening (30 min): Try to remember what I actually accomplished. Write a task list for tomorrow that's really just today's list renamed.

Daily total: ~2.5 to 3 hours. Every day.

None of this required my judgment. None of it needed my specific expertise. It just needed time — and I was the only person available to give it.


## Why I Didn't Just Buy a Tool

The obvious answer is: use a tool. Subscribe to something. Automate it.

I tried that. I have subscriptions to three tools I barely use, a Notion setup that felt like a productivity system until I had to actually use it under pressure, and a content calendar that's been "in progress" since October.

The problem with buying tools is that they're built for a general user. They optimize for the median workflow, not yours. You spend as much time adapting to the tool as you do doing the work.

I'm a software person. I build things. So I asked a different question:

What if the tool knew exactly how I work, what I care about, what my company is, and what good output looks like for me specifically?

That's not a SaaS product. That's a custom system. And the only way to get it is to build it.


## Why I Didn't Just Buy a Tool


I started calling it a "Founder OS" — not because it's a grand product, but because that's literally what I needed. An operating system for how I run my work.

Not an AI assistant that answers questions when I ask. Not a chatbot. A system that runs in the background, executes scheduled work, and surfaces what I need to know — without me having to remember to ask.

Here's what I built:

6 agents, each with a specific job:

Recon — runs three times a day and produces an intelligence report on what's happening in AI, tech, and my industry. I wake up knowing what matters without opening a single tab.

Broadcast — reads Recon's intel and drafts social content for X and LinkedIn. I get options in my Telegram. I approve, edit, or skip. The good ones get posted.

Brief — writes a weekly newsletter draft based on the week's intel. I edit and send. First draft done without me.

Engineering — monitors my codebase, flags technical debt, reviews priorities. Runs every weekday morning.

TekOps — handles business operations. Daily task digest. And now: generates NDAs. Client name, type of agreement, scope — it drafts the full document and sends it to my Telegram as a .docx ready to review.

Command — the coordinator. Runs heartbeat checks. Takes messages I send directly and routes them to the right agent. My Telegram interface to everything.

Total infrastructure cost: $4.20/month on a Hetzner server.

Total Claude API cost at current usage: ~$8–15/month (I'm implementing prompt caching which will cut this in half).

So for roughly the cost of two cups of coffee a month, I have a system that does 2.5 hours of my daily work.


## What It Feels Like to Use
I open Telegram in the morning. Recon's intel is already there. Broadcast has two tweet drafts waiting. TekOps has flagged that I have a follow-up due today.

I spend 15 minutes reviewing instead of 45 minutes producing.

When a client needs an NDA, I type /nda ClientName, mutual, 2-year, software consulting in Telegram. 45 seconds later I have a .docx with Tekvo's legal entity, the right governing law for India, all the standard clauses, and a review checklist. I read it, make one or two edits, send it.

That used to take 40 minutes. Now it takes 4.

I'm not claiming it's perfect. Recon doesn't have real web access yet — that's the next thing I'm fixing. Some drafts aren't good enough to post. The system is still being tuned. But even at 70% quality, the time savings are real and they compound every single day.

I'm Saranraj, founder of Tekvo . Building Products Writing about AI systems that actually work for solo founders.

