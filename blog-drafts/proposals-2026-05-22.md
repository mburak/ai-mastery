# Blog Post Proposals — 2026-05-22

Generated for: mburak/ai-mastery  
Today's date: 2026-05-22  
Catalog cross-checked: 20 published posts (through `2026-05-11-an-assistant-is-more-than-a-model.md`)

---

## Originality check: modes already covered

Before proposing, here's a quick map of what the catalog has touched heavily:

- Reflection / retrospective — posts 4, 9, 23
- Engineering wisdom via analogy — posts 2, 5, 10, 12, 15
- Post-mortem — post 7
- Technical deep dive — post 13 (tokenization)
- Contrarian / "I don't always use AI" — post 14
- Failure analysis — posts 7, 15
- Model/assistant selection — posts 16, 20
- Book-anchored — post 17
- Evals (internal, statistical confidence) — post 18
- Agent architecture pattern recognition — post 19
- Non-determinism in a single session — post 11
- Context loss in the developer — post 8
- Trust framing — post 6
- SDLC cycle patterns — post 10
- Junior-to-senior learning path — post 12

The five proposals below deliberately avoid all of these modes.

---

## Proposal 1: "The Prompt Was Never the Problem"

**One-sentence thesis:** The term "prompt engineering" put the focus in the wrong place — the real work has always been what surrounds the prompt, and the discipline of engineering that context is older than LLMs.

**The angle:**  
"Context engineering" got named and formalized in 2025–2026 (Karpathy coined it, Anthropic published a pattern guide for agents). But for any engineer who has designed SQL queries with good joins, built cache invalidation logic, or curated inputs to a rules engine, the instinct is completely familiar: what you put in front of the function matters more than the function signature. The vocabulary is new. The problem isn't.

This is distinct from post 13 ("Text Isn't Text"), which was about tokenization — what the model sees at the character level. This post is about the layer above that: what information you choose to include, exclude, compress, or retrieve before the model ever sees a token. It's also distinct from post 8 ("What Actually Slows You Down"), which was about the human's understanding gap. This is about the model's input architecture.

The concrete anchor: a real scenario where the prompt was fine and the context was broken — e.g., the unfinished RAG pipeline from post 7 (which never built the retrieval layer) was a context engineering failure masquerading as a pipeline problem.

**Why timely:**  
Context engineering is the dominant engineering conversation of mid-2026. Andrej Karpathy's framing went viral in mid-2025, Anthropic published a formal pattern guide in 2026, and the LogRocket post from this month describes teams now treating context as "instrumented, tested, versioned, and continuously optimized." The term is still new enough that naming it clearly in the author's voice adds real signal.  
Source: https://blog.logrocket.com/llm-context-problem/ | https://blog.american-technology.net/context-engineering/

---

## Proposal 2: "The Leaderboard Stopped Mattering"

**One-sentence thesis:** The AI benchmark numbers you see published in May 2026 are nearly useless for deciding which model to use — not because the models are bad, but because the tests saturated and the companies train to the tests.

**The angle:**  
SWE-bench Verified was retired in February 2026 after OpenAI discovered that at least 59.4% of remaining tasks were flawed, unsolvable, or contaminated — the models could reproduce the gold patches verbatim from memory. The leaderboard for remaining benchmarks now clusters frontier models within tenths of a percentage point (Claude Opus 4.7 at ~80.9%, Gemini 3.1 Pro at 80.6%, GPT-5.2 at 80.0%). The numbers look precise and mean almost nothing for your specific task.

This is distinct from post 18 ("Tests Stopped Being Boolean"), which was about internal evals replacing unit tests for your own products. This post is about the external benchmark ecosystem — the published scores companies use for marketing — and what a working engineer should do when those numbers can't be trusted. The answer is the same thing senior engineers have always done when a metric gets gamed: stop optimizing for the metric and go back to the actual problem.

Concrete anchor: the benchmark saturation story as a direct parallel to Goodhart's Law — any measure that becomes a target ceases to be a good measure. A 27-year engineer has seen this before (code coverage %, velocity points, bug counts). The new version just happens to involve matrix multiplications.

**Why timely:**  
SWE-bench Verified retired February 2026, contamination discovered via GPT-5 probing. SWE-bench Pro emerged as a replacement, itself already contested. Kili Technology's 2026 benchmark guide explicitly calls the evaluation system "not enough." This is the peak of the credibility crisis.  
Source: https://www.adwaitx.com/openai-swe-bench-verified-retired-ai-benchmarks/ | https://kili-technology.com/blog/ai-benchmarks-guide-the-top-evaluations-in-2026-and-why-theyre-not-enough

---

## Proposal 3: "Models Don't Have Changelogs"

**One-sentence thesis:** When Anthropic quietly updates a model, your product's behavior can change without a deployment — and all the tooling engineers built for dependency management wasn't designed for this.

**The angle:**  
In traditional software, you pin a dependency version, you read the CHANGELOG, you write tests before upgrading. Model providers update named versions silently. "claude-opus-4-7" today is not the same model it was three months ago. There's no semantic versioning, no deprecation notice, no diff to review. Your evals fail weeks later and you're debugging a ghost.

This is meaningfully different from post 11 ("Same Prompt, Different Code"), which covers non-determinism *within* a session — the same prompt giving different outputs on the same model. This post is about non-determinism *over time* — the model itself changing underneath you. Two different engineering problems that happen to look similar on the surface.

Concrete anchor: the n8n production case from February 2026 (v2.4.7 → v2.6.3 upgrade broke JSON schema generation silently) as a real example of the class of failure. Not a model update specifically, but same pattern: third-party system changed behavior with no changelog. The AI version is structurally identical but harder to detect.

**Why timely:**  
AscentCore published "Why Your AI Agents Are One Update Away from Breaking" in May 2026 specifically calling this out. The rapid release cadence (five major closed releases since February alone, per the May 2026 model landscape summary) makes this failure mode increasingly common.  
Source: https://ascentcore.com/2026/05/04/why-your-ai-agents-are-one-update-away-from-breaking/ | https://whatllm.org/blog/new-ai-models-may-2026

---

## Proposal 4: "More Context, Same Confusion"

**One-sentence thesis:** Ten-million-token context windows feel like they finally solved the memory problem — they didn't, they just moved the failure mode from "can't fit it" to "can't focus on it."

**The angle:**  
Llama 4 shipped a 10M-token context window. MiniMax-M1-80k has 1M native tokens. The message from the model providers is: give it everything, the window is now infinite. The engineering reality is different. Models with long contexts lose coherence over distance — the "lost in the middle" problem. The constraint moved from *fitting* information in to *keeping the model focused* on the right part of what's in there.

This connects back to post 7 (the unfinished RAG pipeline) but goes in a different direction. Post 7 was about building a retrieval system that never got built. This post would be about what happens when you think long context makes retrieval unnecessary — and discover the model still loses the thread. The insight is that bigger windows changed the surface area of the failure, not the presence of failure.

Good engineering framing: the constraint didn't disappear, it migrated. This is a familiar pattern from hardware optimization — you speed up the CPU, the bottleneck moves to memory bandwidth. You increase memory, it moves to cache misses. Context windows scaled, the bottleneck moved to attention degradation over distance.

**Why timely:**  
The Llama 4 10M-token window launched in Q1 2026 and immediately generated debate about whether long context was "good enough" to replace RAG. The LogRocket "LLM context problem" piece from 2026 explicitly addresses this: "The context problem in 2026 is not primarily about model capability; the real challenge is information discipline."  
Source: https://blog.logrocket.com/llm-context-problem/ | https://aimultiple.com/ai-context-window

---

## Proposal 5: "Thinking Costs Something"

**One-sentence thesis:** Reasoning models are genuinely more accurate, but "slower and more accurate" hides the real tradeoff: the failure mode shifts from "wrong answer" to "confidently explained wrong answer," which is harder to catch.

**The angle:**  
Extended thinking, chain of thought, reasoning budgets — these are now a category with 20+ options across OpenAI, Anthropic, Google, DeepSeek, and others. The narrative is that thinking longer = thinking better. For hard reasoning tasks, that's often true. But the failure mode that emerges is subtler than a standard model's: a reasoning model can produce a detailed, coherent, internally consistent argument that is completely wrong. The scaffolding of reasoning makes the error look authoritative.

This is a new engineering decision that has no prior analog: when do you pay the latency and compute cost of extended thinking, and when does that cost make things worse rather than better? The frame is resource allocation — like deciding between a synchronous blocking call and a queue-based async flow. Sometimes you need the blocking call. Sometimes you just added latency to a request that didn't need it, and now the user is waiting for a confident wrong answer instead of a quick wrong answer.

Concrete technical anchor: Gemini 3.1 Pro at 94.3% on GPQA Diamond (hard science reasoning) — this is where extended thinking is genuinely earning its keep. Contrast with coding tasks where Claude Opus 4.7 leads without necessarily reasoning aloud. The gap tells you something about when thinking helps.

**Why timely:**  
The reasoning model category exploded in early-mid 2026. DeepFounder's May 2026 guide covers 20+ reasoning model options and notes the category has "saturated" with providers all claiming extended thinking. The question of *when* to use reasoning (vs. standard) is the current practical engineering question that nobody is answering well.  
Source: https://deepfounder.ai/ai-reasoning-models-2026-o3-gemini-deepseek-claude/ | https://sureprompts.com/blog/ai-reasoning-models-prompting-complete-guide-2026

---

## Summary table

| # | Working Title | Core Mode | Timeliness Anchor |
|---|---|---|---|
| 1 | The Prompt Was Never the Problem | New discipline / vocabulary correction | Context engineering formalized by Karpathy + Anthropic, 2025–2026 |
| 2 | The Leaderboard Stopped Mattering | Contrarian / Goodhart's Law applied | SWE-bench Verified retired Feb 2026 after contamination |
| 3 | Models Don't Have Changelogs | Engineering failure mode / dependency | Silent model updates + May 2026 rapid release cadence |
| 4 | More Context, Same Confusion | Technical misconception correction | 10M-token windows shipped; "lost in the middle" persists |
| 5 | Thinking Costs Something | New resource allocation decision | 20+ reasoning models in 2026; category exploded |

None of these repeat an existing post's primary mode. All five are grounded in specific technical anchors or real engineering failure cases. All five are in scope for the "experienced engineer going deep on AI" arc.
