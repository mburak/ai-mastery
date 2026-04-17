---
layout: post
title: "What Actually Slows You Down"
date: 2026-02-16
categories: [foundations]
tags: [ai-coding, workflow, productivity, specs]
image: /assets/images/post-8-hero.png
---

Everyone talks about hallucinations and trust. Those aren't what slow me down.

<!--more-->

The real friction is the gap between how fast you can build with AI and how well you understand what you've built. That gap is fine in the moment. It's expensive later.

**The clearest example is the understanding gap.** The AI writes code. It looks right. I move on. Later something breaks and I have to debug code I don't fully understand — code I didn't write and didn't read carefully enough when it was generated. The bug isn't the expensive part. The archaeology is — re-reading generated code under pressure, trying to reconstruct what it was supposed to do and why it was structured that way.

It compounds with state of mind. When I'm sharp I ask the AI to explain what it did before moving on. When I'm tired I ship and hope. I've learned to notice which kind of session I'm in — but I don't always act on it. The tell is usually when I find myself accepting an output without really reading it, just running it to see if it works.

**Context loss is the same problem at a different scale.** Every new session starts cold. The decisions made yesterday, the constraints established last week, the reason a particular approach was chosen — none of it carries over. I re-explain things I've already explained. And when a session runs long, the AI starts quietly contradicting earlier decisions without flagging the change. The context drifts because I'm moving faster than I'm documenting.

**Spec drift is the long-term version.** The AI makes small changes that weren't in the spec — usually reasonable, often unnoticed. They accumulate. At some point the spec and the code have diverged and neither is fully the source of truth. The longer I go without reconciling them, the worse the debt gets.

Three different problems, same root cause. You can build fast with AI. The cost shows up when you have to go back.
