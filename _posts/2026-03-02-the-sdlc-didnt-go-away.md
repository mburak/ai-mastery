---
layout: post
title: "The SDLC Didn't Go Away"
date: 2026-03-02
categories: [foundations]
tags: [engineering, sdlc, ai-architecture]
image: /assets/images/post-10-hero.png
---

I've seen the SDLC compress three times in my career. Agile compressed the months of upfront design that waterfall required. CI/CD compressed deployments from weeks to seconds. Each time, a phase that dominated the calendar shrank to almost nothing. The focus moved to something new — testing automation, observability, infrastructure as code.

<!--more-->

This time is different. The phase getting compressed is implementation itself. The thing engineers built their careers on.

Last week I wrote a spec for a retrieval change. The spec took two hours. The implementation took fifteen minutes. The review took close to an hour. That ratio would have been inverted at every previous point in my career.

The interesting question isn't where coding went. It's where the work moved to. And unlike previous SDLC shifts, the work didn't move to new disciplines. It moved back to phases we thought we'd already minimized.

Specs are the obvious one. They used to be a paragraph in a ticket, enough to remind you what you were building. Now, when a model can implement almost anything, the spec is the engineering. The bottleneck moved from building to describing.

Design got heavier too. When implementation is cheap, the cost of building the wrong thing is what matters. I used to start coding earlier than I should have because the cost of being wrong was a few hours of rework. Now I sit with the design longer, because the implementation is so fast that the design becomes the bottleneck.

Review is the big one. Most of the code I "write" is code I'm checking. Skimming a PR for obvious bugs is one cognitive task. Vetting AI output that looks confident, formats cleanly, and might be subtly wrong is another. **The skill that used to be a tax on senior engineers reviewing juniors is now the daily work.**

The shape of the SDLC didn't change. The weight on each phase did. The phases that used to be the engineering — implementation, debugging — are getting easier. The phases we used to treat as overhead — specs, design, review — are where the actual engineering now lives.

Every previous compression created new phases. This one made the old ones heavier.
