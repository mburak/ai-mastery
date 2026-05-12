---
layout: post
title: "The One Process Can't Fix"
date: 2026-04-06
categories: [foundations]
tags: [engineering, ai-architecture, debugging]
image: /assets/images/post-15-hero.png
---

When people list what AI is bad at, the same examples come up. Hallucinations. Math. Counting letters. Those are real, and mostly easy to work around — you know they're coming.

<!--more-->

There's a tier of failures below the famous ones. They were harder to spot and they used to cost me a lot.

I'd ask the model to update one function and get back changes to three more. I'd explain a constraint in chat and watch it get ignored two turns later. I'd write code in a deliberately terse style and have it rewritten "for clarity" the next time I touched the file.

I built process around most of these. Specs in files. Plans broken into tasks. Constraints written down where the model can read them every turn instead of relying on the conversation. The instruction drift and the unwanted refactors mostly went away.

The over-complexification didn't.

I'll ask for the smallest possible change. The response will include the change plus a few "improvements." I'll say "no tests, no error handling, no docstrings." I'll get the change with one docstring. The model has its own idea of what good code looks like, and it leaks through every constraint I write.

This isn't laziness or context loss. It's a bias in the training. The model has seen a lot of "production-grade" code — error handling, tests, type hints, documentation, fallbacks — and it has learned that "good code" looks like that. Even when I tell it explicitly: smaller, less, just this — the bias toward completeness shows up at the margins.

**This is a failure that process can't fix. The model isn't ignoring my constraint. It's working against a stronger prior.**

The other failures yielded to a written spec. This one needs me at the diff, every time. Reading carefully. Stripping what I didn't ask for. Saying "smaller" until the diff is actually smaller.

The famous failures are the ones you hear about. The unnamed ones are the ones you build process around. This one is the one I keep stripping out by hand.
