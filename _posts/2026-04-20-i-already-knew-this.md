---
layout: post
title: "I Already Knew This"
date: 2026-04-20
categories: [foundations]
tags: [engineering, learning, ai-engineering, reading]
image: /assets/images/post-17-hero.png
---

I read Chip Huyen's [*AI Engineering*](https://www.amazon.com/AI-Engineering-Building-Applications-Foundation/dp/1098166302){:target="_blank"} last month. Twenty-seven years of engineering meant most of it was familiar territory. Distributed systems. Reliability. Pipeline design. Cost-aware architecture. The patterns mapped onto things I'd been doing for decades.

<!--more-->

That's not why the book hit.

The book hit because it gave me names for things I'd been doing by intuition.

I'd been comparing model outputs across runs to gut-check quality. The book called it eval methodology — a structured discipline with criteria, datasets, judges, and validation.

I'd built a retrieval pipeline that mostly didn't work and never knew exactly why. The book had a taxonomy: retrieval failures, generation failures, integration failures. Each with a different cause.

I'd been routing different tasks to different models for cost. The book had vocabulary for it — compound systems, model routing, the tradeoffs between them.

The names matter more than I expected. Intuition runs alone in your head. Names let you reason with other people about the same thing. They let you defend choices. They let you compose patterns. They let you teach.

Last week I was writing a spec for an eval pipeline. I caught myself mixing two different evaluation patterns. A month ago I'd have written "something's off here, think harder" in a comment and moved on. Now I had words. I named the patterns, split them, the spec sharpened. The vocabulary did real work.

For most of my career, the senior engineer's edge was pattern recognition you couldn't articulate. The patterns were real. The articulation was post-hoc, if it existed at all. New engineers worked alongside you and absorbed it by watching.

**This is a new field. Articulation isn't optional. The vocabulary is racing the practice.**

I came out of the book the same engineer I went in. But now I have words. And the words let me think in a way I couldn't before.
