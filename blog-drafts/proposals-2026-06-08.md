# Blog Post Proposals — 2026-06-08

Generated from: catalog cross-reference (21 published posts + 5 prior proposals from 2026-06-01) + web research on AI/tech trends through June 2026.

Prior proposals (2026-06-01) already covered: context engineering as architecture, benchmark skepticism, AI code optimism bias, open source cost curve shift, spec writing for AI. All five proposals below are in different territory.

---

## Proposal 1: Not Every Call Needs to Think

**Working title:** Not Every Call Needs to Think

**Thesis:** Reasoning models — chain-of-thought at inference time — are a routing decision, not an upgrade, and knowing when to pay for thinking is a system design skill, not a model selection skill.

**Angle:**
Post 16 ("A Fleet, Not a Default") covered selecting across providers. Post 20 ("An Assistant Is More Than a Model") reframed the assistant ecosystem. Neither addressed inference-mode selection: the choice between a fast, cheap path and a slow, expensive one *within* a model family. Claude Opus 4.8 in extended-thinking mode costs 5–30x more tokens per task than standard mode; for most tasks in a working day, standard mode is correct. A 27-year engineer has made this tradeoff forever — synchronous DB query vs. cached result, batch job vs. real-time — and the mental model transfers directly. What's new is that the routing decision is semantic, not numeric: you're not predicting latency, you're predicting whether the task benefits from deliberate reasoning. The concrete anchor is a simple rule Matias has arrived at: quick synthesis, answering questions, routine code changes — standard mode. Debugging an obscure failure, evaluating a complex architectural tradeoff, catching edge cases in a spec — thinking mode. The heuristic isn't perfect, but the cost of not having one is.

- **Timely:** [Zylos Research — Inference Economics: AI Agent Compute Markets (April 2026)](https://zylos.ai/research/2026-04-13-inference-economics-ai-agent-compute-markets) reports reasoning-mode agents require 5–30x more tokens per task than standard chatbots. At production scale, unconstrained thinking mode converts a manageable monthly bill into an unmanageable one overnight.

---

## Proposal 2: The Docstring Is the Contract

**Working title:** The Docstring Is the Contract

**Thesis:** When you define a tool for an AI agent, the function schema is an interface — but it's written in prose, not types, and that changes everything about how you design it.

**Angle:**
Post 13 ("Text Isn't Text") showed the model sees integer token IDs, not characters — a fundamental inversion of what an engineer expects. There's a parallel inversion when defining MCP tools: you write function schemas, but the model reads your parameter *descriptions*, not your type annotations. The docstring you'd normally dash off as an afterthought is now the primary contract. For a 27-year engineer who's designed hundreds of typed interfaces, this lands like a punch: precision that used to come from types now has to come from prose. The practical consequence is real: `description: "The user's ID"` and `description: "The internal UUID of the authenticated user, not the display name"` produce meaningfully different model behavior — but your linter won't catch the first one. The anchor is a specific failure mode: tool invocations that pass all type checks and fail semantically, because a parameter description was technically correct and practically ambiguous. That's a new class of interface bug.

- **Timely:** [WorkOS — Everything Your Team Needs to Know About MCP in 2026](https://workos.com/blog/everything-your-team-needs-to-know-about-mcp-in-2026) documents MCP as the de facto production standard, now adopted by OpenAI, Google DeepMind, and Microsoft. The interface design question is universal, but the tooling for writing good tool schemas is still catching up.

---

## Proposal 3: Hard Is Easy and Easy Is Hard

**Working title:** Hard Is Easy and Easy Is Hard

**Thesis:** The model's capability profile doesn't scale linearly with task complexity — it's jagged in ways that defeat intuition, and a 27-year engineer trained on "hard problems take more time" keeps getting surprised by where the cliff actually is.

**Angle:**
Post 11 ("Same Prompt, Different Code") covered semantic non-determinism — the same prompt producing different outputs. This is a different and orthogonal problem: the model is *reliably* good at some things you'd expect to be hard, and *reliably* bad at some things you'd expect to be easy. That's the "jagged frontier" — models can refactor a gnarly 500-line function brilliantly and then get a locale-specific date format wrong three times in a row. The insight isn't that models are unreliable. It's that you are the wrong person to predict intuitively where the capability cliff is. Your 27 years of engineering teach you that complex ≈ hard and simple ≈ easy. The model has a completely different difficulty topology, and your intuitions about it are about as accurate as your first guesses about what the tokenizer does. The concrete anchor: mapping tasks Matias has tested against the model and building a working mental model of where it excels and where it quietly fails — not from documentation, but from accumulated experience.

- **Timely:** [arxiv — "A Model of Artificial Jagged Intelligence" (January 2026)](https://arxiv.org/pdf/2601.07573) formalizes this empirically, showing AI systems exhibit performance profiles that don't correspond to human difficulty hierarchies. The paper gives a name to something senior engineers encounter regularly but haven't had vocabulary for.

---

## Proposal 4: The Model Is a Dependency

**Working title:** The Model Is a Dependency

**Thesis:** Upgrading a model version can silently break working behavior — and 27 years of dependency management didn't prepare you for a dependency whose interface is unchanged but whose behavior is defined by a trillion-parameter weight matrix.

**Angle:**
Every other dependency in software has a changelog, semver guarantees, or at minimum a diff you can read. When Claude Opus 4.8 replaced 4.7 or GPT-5.5 replaced GPT-5, the API surface was identical — but the semantic behavior of outputs shifted. Prompts that worked reliably started producing different structures, tones, or reasoning paths. This isn't a bug. It's the nature of a dependency whose "source code" is not inspectable. The practical implication connects directly back to post 18 ("Tests Stopped Being Boolean"): you need an eval suite not just to validate your system at build time, but to detect when a model upgrade silently changes behavior you were relying on. The concrete anchor is a golden-output regression: re-running 20 representative prompts after a model update and finding 3 changed in ways you'd classify as wrong. That's a regression — but not one a type checker, linter, or unit test would catch. Model versioning and the eval suite as a compatibility harness are the same problem.

- **Timely:** [LLM Stats — Latest AI Model Releases, June 2026](https://llm-stats.com/ai-news) documents the accelerating pace of frontier model updates — Claude Opus 4.8, GPT-5.5, Gemini 3.1 Pro all released within a four-month window. Production teams are upgrading frequently and discovering that semantic regressions don't show up in their test suites.

---

## Proposal 5: I Couldn't See What It Was Doing

**Working title:** I Couldn't See What It Was Doing

**Thesis:** Production AI systems are harder to observe than any system a 27-year engineer has built before — because the causal chain between input and wrong output is written in prose, and the tooling to trace it barely exists.

**Angle:**
Post 8 ("What Actually Slows You Down") identified the understanding gap during development: the gap between building speed and comprehension. This post goes to the production layer: once something ships, how do you know what the model is actually doing? Logs give you inputs and outputs, but not the reasoning in between. A 27-year engineer has cared deeply about observability — distributed tracing, structured logging, APM dashboards — but those systems emit structured signals. A model call emits prose. When an agent takes the wrong action, the causal chain is a sequence of natural-language intermediate states. The concrete anchor: debugging a production issue where an agent took the wrong branch — no stack trace, no line number, no event ID. The only trace was the model's output text. Structured logging of prompts, outputs, chain-of-thought, and tool invocations is the bare minimum. Most teams aren't doing it, and the absence doesn't feel like a gap until something goes wrong in production and you realize you have nothing to look at.

- **Timely:** [Qualys TotalAI — "MCP Servers: The New Shadow IT for AI in 2026" (March 2026)](https://blog.qualys.com/product-tech/2026/03/19/mcp-servers-shadow-it-ai-qualys-totalai-2026) documents teams deploying MCP-connected agents without visibility into which tools are being invoked or why. The observability gap at the agent layer is named and growing.

---

## Coverage check

| Proposal | Mode | Nearest existing post | Why it's different |
|---|---|---|---|
| Not Every Call Needs to Think | System design / cost routing | 16 (fleet selection), 20 (assistant ecosystem) | Those cover provider/assistant choice; this covers inference-mode routing within a model |
| The Docstring Is the Contract | Technical deep dive | 13 (tokenization), 19 (agent patterns) | Technical but focuses on interface design in prose — a new class of API bug |
| Hard Is Easy and Easy Is Hard | Counterintuitive insight | 11 (non-determinism) | Non-determinism is about *variability*; jagged frontier is about *capability shape* — orthogonal |
| The Model Is a Dependency | Engineering practice | 18 (evals), 16 (fleet) | Evals for behavioral regression on model upgrades is a specific practice not yet covered |
| I Couldn't See What It Was Doing | Production engineering | 8 (what slows you down), 6 (trust/failure modes) | Development friction vs. production observability are different problems |
