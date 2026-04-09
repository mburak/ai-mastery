---
layout: post
title: "Why I'm Going Deep"
date: 2026-01-19
categories: [foundations]
tags: [ai-architecture, learning, retrieval, compound-ai]
---

Things are working. I'm shipping.

So why go deep now?

<!--more-->

![](/assets/images/post-4-hero.png)

The honest answer is uncomfortable: staying shallow is easier, and I've been doing it. Making architecture decisions, choosing models, designing retrieval systems — all of it, more or less on vibes. I kept what worked, replaced what broke, and couldn't always tell you why.

That's fine when you're moving fast. Until it isn't.

The clearest example: chunking. When you build a retrieval system, you have to decide how to split documents — chunk size, overlap, whether to chunk by sentence, paragraph, or section. I made those decisions by trying things and seeing what worked. But I didn't understand *why* one worked better than another. And when something went wrong, I was debugging blind — retrieval returning wrong context, the model ignoring what I'd fed it. Guessing at the symptom, not the cause.

There's also a less flattering reason: I co-founded a company where AI is the core technology. Not AI assisted, not AI enhanced — AI is the product. Building on something I don't understand properly started feeling irresponsible. Not in a theoretical way. In a "I'm making expensive decisions here" way.

**The gap isn't just about internals — it's about the whole picture.** Why does chunking strategy affect what the model can do with the context it's given? Why do some evals catch real problems and others just give you false confidence? I've built enough to have questions I can't answer. I haven't built enough to know which questions matter most.

So I'm working through it — by building, not by reading first. Real projects, not tutorials.

I don't know yet if it'll change how I build. But "I'm not sure why this works" stopped feeling acceptable the moment I started making real bets on it.

I'd rather know.
