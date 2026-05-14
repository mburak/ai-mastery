---
layout: post
title: "Tests Stopped Being Boolean"
date: 2026-04-27
categories: [foundations]
tags: [engineering, ai-engineering, testing, evals]
image: /assets/images/post-18-hero.png
---

A unit test asks one question: does this input produce that output. Pass or fail. The system gives back a clean yes or no. You can sleep easier when the test passes.

<!--more-->

I've been writing those tests for 27 years. The shape of the question never changed.

That model of testing doesn't work for AI.

The model can produce different outputs for the same input. Both correct. The "expected output" question doesn't have a single answer to compare against.

So you stop testing. You evaluate.

An eval doesn't ask "did X equal Y." It asks something fuzzier: given these inputs, did the outputs satisfy these properties — most of the time? The boolean is replaced by a score. The single check is replaced by a distribution.

For each behavior I care about, I keep a small set of representative inputs — a golden dataset. I run the model against them and score the outputs against criteria. Sometimes by hand against a rubric. Sometimes with another model as judge. Sometimes with programmatic checks — that the output contains the required field, parses as valid JSON, stays within a length limit.

The score is a number, not a verdict. I track it over time.

Last month I bumped the model version on a classification step. The eval score dropped four points on edge cases. The model was "better" overall — higher on the easy inputs — but it hallucinated more on the hard ones. Without the eval I'd have shipped the swap, and the regression would have surfaced in production.

When the score drops, something changed. Three suspects: a new model version, a prompt I edited, or a shift in the input distribution. The diagnosis isn't always obvious; the regression is.

**Tests gave me confidence by being definitive. Evals give me confidence by being statistical.**

That's a colder kind of confidence than I'm used to. The eval saying "92% on the rubric, slightly down from 94% last week" is real information. It just doesn't feel like a green checkmark. It feels like a thermometer.

The unit test answered a yes/no question. The eval tracks a quality question, and the answer keeps moving. The work didn't get easier. It got different.
