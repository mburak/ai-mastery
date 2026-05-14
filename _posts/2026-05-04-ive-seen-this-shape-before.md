---
layout: post
title: "I've Seen This Shape Before"
date: 2026-05-04
categories: [foundations]
tags: [engineering, ai-architecture, agents]
image: /assets/images/post-19-hero.png
---

Last month I was sketching the architecture for an agent — a multi-step workflow where the model decides what to do next, calls a tool, evaluates the result, plans the next step. Halfway through the diagram I realized I'd drawn this before. Many times. In other jobs, other decades.

<!--more-->

Different domain, different vocabulary, same shape.

A model in a loop. A controller that decides which tool to invoke. A state machine of intermediate results. Tool descriptions that are essentially API specs. Termination and retry logic.

I built ETL pipelines like this in the early 2000s. I built orchestration systems like this in the 2010s. The control flow was always: receive input, decide on operation, invoke, check result, decide next. The thing in the middle was different — rules in the ETL era, code in the orchestration era, an LLM now. The shape stayed.

This isn't a complaint. It's a relief. It means I have context for what an "agent" actually is. I know which parts are hard (state management, observability, failure recovery, idempotency). I know which parts go wrong first (the controller). I know how to think about scale: not until I have to.

What's actually new isn't the shape. It's the thing in the middle. A controller that can read natural language tool descriptions, reason about which one fits, generate arguments, interpret results — that's new. The protocol for calling tools (structured outputs, function schemas) is new. The kinds of failure modes (hallucinated tool names, premature exits, infinite loops) are new.

Calling the whole pattern "agentic" is fine. Calling it brand new isn't.

Right now, half of what's being marketed as an agent is something we already had a name for. Some of it is rebadged RPA. Some of it is a scripted workflow with an LLM step. Some of it is a chat interface with three function calls glued on. The buzzword is masking pattern recognition that engineers should be doing.

**This isn't dismissal. It's defense. The pattern is well-understood, even when the term sounds new. You can reason about agents from existing engineering knowledge.**

The hype cycle says we're at peak inflated expectations. Most of the discourse is either evangelical or cynical. The useful position is somewhere else: this is a shape I know how to build, with one genuinely new piece in the middle. Treat it like that.
