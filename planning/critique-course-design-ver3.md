# Critique: course-design-ver3.md

Synthesized from three independent reviewers (Correctness & Completeness, Clarity & Persuasiveness, Devil's Advocate). Deduplicated and prioritized.

---

## Critical

### 1. Session 4 is overloaded (all 3 reviewers)

Three distinct topics — reporting pipelines, LLM deployment, data security — in 90 minutes. 40 min of lecture, students intellectually exhausted by the breakout. v2 split this across two sessions.

### 2. Session 6 lacks anchor (Clarity + Devil's Advocate)

Without the SaaSpocalypse frame from v2, "AI as Thinking Partner" feels disconnected from the agent-focused arc. Pre-mortems and assumption audits are generic decision-support skills, not specific to this course's tools. The build-vs-buy segment at minute 70 feels bolted on.

### 3. RAG introduced too late and too compressed (Devil's Advocate + Correctness)

Session 7 introduces a conceptually different system (embeddings, vector stores, chunking) in one session. Students must then choose RAG infrastructure for their capstone homework that same night. No hands-on RAG build (only optional demo viewing).

### 4. Sessions 5-8 shift to lecture-heavy (Clarity)

Hands-on time drops sharply after Session 4. Session 5 has only 13 min of red-teaming, Session 6 has 15 min of abstract exercises, Session 7 has 14 min. Executive engagement risk.

---

## Warning

### 5. Session 2 timing overlap (Correctness)

Line 123 ends breakout at "82-88" but line 124 shows homework at "85-90" — overlapping range. Should be 88-90.

### 6. ROI template built on soft estimates (Clarity)

Session 2 gives 10 minutes to sketch a data map and estimate ROI but never teaches an estimation method. The capstone rests on this foundation.

### 7. Data security lecture is abstract (Clarity)

Session 4 describes four approaches to data privacy but never shows them in action. A 3-minute demo (ask for salary data, blocked by guardrails) would make it concrete.

### 8. Klarna case study and RAG document collection don't exist yet (Correctness)

Both are required resources with no indication they've been created. Klarna feeds directly into Session 6 discussion; RAG docs are the entire Session 7 demo.

### 9. Linux server orphaned after Session 4 (Clarity + Devil's Advocate)

Never mentioned in Sessions 5-8. Creates a two-tier experience with no accountability.

### 10. No fallback plan for live demo failure (Clarity)

Sessions 1-4 are demo-heavy on Zoom. No canned recordings mentioned for API outages.

### 11. "No coding required" vs. Session 7 RAG deployment (Devil's Advocate)

Asking executives to choose embedding models and vector stores in their capstone stretches the "no coding" promise.

### 12. Data security repeated in Sessions 4 and 5 (Correctness)

Session 4 (lines 173) covers the four approaches to managing data exposure. Session 5 (line 197) repeats "Four approaches to managing privacy (aggregated results with guardrails, blind templates, on-premise LLM, schema-only with sanitized errors)." This is redundant — either cover it once or explicitly build on it the second time.

### 13. Klarna case creates narrative whiplash (Clarity)

Session 1 opens with the inevitability of AI disruption ($2T selloff). Session 5 homework assigns a case study of a company that tried AI replacement and partially reversed. If the opening sells inevitability, the Klarna case sends a mixed message without a recovery frame.

---

## Suggestion

### 14. Teach an ROI estimation framework in Session 2

Even 5 minutes of "analyst hours x cost + decision delay cost" with a worked example would ground the template.

### 15. Session 1 "Business Lens" (min 75-88) may land when attention is waning

Consider moving it to right after the demo, before hands-on, to capitalize on the provocation.

### 16. Provide guided discussion questions for Klarna case study

3-4 specific questions rather than open-ended "what went right/wrong."

### 17. Share cross-session summary table with students

In pre-program video or Session 1 — they want to see the arc.

### 18. Capstone rubric

Share evaluation criteria in Session 7 so students know what "good" looks like.

### 19. Maker/checker reinforcement is subtle in Sessions 6-7

The recurring elements section claims reinforcement but it's more implicit than explicit in the session content.

### 20. Call out recurring threads explicitly to students

The ROI template thread, deployment architecture thread, and maker/checker theme are well-designed but only visible in the instructor-facing recurring elements section. Students would benefit from hearing "we'll build on this template throughout the course" in Session 2.

### 21. Session 3 optional build is key but labeled "optional"

The "Optional: Live Build with Claude Code" (line 147) is the primary vehicle for the "50 lines of code" learning objective. If it's truly optional, some students may not internalize agent architecture. Consider making it a required viewing of a pre-recorded demo instead.

### 22. Cost modeling under-specified

Session 4 gives one cost example ($0.01-0.05 per query) but doesn't teach students how to build a cost model. RAG costs (embedding API, vector store hosting) are not quantified in Session 7.

### 23. Change management and organizational resistance under-covered

Sessions address "who has the judgment to verify" but not how to drive adoption, retrain reporting teams, or navigate middle management resistance. Session 8 mentions "establish governance before shadow IT" but doesn't address the human side of the transition.

### 24. No vendor selection framework

The course is heavy on "build vs. buy" but most enterprises will buy. No framework for evaluating Salesforce Agentforce vs. Cohere vs. a custom build. No guidance on what questions to ask a vendor.
