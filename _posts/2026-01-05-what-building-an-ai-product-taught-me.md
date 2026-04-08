---
layout: post
title: "What Building an AI Product Taught Me About Engineering"
date: 2026-01-05
---

In late December I wrote about what surprised me when I started going deep on AI. By January I was building something real. That's when the actual lessons started.

The first thing I realized is that the AI part is not the hard part. Or at least, it's not the part that takes the most thinking. The hard part is everything around the AI — how data gets in, how you validate what comes out, how you handle the cases where the model gets it wrong.

I spent years designing systems. Queues, APIs, data models, failure modes. I assumed AI products would be a fundamentally different kind of work. They're not. **They're system design problems with a probabilistic component in the middle.**

Say you're building a pipeline that takes unstructured input, extracts useful information, and turns it into something a user can act on. That's not a new pattern. Engineers have been building ETL pipelines forever. The difference is that one of your transformation steps is now a language model, and language models are confident, fast, and *sometimes wrong*.

So you end up spending a lot of time on the edges. Input validation. Output schemas. Confidence thresholds. Fallback behavior for when the model isn't sure. Human review steps. These aren't AI problems. They're engineering problems. And that was reassuring — until I realized I was still getting the scope wrong.

The other big lesson was about scoping. When you're building with AI, your feature list grows faster than you can think. The model can do so many things. Every conversation with it gives you three new ideas. I had to be ruthless about what the MVP would NOT do. I probably cut more features than I kept. That discipline felt more important than any architecture decision I made.

And that [compound AI](https://bair.berkeley.edu/blog/2024/02/18/compound-ai-systems/){:target="_blank"} idea from the research papers? It's not theoretical. When you're building something real, you naturally end up with multiple models or multiple calls doing different jobs. One step extracts text. Another classifies it. Another pulls out structured data. Another generates something human readable. Each step has its own failure mode, its own evaluation criteria, its own place where things can quietly go wrong. It's not one model doing everything. It's a pipeline, and the pipeline is the product. The model is just one part of it.

The thing I got most wrong was thinking I needed to figure out the AI before I could design the system. It was the opposite. I needed the system design to know what to ask of the AI.
