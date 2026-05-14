---
layout: post
title: "An Assistant Is More Than a Model"
date: 2026-05-11
categories: [foundations]
tags: [engineering, ai-architecture, coding-assistants, tools]
image: /assets/images/post-20-hero.png
---

GPT-5.5 dropped three weeks ago. It leads Claude Opus 4.7 by thirteen points on Terminal-Bench 2.0 and wins on most coding evals. The benchmarks are real. The numbers aren't marketing.

<!--more-->

The question I keep getting: am I switching from Claude Code to Codex?

And yet the market mostly hasn't switched. Three weeks in, Claude Code is still the most popular agentic coding tool with professional developers. That gap — between a clear model-level win and the slow assistant-level adoption — is the interesting part.

Benchmarks measure the model. You're picking the assistant.

An assistant is the model plus everything around it. The agent loop. The way it reads and respects your repo conventions. The memory layer (CLAUDE.md, AGENTS.md, or whatever your tool persists across sessions). The MCP servers and tools it can reach. The terminal vs IDE integration. The UX of approving diffs, watching it think, redirecting mid-task.

A new state-of-the-art model improves one of those things. The rest stay the same.

What changes when you switch assistants:

- The memory model. Each tool has its own conventions for what gets read every turn vs what sits in the conversation. You rewrite your project context. You re-learn what to put where.
- The tool ecosystem. MCP servers, skills, integrations you've added — they're tied to the assistant, not the model. Switching means rebuilding or losing them.
- The agent loop's failure modes. Each assistant has its own way of looping, exiting, asking for clarification, retrying. The model is only one input into how that loop behaves.
- The keyboard and how it feels to use. The small things — how it shows diffs, how you interrupt, how you point it at a file — add up to hours per week.

A 13-point benchmark gap on Terminal-Bench is genuinely a win for the model. It's not a 13-point gap on your daily work. Your daily work runs through the whole assistant.

**Switching the model is a question. Switching the assistant is a migration.** And migrations are expensive even when the destination is better.

I considered testing Codex. I decided not to. Recreating my workflow inside it — CLAUDE.md, MCP servers, the rituals around how I review and ship — is exactly the kind of effort I'm not willing to spend to find out whether the new model is meaningfully better for my work. The migration cost isn't theoretical.

GPT-5.5 is genuinely strong, and the field reports back that up for agentic one-shot work. The right move isn't switching assistants. It's putting the new model where it earns its place — second opinions, hard one-shot tasks, tasks the current assistant can route to it without rewiring my main loop.

The fleet extends to assistants too. You don't have to pick one.
