---
layout: post
title: "A Fleet, Not a Default"
date: 2026-04-13
categories: [foundations]
tags: [engineering, ai-architecture, cost]
image: /assets/images/post-16-hero.png
---

Most takes on AI tools assume one model. Pick the best, use it everywhere. That's not how I work.

<!--more-->

I use four model families day to day. Claude for most of my coding. GPT for second opinions on hard decisions. Gemini for PR reviews on GitHub. Open-source where it's the best fit.

The reason is cost — or rather, not overpaying for capability I don't need.

If I used the most capable model for every prompt, my monthly bill would be off by an order of magnitude. Opus adds up fast. Haiku is nearly free. For dozens of prompts an hour, that math compounds.

So the question isn't "which model is best?" It's "which model is good enough for this task at the lowest price?"

My rough mapping:

- Hard coding problems, novel logic, architecture decisions → Opus. The depth shows up where it matters.
- Routine refactors, well-defined tasks → Sonnet. Cheaper, capable enough, faster.
- Quick reformatting, simple lookups, throwaway prompts → Haiku. Pennies. No reason to spend more.
- PR reviews on GitHub → Gemini. Integrated, cheap, different perspective from my coding model.
- Second opinion on hard decisions → GPT-5. Different training, different blind spots.

The same logic works at every scale. Qwen does OCR well enough — and cheaper than the closed alternatives. DeepSeek is well-tuned for certain classification work. GPT-5 might do these better, but I don't need better. And inside a single provider, an older model is often the right pick when the newest one is overkill.

For months I defaulted to Opus on everything — commits, changelogs, doc updates, reformatting. The work didn't need that depth. Routing routine work to Haiku dropped my bill considerably without anything getting worse.

The mistake is using the wrong end of the spectrum. The other direction is worse: using a small model on a problem that needs depth. The small one gives you confident wrong answers. You don't notice. You ship the wrong thing.

**The model isn't a tool you use. It's a fleet you allocate.**

Each task gets the right model at the right price. The skill is calibrating — what's good enough, when to pay up, when not to.

Cost stops being a billing question and becomes an architectural one. How you spend tokens shapes what you build.
