# Blog Post Proposals — 2026-05-25

Generated for: mburak/ai-mastery  
Catalog checked: 21 published posts (#1–#21)  
Trend window: May 2026

---

## Framing notes

The catalog already covers these modes heavily — proposals below avoid them:
- Reflection/retrospective (posts #4, #9)
- Management-to-AI wisdom transfer (posts #2, #5)
- Post-mortem (post #7)
- Tokenization / technical deep dive (post #13)
- Contrarian "I skip AI for X" (post #14)
- Failure analysis / structured workflow limits (posts #8, #15)
- Fleet and model selection (posts #16, #20)
- Book-anchored vocabulary moment (post #17)
- Evals and non-boolean testing (post #18)
- Agents as orchestration shape (post #19)
- Build cost / ownership cost (post #21)

---

## Proposal 1 — "Context Is Not a Prompt"

**Thesis:** What's being called "context engineering" in 2026 is something good engineers have been doing by instinct all along — deliberately managing what the model *knows*, not just how you talk to it — and CLAUDE.md is a better example of that discipline than any clever prompt template.

**Angle:**
The "context engineering vs. prompt engineering" debate finally has a name and a Gartner declaration behind it. But the author has been doing this since day one: voice rules, a numbered post catalog, confidentiality constraints, background on Matias as a person — none of that is a prompt, it's curated context. This post names the practice, connects it to something the author already built (CLAUDE.md), and explains the architectural distinction: a prompt is an instruction; context is the managed state of what the model is allowed to know.

This is distinct from post #17 ("I Already Knew This," Chip Huyen) — that post was about vocabulary for AI engineering taxonomies from a book. This is about a specific operational discipline that the author is already practicing. It's also distinct from post #7 (the RAG pipeline) which was about data ingestion. Context engineering spans retrieval, session state, and persistent memory — the whole pipeline, not just one stage.

Concrete anchor: compare what Claude's output looks like with CLAUDE.md versus a cold session. The author has real experience of this. The discipline of writing a good CLAUDE.md *is* context engineering — he just didn't have a name for it.

**What makes it timely:**
"Context engineering" became a dominant search and publication topic in May 2026. Taskade, Memgraph, Firecrawl, and SuperMemory all published definitive guides in the last two weeks. Phil Schmid at Google DeepMind defined it as "the discipline of designing and building dynamic systems that provide the right information and tools, in the right format, at the right time." Gartner declared 2026 "The Year of Context."
- Source: https://www.taskade.com/blog/context-engineering
- Source: https://memgraph.com/blog/prompt-engineering-vs-context-engineering

---

## Proposal 2 — "SQL Injection Taught Me This Once"

**Thesis:** Prompt injection is structurally identical to SQL injection — untrusted external content treated as trusted instructions — and developers are making the same category error they made in 1998, in a system that has a lot more access than a database.

**Angle:**
Every engineer of Matias's vintage solved SQL injection. The fix was conceptually simple: treat user input as data, never as commands. Use parameterized queries. Parameterize the boundary. Prompt injection is the same category of error: the model receives untrusted content (a vendor invoice, a GitHub PR description, an email thread) and cannot reliably distinguish "analyze this" from "do this." The attack arrives through legitimate content, not a malicious user prompt.

What makes this worse than classic injection: the vulnerable path is indirect. Over 80% of documented attacks in enterprise AI systems in 2026 are indirect — embedded in documents, emails, web pages, database content the agent processes. The author has built agents (post #19) and trusts his multi-model review workflow (post #6) — but neither of those posts touched the security surface that opens up the moment an agent can read external content.

Concrete anchor: CVE-2025-53773, where a malicious PR description triggered remote code execution via GitHub Copilot (CVSS 9.6). The author uses Claude Code for code review. This is directly in his toolchain.

Framing matters here: this isn't alarmist. The author knows we solved SQL injection. The point is the same clarity is needed here, and the same pattern — recognizing the category error first — is how you get there.

**What makes it timely:**
Microsoft Security Blog published "When prompts become shells: RCE vulnerabilities in AI agent frameworks" on May 7, 2026. OWASP still ranks prompt injection as LLM01 (the #1 LLM vulnerability). Prompt injection attacks have surged 340% in 2026. Security is completely absent from the current catalog.
- Source: https://www.microsoft.com/en-us/security/blog/2026/05/07/prompts-become-shells-rce-vulnerabilities-ai-agent-frameworks/
- Source: https://markaicode.com/prompt-injection-attacks-ai-security-2026/

---

## Proposal 3 — "The Leaderboard Is For Someone Else"

**Thesis:** AI benchmarks are the résumés of models — they measure something real, but not the thing you're actually hiring them for.

**Angle:**
Matias has read thousands of résumés over 14 years in management. He knows the difference between a résumé that looks impressive and a hire who actually works. Benchmarks are doing the same thing for models: Gemini 3.1 Pro at 94.3% GPQA Diamond is a strong résumé line. But GPQA Diamond measures PhD-level science question answering — which is not the skill being recruited for when you're debugging a Next.js routing bug at midnight.

The May 2026 landscape made this especially visible: Claude leads coding, Gemini leads reasoning, GPT leads creative writing, all on different benchmark suites with different task definitions, evaluated by different parties. The leaderboard isn't lying — it's just answering a different question than "which model should I use for my codebase."

This is distinct from post #16 (A Fleet, Not a Default) which was about *how* the author selects models from personal experience. This post is about the *mechanism* of why benchmarks fail as a selection signal — and what to do instead (your own domain-specific evals, connecting to post #18, closing a loop in the catalog).

Concrete anchor: if the author ran Gemini 3.1 Pro on his actual codebase versus his actual Claude workflow, what would he measure and why? Benchmark scores are a starting point for the interview, not the hiring decision.

**What makes it timely:**
Gemini 3.1 Pro's benchmark release in May 2026 was described as having "reshaped the competitive landscape" by multiple outlets, while the Anthropic Agentic Coding Trends Report shows only 29% of developers trust AI outputs (down from 40% in 2024, despite 84% adoption). The gap between benchmark claims and practitioner trust has never been wider.
- Source: https://o-mega.ai/articles/ai-model-benchmarks-pricing-may-2026
- Source: https://uvik.net/blog/ai-coding-assistant-statistics/

---

## Proposal 4 — "State Doesn't Live in the Prompt"

**Thesis:** Treating the context window as memory is a category error — memory is an architectural problem, and more tokens don't fix it any more than more RAM fixes a badly designed database schema.

**Angle:**
The author has three data points in his own history that all point at this problem without naming it: the RAG pipeline (post #7) that failed because retrieval was never built; the agent architecture (post #19) that he recognized as a state machine; and CLAUDE.md (mentioned in post #20) as a "memory layer." None of those posts asked the direct question: where does state actually live in a production AI system?

The "context rot" problem is real and documented: models catch information at the start and end of a long context but lose the middle. A 2M token window still forgets after the session ends. The architectural answer has three distinct layers — episodic memory (what happened this session), semantic memory (persistent facts/knowledge), procedural memory (how-to patterns). Each requires a different solution.

The concrete anchor here is uncomfortable: every careful CLAUDE.md the author writes is doing manual memory hydration. Every time the context resets, he's rebuilding state by hand. That's a workaround, not an architecture. Naming it is the first step to designing around it.

This covers completely new ground relative to posts #7 (ingestion story, not statefulness), #19 (orchestration shape, not session state), and #20 (mentioned memory layer without analyzing it). Memory as a first-class architectural concern hasn't been tackled.

**What makes it timely:**
mem0.ai published "State of AI Agent Memory 2026" in May, naming memory as a first-class architectural component with its own benchmark suite. QCon London 2026 featured a talk titled "Beyond Context Windows: Building Cognitive Memory for AI Agents." VentureBeat covered the GAM (Generalized Associative Memory) paper that directly challenges the long-context approach.
- Source: https://mem0.ai/blog/state-of-ai-agent-memory-2026
- Source: https://venturebeat.com/ai/gam-takes-aim-at-context-rot-a-dual-agent-memory-architecture-that
- Source: https://qconlondon.com/presentation/mar2026/beyond-context-windows-building-cognitive-memory-ai-agents

---

## Proposal 5 — "Story Points Were Always a Proxy"

**Thesis:** Engineering teams have always measured proxies instead of value delivered — AI didn't break engineering productivity metrics, it just made the gap between the proxy and the thing impossible to ignore.

**Angle:**
Matias spent 14 years managing engineering teams. Story points, velocity, PR throughput, lines of code — these were always imperfect proxies for the thing that actually mattered (are we delivering value?). They worked roughly because implementation effort correlated with complexity and impact. If a feature took 5 story points of effort, it was probably doing something non-trivial.

AI broke that correlation completely. A developer with Claude Code can generate 10x the PRs in a sprint. Velocity goes to infinity. Story points stop meaning anything. The instinct — which he's probably seen or heard in engineering leadership discussions already — is to invent new proxies (AI-code percentage, acceptance rate, lines reviewed). That's the same mistake at the next level.

The real insight is management-flavored, which fits the catalog's occasional return to the author's leadership past: this is the forcing function that should finally move engineering measurement toward business outcomes and system quality over time. The ownership cost from post #21 (refactors sweep wider, migrations touch more) is one version of quality. User outcomes is the other.

This is distinct from post #10 (SDLC compression — about phases), post #12 (typing used to be the lesson — about the junior feedback loop), and post #21 (building is cheap, owning isn't — about ownership cost at the technical level). None of those posts addressed what happens to *management measurement systems* specifically. That's new ground.

**What makes it timely:**
The "AI Coding Assistant Statistics & Trends 2026" report claims a 31.4% average productivity increase from AI tools — measured in developer-hours-per-feature or lines-of-code-per-day. No one in the report defines what productivity means. That definitional void is the post.
- Source: https://www.secondtalent.com/resources/ai-coding-assistant-statistics/
- Source: https://resources.anthropic.com/hubfs/2026%20Agentic%20Coding%20Trends%20Report.pdf

---

*Generated 2026-05-25. Catalog cross-referenced against 21 published posts. Trends sourced from web searches conducted same date.*
