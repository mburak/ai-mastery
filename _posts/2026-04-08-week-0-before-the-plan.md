---
layout: post
title: "What I Thought I Knew About AI"
date: 2026-04-08
categories: [foundations, pre-work]
tags: [llm, tokens, compound-ai, karpathy]
---

I've been a software engineer for over 20 years. The last five I spent in management, and lately I've been wanting to get back to building things. Specifically, I want to get good at AI engineering. Not just using the tools but actually understanding how they work and how to build with them.

So I started learning. This post is about the first few things that surprised me.

## Why tokens and not words

I've used LLMs a lot but never really thought about why they work with tokens instead of words. Turns out words are just too messy. Different languages, different forms of the same word, compound words. Subword tokenization solves this by breaking text into smaller pieces from a fixed vocabulary. It can handle any language and any new word it hasn't seen before. It makes a lot of sense once you see it, but I had never thought about it.

## There are two types of language models

I always assumed "language model" meant what GPT does. Predict the next token, left to right. But there's another kind: masked language models like BERT. Instead of predicting what comes next, they predict missing tokens anywhere in a sentence.

Turns out these are really important for things like embeddings and search. I had no idea. I always just thought of the autoregressive type since that's what ChatGPT and Claude use.

## Systems, not models

I also read a blog post from Berkeley about Compound AI Systems. The main idea is that the best AI results don't come from a single model call. They come from combining models with search, tools, code execution, and other components.

As an engineer this made a lot of sense to me. It's not about having the smartest model. It's about building the right system around it. That's just good engineering.

## What's next

I'm working through the fundamentals now and will be sharing what I learn and build as I go. If you're an engineer getting into AI I'd like to hear what surprised you too.
