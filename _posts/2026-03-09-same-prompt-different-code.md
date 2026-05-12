---
layout: post
title: 'Same Prompt, Different Code'
date: 2026-03-09
categories: [foundations]
tags: [engineering, ai-architecture, debugging]
image: /assets/images/post-11-hero.png
---

Last week I ran the same prompt against the same model twice in a row. Both attempts produced working code. The implementations were different.

<!--more-->

That's not a bug. It's how these systems work. And it's the part of working with AI that took me longest to accept.

I've worked with non-deterministic systems for most of my career. Race conditions, eventually-consistent databases, distributed timing bugs. The plumbing of any real production system is non-deterministic — you don't know what order things will happen in, when messages will arrive, whether a write made it to the replica yet.

This is different. The non-determinism isn't in the plumbing. It's in what the system is actually trying to do.

Race conditions had a fix: better synchronization, better isolation, better failure handling. The bug was deterministic; you just had to find it. With a model, the "bug" might be in the variance itself. Two outputs can both be technically correct and substantively different. There's no synchronization to add. You can lower the temperature and the variance shrinks, but it doesn't vanish.

That changed how I debug. Reproducing a problem used to mean finding the exact inputs and replaying them. Last month I spent half an hour reproducing a bug I had hit. I had to run the same prompt about thirty times before I saw it twice.

It changed how I test. The old question was "did this input produce that output." The new question is "did this input produce an output that satisfies these properties." Tests look more like contracts now — ranges, shapes, invariants. Less "exactly this string" and more "a string that does X."

And it changed where my confidence comes from. I used to feel confident when I'd traced a path through the code and seen exactly why something worked. Now confidence comes from running the thing enough times to know its distribution. That's a colder, more statistical kind of confidence than I'm used to. It works, but it doesn't feel the same.

The rigor isn't gone. It moved. **Engineering used to be about controlling what a system does. Now it's also about characterizing what it might do.**

I'd worked with non-determinism for twenty years before this. None of it prepared me for this kind.
