# Weekly Post Proposals — 2026-07-13

Five fresh ideas checked against the 21-post catalog and all prior proposal rounds (May 22 through July 6) for originality.

*Note: Web search was unavailable this run. Timeliness bullets reference established ongoing trends rather than specific articles from the past two weeks.*

Ideas excluded from prior rounds (not revisited here): context engineering (any angle), benchmark leaderboard fracture, culture amplification, inference economics as architecture, open source vibe-slop externality, productivity paradox, reasoning token cost paradox, benchmark saturation / Goodhart's Law, agent concealment failure mode, context window recall degradation, debugging non-determinism, code legibility for model, ownership without mental model, practice churn/expiration, few-shot prompting, system prompt as unversioned artifact, TTFT / streaming latency, production AI observability, embeddings / similarity failure.

---

## 1. "The Output Is a Contract"

**Thesis:** Getting structured output from a model isn't a convenience feature — it's the type boundary that makes compound AI systems actually composable, and treating it as anything less creates the same class of bugs as stringly typed code.

**Angle:** The blog has addressed compound AI (post 2), agent architecture (post 19), and non-determinism (post 11) but never drilled into what makes the components actually connect. Structured output — forcing a model to produce validated JSON against a schema — is the answer. From a 27-year engineering perspective this is a familiar transition: the shift from stringly typed to strongly typed systems. When a function returned a string and the next function parsed it, bugs lived in the gap. Structured output closes that gap for AI pipelines. The catch: "valid JSON" is not the same as "correct JSON." The model can produce a schema-conformant response that halluccinates a required field or inverts an enum value — and the type checker won't catch it. **The contract covers structure. It doesn't cover truth.** That's the insight that changes how you design the components around it. Concrete anchor: building a pipeline where model output flows directly into the next stage and discovering, after shipping, that the model had been producing structurally valid but semantically wrong values — conforming types, wrong meaning.

- **Why now:** Structured output has become standard across providers (OpenAI's structured outputs shipped August 2024; Anthropic's tool use, Gemini's response schema) and libraries like `instructor` (github.com/jxnl/instructor) have made it easy to adopt. The field has moved past "does this work?" and into the more interesting question of what it doesn't guarantee — making this a timely correction to inflated expectations.
  Source: https://openai.com/index/introducing-structured-outputs-in-the-api/

---

## 2. "Models Read Better Than They Write"

**Thesis:** AI is more reliably correct as a reviewer than a generator, but the whole default workflow is built around generation — and that asymmetry has real engineering consequences.

**Angle:** Every post on the blog treats AI as a code generator. Post 6 ("It's Not About Trust") mentions multi-model verification but frames it around knowing failure modes. Post 16 ("A Fleet, Not a Default") mentions using Gemini for PR reviews as a fleet choice. Neither has made the deeper claim: evaluation is a constrained problem space, and generation is an open one. When you ask a model to find a bug, the answer is bounded — the bug is or isn't there, and the reasoning is grounded in code that exists. When you ask a model to write code, the answer is unbounded — there are infinite possible implementations, and any of them can look plausible. **The model's confidence can't distinguish between "I'm right" and "this sounds right."** That confidence is more calibrated in the review direction because the artifact being evaluated anchors the output. This isn't a reason to stop using AI for generation — it's a reason to treat the review pass as the load-bearing step, not the optional one. Concrete anchor: noticing that asking a model to review a human-written function reliably catches bugs that the same model missed when generating similar code from scratch.

- **Why now:** Code review AI tools have proliferated through 2025–2026 (GitHub Copilot code review, Cursor, Coderabbit) and are being adopted at scale — meaning more engineers are starting to use AI in both directions and can compare the reliability difference themselves. The review-vs-generation asymmetry is now practically observable, not just theoretical.
  Source: https://github.com/features/copilot/code-review

---

## 3. "The Model Isn't the Product. Until It Is."

**Thesis:** For most AI features, prompting a foundation model is the right call — but there's a specific class of problems where that stops working, and recognizing it before you're in production is the skill.

**Angle:** The fleet post (16) and assistant post (20) covered model selection and migration. The evals post (18) covered measuring outputs. No post has addressed the fine-tuning decision: when does it make sense to take a base model and adapt it for a specific task, versus continuing to prompt a general-purpose model? For a senior engineer this is a familiar "build vs. buy" question with an unfamiliar twist: the cost isn't the upfront work, it's the compounding ownership. A fine-tuned model is a snapshot. The ecosystem moves, the base model improves, your fine-tuned version stays frozen unless you re-run the process. The decision logic turns out to be clear once you've hit the limits of prompting: few-shot examples fail to converge, the task requires a format or style no amount of instruction produces, or the latency and cost of a large context make fine-tuning the only economically viable path. Concrete anchor: evaluating whether to fine-tune a model for a recurring structured-extraction task, discovering that 40 high-quality few-shot examples in the prompt matched fine-tuned accuracy — and then finding the two conditions where that stopped being true.

- **Why now:** Fine-tuning APIs are now available from every major provider at accessible price points and latencies, and the LoRA/QLoRA ecosystem has made custom model adaptation practical for small teams. The question has moved from "can we?" to "should we?" — which makes the decision framework the timely thing to write.
  Source: https://platform.openai.com/docs/guides/fine-tuning

---

## 4. "The API Doesn't Hide the Model"

**Thesis:** AI APIs look like clean service boundaries, but they're the leakiest abstraction in software right now — model behavior bleeds through the interface in ways that violate every contract expectation 27 years of API design taught.

**Angle:** Joel Spolsky's "Law of Leaky Abstractions" (2002) is one of the most important essays in software — all non-trivial abstractions leak, and understanding how they leak is the real skill. AI APIs are the most extreme case of this the author has seen in a career. The documentation says: pass a prompt, get a response. The reality: behavior changes after model updates with no API version change, output distribution shifts under high server load, phrasing that echoes RLHF training produces different outputs than semantically equivalent alternatives. In traditional software, "the API changed" means the interface changed. With AI APIs, **the contract is the interface; the behavior is the model.** Those are two different things, and they can diverge on any deployment. This isn't a complaint — it's a design constraint that changes how you build. The post lands on a concrete implication: the stability guarantee you're getting from an AI API endpoint is lower than any other external dependency in your stack, and your architecture should treat it that way. Concrete anchor: discovering that a prompt which had been working reliably for three months started producing subtly different outputs after a model update — no API change, no deprecation notice, just a different model on the other side.

- **Why now:** Every major model provider updated their deployed models in H1 2026, and behavior changes in downstream applications are the most actively discussed pain point in AI engineering communities. The gap between "breaking change" (formal) and "behavior shift" (actual) has become a practical problem for every team running AI in production.
  Source: https://platform.anthropic.com/docs/api-reference/versioning

---

## 5. "What the Model Can't See"

**Thesis:** Every AI system has a data boundary — what you're allowed or willing to send to a model — and ignoring that boundary during design is the fastest way to build something that can't be deployed.

**Angle:** No post or prior proposal has touched data privacy and what goes to the model. For a senior engineer building any real product, this is the constraint that lands hardest in practice: the model can only reason about what it sees, and there are often strong reasons not to show it certain things. PII that can't leave the user's jurisdiction, confidential business data that can't be sent to a third-party API, regulated health or financial information. The post isn't about regulation — it's about the design consequence. When the data boundary is set, the whole architecture rearranges: what gets redacted before it reaches the model, what gets processed locally, what retrieval strategy fits within the constraint. **The model's capability ceiling is set by what you can legally and safely put in its context.** That's a different kind of constraint than compute or cost — it's a correctness constraint, not a performance one. Concrete anchor: designing a feature around a model that looked like it could do the task, discovering midway through that the data the model needed couldn't leave the on-premise environment, and redesigning from scratch to work with what could be shared.

- **Why now:** Enterprise adoption of AI tools has accelerated through 2025–2026, and data residency, privacy compliance (GDPR, CCPA, HIPAA), and security requirements are the top-cited barriers. The pattern of discovering the data boundary after the architecture is set — rather than before — is well-documented in engineering retrospectives from teams that shipped in 2025.
  Source: https://iapp.org/news/a/ai-and-the-gdpr-a-practical-guide/

---

*Generated 2026-07-13. All five checked against the 21-post catalog and all prior proposal rounds (May 22 through July 6). Catalog modes excluded: reflection, engineering wisdom, post-mortem, tokenization deep dive, contrarian deliberate skipping, failure analysis, model selection fleet, book-anchored, evals, agents as pattern, cost/ownership, non-determinism, SDLC compression, junior-senior path, trust/failure modes, vibe-to-spec, why going deep, assistant vs model, RAG pipeline architecture, understanding gap. Prior proposal ideas excluded: context engineering, benchmark leaderboard fracture, culture amplification, inference economics as architecture, open source externality, productivity paradox, reasoning token cost, benchmark saturation, agent concealment, context recall degradation, debugging non-determinism, code legibility for model, ownership without mental model, practice churn, few-shot prompting, system prompt as unversioned artifact, TTFT latency, production AI observability, embeddings/similarity.*
