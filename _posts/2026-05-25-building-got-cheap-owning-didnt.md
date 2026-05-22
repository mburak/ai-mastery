---
layout: post
title: "Building Got Cheap. Owning Didn't."
date: 2026-05-25
categories: [foundations]
tags: [engineering, scope, yagni]
image: /assets/images/post-21-hero.png
---

About thirty percent of what I built for my MVP was scope I wouldn't have built if it weren't cheap. Features, options, configurations, niceties that the AI made trivial to add. None of them are wrong. None of them are useful, either.

<!--more-->

That's the thing about cheap implementation. It removes the friction that used to filter for what was worth building.

For most of my career, MVP discipline wasn't a virtue I had. It was a tax I paid. Every feature cost real hours of typing, debugging, fixing. The cost was the filter. "Do I really need this?" wasn't a values question. It was a math question. The math said no most of the time.

AI changed the math. A feature that used to take a day now takes an hour. A config option that used to take an afternoon takes ten minutes. The marginal cost of "while we're at it" dropped to a level where "while we're at it" wins every time.

What didn't change: ownership. I still have to read it. Debug it when something breaks. Update it when the model changes. Test it when I refactor. Re-learn it when I haven't touched it in months. Migrate it when the framework moves. None of that got cheaper. None of it scales with the speed of building.

Each piece was cheap to add. Each piece is cheap to keep. But they compound. Every refactor sweeps wider. Every migration touches more. Every bug has more places to hide. The cost isn't in any single feature — it's in how they accumulate. I traded a small expense at build time for a recurring, compounding expense over the life of the product.

**Building got cheap. Owning didn't.**

The question used to be "can I build this?" The cost of typing forced it. The new question has to be "do I want to own this?" Same instinct, different time horizon. Cheap to build, expensive to have.

Earlier in my career I learned a sharper question than either of those: "is this the most impactful thing I could be working on?" That question doesn't care about the cost of building. It cares about whether the work matters. It was the right question when building was expensive. It's the right question now that building is cheap.

The friction was doing work. The work was filtering. With the friction gone, the filter has to be deliberate. Less is still more — just for different reasons now.
