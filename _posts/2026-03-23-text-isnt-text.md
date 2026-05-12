---
layout: post
title: "Text Isn't Text"
date: 2026-03-23
categories: [foundations]
tags: [ai-architecture, tokenization, learning]
image: /assets/images/post-13-hero.png
---

Last week I sat with a tokenizer for an afternoon. Pasted strings, watched them split, tried to predict how each one would break before I pasted it. I was wrong more often than right.

<!--more-->

You've probably seen the strawberry example — count the r's, model gets it wrong. It's a symptom of something simpler. Something I'd never had to think about. The model doesn't see "strawberry" as s-t-r-a-w-b-e-r-r-y. It sees something closer to "straw" + "berry." The letters aren't there as letters. They're inside opaque chunks the model treats as units.

This is byte-pair encoding — BPE. The tokenizer has a fixed vocabulary of around 100,000 entries. Common words are single tokens. Rare words get split into subword pieces. "The" is one token. "Strawberry" might be one or two depending on the tokenizer. A long technical word might be five or six. The splits are learned from training data — frequent combinations get their own token.

That part is mechanical. The conceptual shift was the harder part.

For most of my career, text was a sequence of characters. Code processed strings character by character. Indexing into a string was a constant-time operation over letters. The string was the data.

For the model, the string is an artifact of input encoding. The data is a sequence of integer IDs, somewhere between zero and a hundred thousand. Whatever the model knows about language, it knows in that integer space. **The letters never made it inside.**

Once I saw this, a lot of other things stopped being mysterious:

- The same paragraph in some languages costs noticeably more tokens than in English. Tokenizers are trained on English-heavy data; other scripts often split worse.
- Models do badly on tasks that need letter-level reasoning. Counting characters, anagrams, rhyme detection — the letter is the unit, and the unit isn't there.
- Identifiers tokenize differently depending on style. `userId` is typically one token. `usrId` is three. Same intent, more tokens.

For a 27-year engineer trained to think character by character, this was the part that took longest to internalize. The string isn't the data anymore. The string is an interface.
