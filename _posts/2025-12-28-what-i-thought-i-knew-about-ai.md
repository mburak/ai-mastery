---
layout: post
title: "What I Thought I Knew About AI"
date: 2025-12-28
categories: [foundations]
tags: [llm, tokens, compound-ai, karpathy]
---

A few weeks ago I was explaining to someone how LLMs work. I said something like "they predict the next word based on all the previous words." Confident. Casual. The kind of thing you say when you've used ChatGPT and Claude every day for a year and you figure you get the gist.

Turns out I was wrong about almost every part of that sentence.

I've been in the software industry for over 27 years. The last 14 or so I spent in management and leadership. Recently I stepped away from that because I wanted to get back to building things, specifically in AI. Not just using the tools but actually understanding how they work. So I started digging in. Reading books, watching talks, going through papers. And pretty quickly I realized that the gap between "I use AI" and "I understand AI" was a lot bigger than I expected.

## They don't even use words

The first thing that got me was tokens. LLMs don't operate on words at all. They use subword tokens, which are pieces of words broken up by an algorithm called byte pair encoding. The reason is practical: words are messy. Different languages, different forms of the same word, compound words. A fixed vocabulary of subword tokens can handle all of that by breaking any word, in any language, into known pieces.

I'd typed millions of words into these tools without ever thinking about what was actually happening on the other side. That was a humbling start.

## There's a whole other kind of language model

I always assumed "language model" meant what GPT does. You feed it some text, it predicts the next token, left to right. That's called an autoregressive model. But there's another family I'd never heard of: masked language models, like BERT. Instead of predicting what comes next, they predict missing tokens anywhere in a sequence.

This matters because masked models are what power embeddings and semantic search. The kind of thing that makes RAG systems work. I'd been using products built on both types of models every day without knowing there were two types.

## The thing that actually changed how I think

The real shift came from a Berkeley blog post about Compound AI Systems. The argument is simple: the best AI results today don't come from one model doing everything. They come from systems. A model plus retrieval plus tools plus code execution plus control logic, all wired together.

That landed differently for me than the technical stuff. Because building systems is what I've done my entire career. The instinct to decompose a problem, design the right interfaces, handle failure modes, think about what happens at scale. That's not an AI skill. That's an engineering skill.

It reframed the whole thing for me. I went from thinking I needed to become an ML researcher to realizing I needed to become an engineer who understands ML well enough to build real systems with it. Those are very different goals, and the second one felt a lot more like me.

## What's next

I'm going deep on the fundamentals now. I'll be writing about what I learn, what I get wrong, and eventually what I build. If you're an engineer making a similar move into AI, I'd like to hear what surprised you too.
