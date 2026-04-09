---
layout: post
title: "I Didn't Go Back to Coding"
date: 2026-01-12
categories: [foundations]
tags: [ai-assisted-coding, vibe-coding, specs, productivity]
---

In April 2024 I built an iOS and Android app using GPT-4. It was mostly a disaster.

<!--more-->

![](/assets/images/post-3-hero.png)

The pattern was always the same. The AI would generate code. Something would break. I'd paste the error log and explain what was wrong. The AI would say "I understand" and generate slightly different broken code. Repeat. I was spending more time fighting the tool than building the product.

I blamed the AI. Partly I was right — the models were weaker then. But I was also doing it wrong. I was vibe coding before I knew that's what it was called. No specs, no structure, just "make this thing work" back and forth until one of us gave up.

Through 2025 the models improved steadily. Claude 3.5 Sonnet and GPT-4o were noticeably better — fewer loops, more coherent outputs. Things got easier, but the real click came in late 2025 with [Claude Opus 4.5](https://www.anthropic.com/news/claude-opus-4-5){:target="_blank"}. That's when I stopped fighting and started steering.

I started writing proper specs upfront: the data model, the behavior, the edge cases, the interfaces. Before a single line of code. The AI would work from those, I'd review what came back, and the loop got dramatically shorter.

I built a pipeline that ingests Obsidian notes, chunks them, embeds them, and syncs to a vector database — with delta processing, performance benchmarks, and a full test harness. A year earlier that would have been a week of work for a small team, or something I'd have scoped down to a toy. I built it alone, and it would hold up in production.

Somehow it didn't feel like going back to coding. It felt like I'd moved up a level.

I've returned to IC roles before — the last time was five years ago, coming back from an EM stretch. You shake off the rust, relearn some syntax. This wasn't that. I wasn't writing code — I was writing specs and reviewing outputs. That's closer to architecture than implementation — honestly, more like what I was doing as an engineering manager than as a senior IC.

And I didn't miss it. The writing-every-line part. I never cared about the language — I cared about building the best product possible. AI just removed the distance between the two.

The engineers who struggle most with this, I think, are the ones who loved the craft of writing code for its own sake. For them something is genuinely lost. For me it turns out I was always building at the wrong abstraction. Now I'm not.
