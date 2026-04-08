---
layout: post
title: "What I Thought I Knew About AI"
date: 2025-12-28
categories: [foundations]
tags: [llm, tokens, compound-ai, karpathy]
---

A few weeks ago I was explaining to someone how LLMs work. I said something like "they predict the next word based on all the previous words." Confident. Casual. The kind of thing you say when you've used ChatGPT and Claude every day for a year and you figure you get the gist.

Turns out I was wrong about almost every part of that sentence.

I've been in the software industry for over 27 years. I've gone back and forth between building things and leading teams. I've been into AI for a while — courses, side projects, building apps with AI coding assistants — but recently I decided to go deep. Not just using the tools but understanding how they work. Pretty quickly I realized the gap between "I use AI" and "I understand AI" was a lot bigger than I expected.

## They don't even use words

The first thing that got me was tokens. LLMs don't operate on words at all. They use subword tokens, pieces of words broken up by an algorithm called [byte pair encoding](https://en.wikipedia.org/wiki/Byte-pair_encoding). Words are messy, so a fixed vocabulary of subword pieces can handle any language by breaking everything into known chunks.

I'd typed millions of words into these tools without ever thinking about what was actually happening on the other side. That was a humbling start.

## There's a whole other kind of language model

I always assumed "language model" meant what GPT does. Feed it text, predict the next token, left to right. That's an autoregressive model. But there's another family I'd never heard of: masked language models, like [BERT](https://research.google/blog/open-sourcing-bert-state-of-the-art-pre-training-for-natural-language-processing/). Instead of predicting what comes next, they predict missing tokens anywhere in a sequence. This matters because masked models are what power embeddings and semantic search, the kind of thing that makes RAG work. I'd been using products built on both types every day without knowing there were two types.

## The thing that actually changed how I think

The real shift came from a Berkeley blog post about [Compound AI Systems](https://bair.berkeley.edu/blog/2024/02/18/compound-ai-systems/). The argument is simple: the best AI results today don't come from one model doing everything. They come from systems. A model plus retrieval plus tools plus code execution plus control logic, all wired together.

That landed differently for me than the technical stuff. Building systems is what I've done my entire career. Decomposing problems, designing interfaces, handling failure modes, thinking about scale. **That's not an AI skill. That's an engineering skill.** I went from thinking I needed to become an ML researcher to realizing I needed to become an engineer who understands ML well enough to build real systems with it. Those are very different goals, and the second one felt a lot more like me.
