# Weekly Post Proposals — 2026-07-27

Five fresh ideas checked against the 21-post catalog and all prior proposal rounds (May 22 through July 20) for originality.

**Trends grounding this round:** Gloss report that 51% of GitHub code is now AI-generated; arXiv "Lore" paper on git history as inter-session knowledge protocol; Kimi K3 2.8T-parameter MoE with 1M context; Grok trained on Cursor usage data (July 8); Block Engineering testing pyramid for AI agents; inference cost decline to $0.006/1K tokens (10x drop year-over-year).

**Cumulative exclusion list (not revisited here):** context engineering (any angle), benchmark leaderboard fracture, culture amplification, inference economics as architecture, open source vibe-slop externality, productivity paradox, reasoning token cost paradox, benchmark saturation/Goodhart's Law, agent concealment failure mode, context window recall degradation, debugging non-determinism, code legibility for model, ownership without mental model, practice churn/expiration, few-shot prompting, system prompt as unversioned artifact, TTFT/streaming latency, production AI observability, embeddings/similarity failure, structured output as type boundary, model reliability in review vs. generation, fine-tuning decision, leaky AI API abstraction, data privacy boundary. **Plus last week's proposals:** MCP/protocol win, spec as machine-readable input, review throughput bottleneck (read gap), tier selection within model families, human-in-the-loop illusion.

---

## 1. "The Commit Message I Can't Write"

**Thesis:** When AI generates the code, the decision provenance disappears — and the next session (yours or the model's) inherits a codebase with no memory of why it looks the way it does.

**Angle:** The catalog has a RAG post-mortem (post 7), a context loss post (post 8), and a spec drift post (post 15) — but none of them address the specific loss of institutional memory encoded in git history. A commit message, at its best, captures WHY: why this approach over the alternatives, what was tried first, what constraint made the obvious solution impossible. When AI generates the code, no human held those decisions consciously long enough to write them down. They live in the session context, which evaporates. Concrete anchor: returning to a PR from three months ago and finding a deliberate-looking architectural choice with no trace of rationale — not in the code, not in the tests, not in the commit. You can't tell if it was considered or accidental. You don't know which parts are load-bearing. The "Lore" paper on arXiv is proposing git commit messages as a structured knowledge protocol precisely because the problem is real and getting worse. The post wouldn't be about tooling — it would be the observation that most teams haven't named this loss yet, and naming it is the first step.

- **Why now:** arXiv paper "Lore: Repurposing Git Commit Messages as a Structured Knowledge Protocol for AI Coding Agents" (March 2026, [arxiv.org/html/2603.15566v1](https://arxiv.org/html/2603.15566v1)) addresses this directly. Combined with Gloss's report that 51% of all GitHub code is now AI-generated ([gloss.run/post/half-of-all-code-on-github-is-now-ai-generated](https://gloss.run/post/half-of-all-code-on-github-is-now-ai-generated)), the institutional memory problem is scaling fast.

---

## 2. "The Model Has Opinions About Your Code"

**Thesis:** The model's training priors are a code style guide you never agreed to, and they'll push through every constraint you set.

**Angle:** Post 15 (one process can't fix) named over-complexification as the failure mode that process can't prevent. This post goes one level deeper and names the mechanism: the model's definition of "good code" is statistical, derived from training data that reflects the average of what ships on GitHub. Intentional local conventions that diverge from that average — deliberate simplicity, domain-specific patterns, principled under-abstraction — read as errors to the model and get silently corrected. The model isn't being difficult; it has strong aesthetic priors and no way to know that your choices were choices. Concrete anchor: asking the model to extend a deliberately minimal service — three functions, no config layer, no interface abstraction — and watching it add error handling, dependency injection wiring, and a factory method you explicitly decided not to include. The post would distinguish between the model being wrong (a bug) and the model being right by its priors while wrong in your context (a structural problem). The second kind doesn't get caught by review unless you know to look for it.

- **Why now:** Grok's new agentic flagship (released July 8, 2026) was trained jointly with Cursor on trillions of tokens of real Cursor usage data — the first coding model explicitly trained on how people *use* AI to code, not just what code looks like. That makes the priors question sharper: what did millions of AI-assisted developers bake into this model's sense of "normal"?

---

## 3. "How Deep Is Deep Enough"

**Thesis:** "Going deep on AI" is the right instinct — but the honest question is where the practical floor is, the point where understanding actually changes what you build.

**Angle:** The blog's entire arc is "going deep on AI." Post 4 (why I'm going deep) covers the motivation. Post 1 covers early surprises. Post 13 (text isn't text) is the first technical deep dive into tokenization. None of them answer the calibration question: how far down should you go, and how do you know when you've gone far enough? Some layers change everything in practice — tokenization changed how prompts get written. Some are intellectually satisfying but haven't touched a production decision — transformer internals, attention head math, MoE routing. The post would be honest about the difference, not as a license to stay shallow, but as a way of being deliberate: knowing why you're going deeper and what will change when you get there. Concrete anchor: reading about sparse MoE routing in Kimi K3 (2.8T parameters, 32B active per forward pass), finding it fascinating, and then asking: has anything I've learned at this level changed a system design decision? If yes, keep going. If not yet, that's worth naming.

- **Why now:** Kimi K3's 2.8T-parameter MoE architecture with a 1M-token context window ([simonwillison.net/2026/Jul/16/kimi-k3/](https://simonwillison.net/2026/Jul/16/kimi-k3/)) is the kind of system that makes "going deep" feel both urgent and overwhelming. The frontier keeps moving. The floor question is the only honest response to that.

---

## 4. "The Test Pyramid Is Upside Down"

**Thesis:** The classic test pyramid breaks when the core component is non-deterministic — and working out what to put where is a harder problem than any tutorial will admit.

**Angle:** Post 18 (tests stopped being boolean) covered the conceptual shift from pass/fail to distribution-based confidence. This post is the architectural follow-on: where do the different test types go in a stack that has AI components? Unit tests still work for deterministic logic around the model — retry behavior, tool schema validation, guardrails. Evals cover model output quality. Integration tests catch composition failures that neither layer can see. The "right" ratio inverts the classic pyramid: the cheap, fast unit tests can't reach the component that matters most, so you end up front-loading integration and eval coverage — which is expensive and slow. Concrete anchor: trying to practice TDD on an AI-mediated workflow and hitting the wall where "write the test first to define expected behavior" can't define the behavior of a component that will give you a distribution of outputs on every call. You end up testing everything around the model and nothing through it — and calling that a test suite.

- **Why now:** Block Engineering published "Testing Pyramid for AI Agents" ([engineering.block.xyz/blog/testing-pyramid-for-ai-agents](https://engineering.block.xyz/blog/testing-pyramid-for-ai-agents)) showing the explicit three-layer rethink in production. Industry is converging on "flatter" or inverted pyramid models for AI-inclusive stacks in 2026, but the guidance for practitioners is sparse.

---

## 5. "The Rewrite Is Cheap. The Risk Isn't."

**Thesis:** AI made the implementation cost of a rewrite nearly zero — which removes the friction that used to force you to think it through.

**Angle:** Post 21 (building got cheap, owning didn't) covered scope expansion and ownership cost when building is cheap. This is a different claim about a different decision: the rewrite vs. extend choice, which was historically gated by implementation cost. Before AI, rewriting was expensive enough to require justification — that requirement filtered out bad reasons (boredom, aesthetics, framework churn). When the cost drops to a weekend, the filter disappears. You start rewrites for reasons that wouldn't have survived a budget conversation. And you discover mid-project that the constraints shaping the original code were real — the legacy decisions you were going to clean up turn out to be encoding domain knowledge you didn't know you had. Concrete anchor: starting a rewrite that was going to be "cleaner," moving fast for the first few weeks, and then finding that every shortcut in the original was actually a load-bearing decision — not bad code, but code whose rationale had to be re-derived from the domain, not the diff. The post wouldn't argue against rewrites. It would argue for knowing that the cost gate was doing real work, and that removing it means replacing it with something deliberate.

- **Why now:** AI inference costs have dropped ~10x year-over-year to roughly $0.006 per 1K tokens ([sesamedisk.com/ai-inference-cost-trends-2026](https://sesamedisk.com/ai-inference-cost-trends-2026/)), and code generation volume is scaling with it. The conditions for impulsive rewrites are at an all-time high; the framework for thinking about when they're warranted hasn't kept up.

---

*Generated 2026-07-27. All five checked against the 21-post catalog and all prior proposal rounds (May 22 through July 20).*

*Catalog modes already covered: reflection, engineering wisdom, post-mortem, tokenization deep dive, contrarian deliberate skipping, failure analysis, model selection fleet, book-anchored, evals, agents as pattern, cost/ownership, non-determinism, SDLC compression, junior-senior path, trust/failure modes, vibe-to-spec, why going deep, assistant vs model, RAG pipeline architecture, understanding gap.*

*Prior proposal angles excluded (cumulative): context engineering, benchmark leaderboard fracture, culture amplification, inference economics as architecture, open source externality, productivity paradox, reasoning token cost, benchmark saturation, agent concealment, context recall degradation, debugging non-determinism, code legibility for model, ownership without mental model, practice churn, few-shot prompting, system prompt as unversioned artifact, TTFT latency, production AI observability, embeddings/similarity, structured output as type boundary, model review vs generation reliability, fine-tuning decision, leaky AI API abstraction, data privacy boundary, MCP/protocol win, spec as machine-readable input, review throughput bottleneck, tier selection within model families, human-in-the-loop illusion.*
