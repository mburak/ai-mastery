# Blog Post Proposals — 2026-06-01

Generated from: catalog cross-reference (21 published posts) + web research on AI/tech trends through June 2026.

---

## Proposal 1: Context Is Engineering Now

**Working title:** Context Is Engineering Now

**Thesis:** Managing what goes into the context window is a first-class engineering discipline — not a configuration detail — and most engineers are still treating it like plumbing.

**Angle:**
Post 7 ("The Pipeline I Built and Never Finished") covered RAG as a failed ingestion project. That post was about the pipeline; this one is about the window itself. The distinction matters: RAG is one tool for managing context. The broader shift is that the context window is now a resource you architect — you decide what goes in, in what order, at what granularity, and what gets evicted. That's not retrieval engineering. That's memory management, but for a system that can't swap to disk. The concrete anchor is the difference between dumping a file into context ("just put it all in") vs. treating context as a budget where every token competes for space. After 27 years of caring deeply about memory layout, Matias finally has something that works like RAM again — except the cost of a cache miss is a wrong answer, not a page fault.

- **Timely:** LogRocket (June 2026) published ["The LLM context problem in 2026: strategies for memory, relevance, and scale"](https://blog.logrocket.com/llm-context-problem/) calling context engineering "a first-class discipline"; a Medium post from the same period titled ["The context window is the new RAM"](https://lyricalstring.medium.com/the-context-window-is-the-new-ram-engineering-for-the-llm-era-3f5a698fc257) surfaced independently. Both signal the field is naming this pattern now.

---

## Proposal 2: The Benchmark Is Not the Grade

**Working title:** The Benchmark Is Not the Grade

**Thesis:** SWE-bench 88% tells you something real about a model — just not anything about whether it will work on your codebase.

**Angle:**
Post 18 ("Tests Stopped Being Boolean") covered evals as a replacement for unit tests — testing your system's outputs. This is the mirror image: benchmarks test the model. They're not the same thing, and the difference matters more than ever right now. May 2026 has been a benchmark arms race: Claude Opus 4.8 at 88.6% SWE-bench Verified, GDPval Elo, Terminal-Bench 2.1, all dropping within days of each other. For an engineer picking a model, this noise is seductive and mostly useless. The concrete anchor: SWE-bench uses GitHub issues from public repos with clean test suites. It does not measure what happens when your repo has 12 years of accumulated tech debt, inconsistent naming conventions, and no tests. The post reframes: benchmarks are baselines, not grades. What actually predicts performance on your codebase is a small eval suite you build yourself — which connects back to post 18 without repeating it.

- **Timely:** [LM Council benchmarks (May 2026)](https://lmcouncil.ai/benchmarks) and [o-mega's model benchmark roundup](https://o-mega.ai/articles/ai-model-benchmarks-pricing-may-2026) both reflect the current benchmark churn. The specific framing of "benchmarks vs. your codebase" is missing from the discourse.

---

## Proposal 3: AI Code Is Optimistic

**Working title:** AI Code Is Optimistic

**Thesis:** AI-generated code is systematically biased toward the happy path — and 27 years of engineering training to think about what breaks means Matias notices this every time.

**Angle:**
Post 6 ("It's Not About Trust") established that knowing failure modes beats trusting the model. Post 15 ("The One Process Can't Fix") covered over-complexification as an AI prior. This post goes narrower and more concrete: AI-generated code handles the success case cleanly and under-handles the failure case almost every time. It's not hallucination. It's an optimism bias baked into training data, which skews toward working examples. The concrete anchor is a real pattern Matias has seen repeatedly — functions that return a result but don't handle the case where the external call times out, the file doesn't exist, or the user sends unexpected input. A 27-year engineer's first instinct is "what breaks this?" The model's instinct is "here's how this works when it works." That gap is real, reproducible, and has production consequences.

- **Timely:** Microsoft researchers published findings (May 2026) that [even frontier models introduce errors in long-running multi-step agent workflows](https://www.theregister.com/ai-ml/2026/05/11/microsoft-researchers-find-ai-models-and-agents-cant-handle-long-running-tasks/5238263); OWASP's 2026 agentic taxonomy separately documented that [AI-generated code handles the happy path but rarely models failure modes](https://www.trantorinc.com/blog/ai-agent-failure-modes-what-goes-wrong-design-resilience). Two independent sources naming the same pattern in the same month.

---

## Proposal 4: Open Source Changed the Math

**Working title:** Open Source Changed the Math

**Thesis:** Four Chinese open-weights models hit frontier coding capability in a 12-day window in May 2026 — and the cost curve for running capable models just broke in a way that changes every architectural assumption you made 18 months ago.

**Angle:**
Post 16 ("A Fleet, Not a Default") covered selecting from providers and models strategically. That post was about the decision; this one is about a structural shift underneath the decision. In May 2026, GLM-5.1, MiniMax M2.7, Kimi K2.6, and DeepSeek V4 all landed at roughly the same capability ceiling as the Western frontier on agentic engineering tasks — at meaningfully lower inference cost. The question this raises for Matias is not "should I use them?" (he already has DeepSeek for classification, Qwen for OCR per the fleet post). The question is: what does a fleet look like when the frontier is reachable at sub-dollar pricing per million tokens? The concrete tension: cost used to be a strong signal for capability. That signal is degrading. The post can be honest about uncertainty — he doesn't know yet what this changes — but can anchor on one real thing: the assumption that "capable = expensive" is no longer reliable, and that's a different kind of engineering constraint than he's ever worked with.

- **Timely:** Air Street Press ["State of AI: May 2026"](https://press.airstreet.com/p/state-of-ai-may-2026) and [CoderSera's May 2026 model roundup](https://codersera.com/blog/ai-models-released-may-2026-monthly-roundup/) both document the Chinese open-weights surge with specific capability numbers. This is a verifiable structural shift, not hype.

---

## Proposal 5: The Spec Is Not the Requirements Doc

**Working title:** The Spec Is Not the Requirements Doc

**Thesis:** Writing specs for AI is a different skill from writing specs for engineers — because engineers fill gaps and models don't — and nobody is talking about that difference explicitly.

**Angle:**
Post 3 ("I Didn't Go Back to Coding") mentioned the shift to spec-driven development. Post 10 ("The SDLC Didn't Go Away") placed specs in the broader SDLC context. Neither made spec writing itself the subject. The concrete insight: when you write a requirements doc for a human engineering team, you write for someone who will read context, notice ambiguities, ask questions, and apply judgment. When you write a spec for an AI coding agent, you're writing for a system that executes literally and fills ambiguities with its trained priors — which may not match yours. That's a fundamentally different writing task. A good spec for a human has enough direction to align intent. A good spec for an AI has enough constraint to prevent unwanted interpretation. The practical anchor: Matias has learned to write specs that close the gaps he doesn't care about rather than leaving them open for the model to fill "sensibly." That's a new skill. It's not hard, but it's learned.

- **Timely:** Addy Osmani published ["My LLM coding workflow going into 2026"](https://addyosmani.com/blog/ai-coding-workflow/) detailing structured phases (elaborate → plan → implement → assert → review). The "elaborate" phase — where the model is prompted to challenge ambiguities — is essentially an acknowledgment that specs need closing before implementation. The discourse is circling this insight without naming it directly.

---

## Coverage check (modes already used)

| Mode | Posts |
|---|---|
| Reflection / retrospective | 9, 23 |
| Engineering wisdom / management transfer | 3, 5, 10, 12, 15 |
| Post-mortem | 7, 8 |
| Technical deep dive | 13 (tokenization) |
| Contrarian | 14 |
| Failure analysis / process | 15 |
| Model / assistant selection | 16, 20 |
| Book-anchored | 17 |
| Evals / testing | 18 |
| Agents (pattern recognition) | 19 |
| Fleet / cost | 16, 21 |
| Non-determinism | 11 |

All five proposals above are in different territory from all prior modes.
