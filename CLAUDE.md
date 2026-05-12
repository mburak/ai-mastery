# AI Mastery Blog — CLAUDE.md

This file lives in the ai-mastery repo root so any Claude Code session opened here has full blog context.

## Blog overview

GitHub Pages blog at mburak.github.io/ai-mastery. Jekyll with minima theme (dark skin). Posts in `_posts/`, drafts in `blog-drafts/`.

## Published posts (keep this updated)

1. `2025-12-28-what-i-thought-i-knew-about-ai.md` — "What I Thought I Knew About AI." Surprises from going deep on AI: tokenization (BPE), attention/BERT, compound AI systems. ~480 words, includes source links.
2. `2026-01-05-what-building-an-ai-product-taught-me.md` — "What Building an AI Product Taught Me About Engineering." Engineering lessons from building an AI product: system design > model, ETL/pipeline analogy, scoping discipline, compound AI in practice. ~390 words.
3. `2026-01-12-i-didnt-go-back-to-coding.md` — "I Didn't Go Back to Coding." The shift from vibe coding (GPT-4, 2024) to spec-driven development (Claude Opus 4.5, late 2025). Returning to IC feels different now — less like coding, more like architecture. ~430 words.
4. `2026-01-19-why-im-going-deep.md` — "Why I'm Going Deep." Why go deep on AI when things are already working. Driven by hitting limits (chunking/retrieval, debugging blind) and co-founding a company where AI is the core technology. The gap is about the whole picture, not just internals. ~300 words.
5. `2026-01-26-what-management-actually-prepared-me-for.md` — "What Management Actually Prepared Me For." Management habits (specs, scoping, handling unreliable systems) transferred directly to AI product development. Stayed technical through side projects but pace/focus different. ~370 words.
6. `2026-02-02-its-not-about-trust.md` — "It's Not About Trust." Trust is the wrong frame for AI coding assistants — knowing failure modes is better. Multi-model verification workflow, tests + model review as complementary layers, better models introduce new risks. ~390 words.
7. `2026-02-09-the-pipeline-i-built-and-never-finished.md` — "The Pipeline I Built and Never Finished." RAG pipeline post-mortem: Obsidian notes, text-embedding-3-large, pgvector/Supabase, delta processing. Chunking was AI-suggested, retrieval layer never built. Key insight: start with retrieval, not ingestion. ~280 words.
8. `2026-02-16-what-actually-slows-you-down.md` — "What Actually Slows You Down." The real friction when building with AI: the gap between building speed and understanding. Understanding gap, context loss, spec drift — three versions of the same problem. ~320 words.
9. `2026-02-23-two-months-in.md` — "Two Months In." Two month retrospective on going deep on AI. Faster, knows what he doesn't know, reads differently, more confident in technical conversations. Black box gap remains. Closer: "I know enough to know how much I don't know yet." ~340 words.
10. `2026-03-02-the-sdlc-didnt-go-away.md` — "The SDLC Didn't Go Away." 27-year SDLC perspective: agile compressed waterfall's upfront design, CI/CD compressed deployments, now AI is compressing implementation. Unlike previous shifts, the work didn't move to new disciplines — it moved back to phases we thought we'd minimized (specs, design, review). ~395 words.
11. `2026-03-09-same-prompt-different-code.md` — "Same Prompt, Different Code." The shift from deterministic to non-deterministic engineering. Distinguishes plumbing non-determinism (race conditions, eventually-consistent DBs) from semantic non-determinism (model output varies in what it's trying to do). Changes how you debug, test, and where confidence comes from. ~415 words.
12. `2026-03-16-typing-used-to-be-the-lesson.md` — "Typing Used to Be the Lesson." 14yr-management + 27yr-engineering perspective on how AI breaks the junior-to-senior path. The forced feedback loop (won't compile, test fails) that built engineers automatically is now mediated by models. New failure mode: looking competent without being competent. Understanding now requires deliberate choice. ~385 words.
13. `2026-03-23-text-isnt-text.md` — "Text Isn't Text." First technical deep dive on the blog. Tokenization (BPE): the model sees subword chunks as integer IDs, never letters. The conceptual shift for a senior engineer trained on "the string is the data" — now the string is an interface. Acknowledges strawberry meme but anchors on deliberate tokenizer investigation. ~410 words.
14. `2026-03-30-i-still-type-some-things-myself.md` — "I Still Type Some Things Myself." First contrarian post. Three categories where Matias deliberately skips AI: small changes (overhead exceeds benefit), learning new tech (typing is the learning), writing in his own voice (CLAUDE.md voice rule). Reframe: the better question isn't "should I use AI?" but "is producing output what I actually want?" ~415 words.
15. `2026-04-06-the-one-process-cant-fix.md` — "The One Process Can't Fix." Three-tier framework for AI failures: famous ones (work around), unnamed ones (build process around), and over-complexification (strip out by hand). Structured workflow (specs/plans/tasks) fixed instruction drift and unwanted refactors. Over-complexification persists because it's a trained-in prior — the model's idea of "good code" leaks through every constraint. ~395 words.

## Voice rules

- Simple, casual, conversational. Write like a person talking, not an essay.
- No hyphens in compound words (use "human readable" not "human-readable").
- No AI-polished language. No words like "delve", "landscape", "journey" (unless natural).
- No specific plan references (no week numbers, no "24-week plan").
- Direct, honest tone. Admits what he got wrong. Shows real thinking, not polished conclusions.
- Short paragraphs. ~400-500 words per post.
- Read it out loud. If it sounds like a LinkedIn post or a press release, rewrite it.
- Use **bold** for a key insight worth highlighting — once or twice per post at most.
- Use *italic* for emphasis within a sentence, sparingly.
- Use links for technical terms or concepts with good reference material. Don't over-link. Always add `{:target="_blank"}` so links open in a new tab.

## About Matias (for voice and accuracy)

- 27+ years in software engineering. Gone back and forth between building things and leading teams throughout his career (not a straight line into management).
- About 14 years in management/leadership roles (Head of Engineering, CTO, EM at a large tech company), but also returned to IC roles multiple times.
- Been into AI for years — courses, side projects, built apps with AI coding assistants. In late 2025 he decided to go deep. This is NOT a new interest, it's an intensification.
- Co-founding an AI startup as of Dec 2025.

## Confidentiality rules (important)

- The startup is NEVER mentioned on the blog. No product name, no domain, no specific use case. The startup builds AI-powered tools for household bureaucracy (government docs, civic admin) but none of this goes on the blog.
- Don't name his previous large tech employer specifically in blog posts.
- Don't link to LinkedIn.
- When discussing engineering lessons from the startup, keep it abstract — talk about patterns (pipelines, compound AI, scoping) without revealing what the product does.

## Content angle

"Experienced engineer going deep on AI" perspective. Focus on surprises, misconceptions corrected, what clicked, engineering insights. Not tutorials. Accessible to non-experts but not naive to experts.

## AI Mastery Tracker (Google Sheet)

The source of truth for Matias's learning progress:
**URL:** https://docs.google.com/spreadsheets/d/1lIWKaAEMNgNZWY_u0zaJavNyfRqMua_Xtvy1FAC9Bh8/edit

Tabs: Dashboard, Weekly Tracker, Kindle Reading Log, Projects, Blog & Content, Phase Assessments, Review Sessions, Daily Planner.

Plan start date: Monday, April 13, 2026. Use `--chrome` to access this sheet and check learning progress when writing new posts or tracking activities.

Log every learning activity (reading, watching, listening, podcasts, blog posts, etc.) in the Learning Log tab. Columns: Date, Type, Title, Source/URL, Phase, Duration (min), Key Takeaway/Notes.

## How to work with Matias

- **Assess actively.** Don't just track completion — assess projects, blog posts, and code. He values honest evaluation over encouragement. He's a 27+ year veteran who can handle direct feedback.
- **Don't sugarcoat.** If a post is weak, say why. If code is tutorial-grade not production-grade, flag it.
- **Help with writing.** He says he's not a strong writer and wants active help structuring and sharpening posts. Best approach: he shares raw takeaways/ideas, Claude helps structure into a publishable post.

## Workflow

Edit files locally, commit, and push with git. After pushing, verify the GitHub Actions build passes and the site renders correctly at mburak.github.io/ai-mastery. Use `--chrome` flag to access the Google Sheet tracker and verify the live site.
