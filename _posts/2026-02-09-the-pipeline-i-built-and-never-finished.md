---
layout: post
title: "The Pipeline I Built and Never Finished"
date: 2026-02-09
categories: [foundations]
tags: [rag, embeddings, retrieval, vector-db]
image: /assets/images/post-7-hero.png
---

I built a pipeline that ingests Obsidian notes, chunks them, embeds them, and syncs them to a vector database. Delta processing, performance benchmarks, a full test harness.

I never implemented the retrieval layer.

<!--more-->

It normalizes markdown, tracks changes via SHA256 checksums, chunks notes at 500 words with 100-word overlap, embeds them using [text-embedding-3-large](https://platform.openai.com/docs/guides/embeddings){:target="_blank"}, and upserts into Supabase via [pgvector](https://github.com/pgvector/pgvector){:target="_blank"}. On typical runs where most notes haven't changed, it skips roughly 60% of the work.

The chunking parameters deserve some honesty. 500 words and 100-word overlap weren't principled decisions — my AI assistant suggested them and I ran with it. I know there's a tradeoff between semantic coherence (bigger chunks) and retrieval precision (smaller chunks), but I couldn't tell you where the optimal point is for my specific data. The pipeline is built on assumptions I can't fully defend.

**What I didn't build is the interesting part.** The ingestion pipeline is infrastructure. The actual product would be the retrieval layer: given a query, find the most relevant chunks, assemble context, feed it to a model. That's where you find out if your chunking was right, if your embeddings are capturing the right semantics, if your similarity thresholds make sense. I never got there.

The ingestion was what I wanted to learn. By the time it was built, I'd learned it — and had other things to build. The infrastructure was clean and the tests passed, but I built the loading dock without building the store.

What I'd do differently: start with retrieval. Build the simplest possible ingestion first, then immediately test whether you can retrieve what you put in. The quality of your retrieval tells you everything about whether your ingestion decisions were right.
