# What Does Your AI Actually See?
## Four Approaches to Data Security When AI Agents Access Enterprise Data

*Pre-reading for Session 5: "What Does Deployment Look Like?"*

---

### The Problem

When an AI agent queries your enterprise data, it generates SQL, runs it, and interprets the results. In Session 3, we discussed where the *code* executes — on the vendor's servers (cloud sandbox) or on yours (Docker containers). But there's a second question that's easy to miss:

**Even when code runs on your servers, the LLM still sees the query results.**

If someone asks "Show me VP compensation above $300K," the code runs locally — but the results (names, titles, salary figures) must be sent back to the LLM so it can write a natural language answer. The LLM needs to see the data to interpret it, spot anomalies, fix errors, and generate narratives. That's what makes it useful. It's also what makes it a privacy concern.

Running code locally protects you from one risk (data leaving your network for execution). It does not protect you from another (data being read by an external LLM for interpretation). These are separate decisions.

### Four Approaches

Organizations managing this tradeoff typically land on one of four approaches. Each makes a different bet on the quality-vs-privacy spectrum.

**Approach 1: Aggregated Results with Guardrails** *(most common in practice)*

The LLM sees aggregated data — totals, averages, counts by category — but not individual records. A data loss prevention (DLP) layer sits between the database results and the LLM, scanning for and redacting anything that looks like PII (names, Social Security numbers, email addresses). Row limits prevent bulk extraction. The compliance team signs off on which data categories the LLM may see.

*Tradeoff:* The LLM can still analyze trends and write narratives. It cannot drill into individual records or spot outliers at the person level.

**Approach 2: Blind Templates** *(used in banking and healthcare)*

The LLM generates SQL and Python code, but results are rendered directly to the user's browser — they never pass through the LLM. Instead, the LLM writes "blind" templates with placeholders: "The top region by revenue is {region_1} at {revenue_1}." The application fills in the actual values. The LLM is a code generator, not an analyst.

*Tradeoff:* Maximum privacy — the LLM never sees real data. But the LLM can't adapt its analysis, notice anomalies, or provide insight beyond what the template anticipated. Useful for standardized reports; poor for ad hoc questions.

**Approach 3: On-Premise LLM** *(for maximum control)*

Run an open-source model (Llama, Mistral, or similar) on your own hardware. No data ever leaves your network — not for code execution, not for interpretation. The LLM sees everything, but "everything" stays inside your security boundary.

*Tradeoff:* Complete data sovereignty. But open-source models are significantly less capable than frontier models (Claude, GPT-4) at SQL generation, multi-step reasoning, and natural language quality. This gap is closing but remains large as of early 2026. You also absorb the infrastructure cost ($50-200K+ for GPU hardware) and the operational burden of running and updating the model.

**Approach 4: Schema-Only** *(a practical middle ground)*

The LLM sees only database schemas and synthetic sample rows — never real data. It generates all code "blind." Results go directly to the user. For the debug loop (when the generated SQL errors out), error messages are sanitized before being sent back to the LLM: data values are stripped from tracebacks, keeping only error types and line numbers.

*Tradeoff:* Strong privacy with reasonable capability. The LLM can generate accurate SQL from schema descriptions alone. But it cannot interpret results, write data-driven narratives, or catch data quality issues. Used by some financial services companies as a compromise between Approach 1 and Approach 2.

### This Is a Policy Decision

The technology to implement any of these four approaches is straightforward. Aggregation filters, DLP layers, blind template engines, and schema-only configurations are all well-understood engineering. The hard part is deciding which approach fits your organization — and that depends on your industry, your regulators, your risk tolerance, and what you need the AI to actually do.

A company that needs the AI to write narrative summaries of customer data (Approach 1) is making a fundamentally different bet than one that only needs it to generate SQL queries (Approach 4). Neither is wrong. Both are defensible. The question for your compliance team is: **what level of data exposure to the LLM is acceptable, given what you're trying to accomplish?**

Come to Session 5 ready to answer that question for your use case.
