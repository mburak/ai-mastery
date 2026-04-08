---
layout: post
title: "Week 0: What I Thought I Knew About AI (And What I Didn't)"
date: 2026-04-08
categories: [foundations, pre-work]
tags: [llm, tokens, compound-ai, karpathy]
---

I've been a software engineer for over 20 years. The last five I spent in management, and now I'm making a deliberate move back into building — specifically, into AI engineering. Not dabbling. A structured, 24-week deep dive from foundations to production systems.

This post covers what I learned during pre-work week, before the real plan starts on Monday.

## Two things that surprised me

### 1. Why tokens, not words

I'd used LLMs plenty, but I'd never stopped to think about *why* they operate on tokens instead of words. Turns out it's a practical tradeoff: words are messy (morphology, compound words, multilingual text), while subword tokenization gives you a fixed vocabulary that can handle any language and any novel word by breaking it into known pieces. It's one of those design decisions that seems obvious in hindsight but reveals how much engineering goes into what feels like "magic."

### 2. There are two types of language models

I always assumed "language model" meant what GPT does — predict the next token. Autoregressive, left-to-right. But there's a whole other family: masked language models (like BERT) that predict missing tokens anywhere in a sequence. These turn out to be critical for embeddings and search — areas I'll hit in a few weeks when I get to RAG systems.

The fact that I'd been using AI tools daily without knowing this distinction tells me exactly why I need this plan.

## Compound AI systems > single models

The other big shift in my thinking came from reading the Berkeley BAIR blog post on Compound AI Systems. The core argument: the best AI results today don't come from a single model call. They come from systems that combine models with retrieval, tools, code execution, and control logic.

As an engineer, this framing clicked immediately. It's not about having the smartest model — it's about building the right system around it. That's an engineering problem, and it's one I know how to think about.

## What's next

Monday I start Phase 1: foundations and modern tooling. Python refresher, FastAPI, Docker, and my first real project — a deployed API service. I'll be posting weekly updates on what I learn and build.

If you're an experienced engineer making a similar transition into AI, I'd love to hear what surprised you too.

---

*This is part of my [24-week AI mastery plan](https://github.com/mburak/ai-mastery). Week 0 of 24.*
