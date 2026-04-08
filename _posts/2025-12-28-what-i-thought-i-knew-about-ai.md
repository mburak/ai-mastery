---
layout: post
title: "What I Thought I Knew About AI"
date: 2025-12-28
categories: [foundations]
tags: [llm, tokens, compound-ai, karpathy]
---

I've been in the software industry for over 27 years. The last 14 or so I spent in management and leadership, and recently I decided to step away from that and get back to building things. Specifically, I want to get good at AI engineering. Not just using the tools but understanding how they work and how to build with them.

So I started learning. Watching talks, reading papers, going through books. This post is about the first few things that surprised me.

## Why tokens and not words

I've used LLMs plenty, but I never stopped to think about why they work with tokens instead of words. Turns out it's a practical tradeoff. Words are messy. Morphology, compound words, multilingual text. Subword tokenization gives you a fixed vocabulary that can handle any language and any new word by breaking it into known pieces. It's one of those design decisions that seems obvious once you hear it but reveals how much engineering goes into what feels like magic.

## There are two types of language models

I always assumed "language model" meant what GPT does. Predict the next token, left to right. But there's a whole other family: masked language models like BERT that predict missing tokens anywhere in a sequence. These are critical for things like embeddings and search.

The fact that I'd been using AI tools daily without knowing this distinction told me I had more to learn than I thought.

## Systems, not models

The other big shift in my thinking came from reading the Berkeley BAIR blog post on Compound AI Systems. The core idea is that the best AI results today don't come from a single model call. They come from systems that combine models with retrieval, tools, code execution, and control logic.

As an engineer, this framing clicked right away. It's not about having the smartest model. It's about building the right system around it. That's an engineering problem, and it's one I know how to think about.

## What's next

I'm working through the fundamentals now and will be sharing what I learn and build as I go. If you're an engineer getting into AI, I'd like to hear what surprised you too.
