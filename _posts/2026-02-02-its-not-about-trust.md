---
layout: post
title: "It's Not About Trust"
date: 2026-02-02
categories: [foundations]
tags: [ai-coding, verification, failure-modes, workflow]
image: /assets/images/post-6-hero.png
---

The code looked right. I reviewed it. It passed.

Another model caught the bug.

<!--more-->

That happens more than I'd like to admit. Not because I'm careless — I do check. But code written with an [AI coding assistant]({{ site.baseurl }}{% post_url 2026-01-12-i-didnt-go-back-to-coding %}){:target="_blank"} can be syntactically correct, stylistically clean, and logically wrong in a way that's easy to miss on a read-through. The bug usually lives in an edge case, not in the obvious path.

What I took from that: the review isn't optional. And I can't always trust my own review either.

So I built verification into my coding workflow. First, I ask the same model that wrote the code to review it — not to regenerate it, just to reason about what it actually does versus what it was supposed to do. The generation context and the review context are different enough that it often catches things it missed the first time. Then a second model does multiple passes with different prompts — looking for logic errors, edge cases, type issues. A third goes deeper on anything that matters.

Tests are part of it too — deterministic where model review is probabilistic. But the relationship isn't clean. Model review regularly finds edge cases that tests missed, even when you thought your coverage was solid.

That's the reframe that actually helped. "Do I trust this output?" is the wrong question. It puts you in a binary. It makes you decide case by case, based on how confident the output looks — which is exactly when you're most likely to miss something. The outputs that are *confidently* wrong look just like the outputs that are *confidently* right.

**The better question is: where does this system fail?** Once you know that, verification isn't a trust judgment. It's a checklist. [Off-by-one errors](https://en.wikipedia.org/wiki/Off-by-one_error){:target="_blank"} in edge cases. Null handling that works on the happy path but silently breaks elsewhere. And the hardest to spot: the model solving a slightly different problem than the one you asked — it interprets ambiguity in your prompt and resolves it confidently, without flagging that it made a choice. You don't notice until the edge case hits.

The models have gotten significantly better over the past year. My verification approach hasn't changed. The error rate went down but the stakes didn't. If anything, better models introduce a new risk — you trust the output more, so you check less carefully, and the errors that slip through are the ones you're least prepared for.

Building verification in means I don't have to make that judgment call every time. It's not about trust. It's about knowing where to look.
