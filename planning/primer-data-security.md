# What Does Your AI Actually See?
## Four Approaches to Data Security

*Pre-reading for Session 5: "What Does Deployment Look Like?"*
*Estimated reading time: 5 minutes*

---

### The Core Problem

When an AI agent queries your enterprise data, the data has to go somewhere. The agent generates SQL, runs it against your database, and gets results back. But then what? The LLM needs to *read* those results to write a summary, spot a trend, or answer a follow-up question. That means your revenue figures, customer names, or employee compensation data are flowing through an AI system — and the question becomes: who else can see it?

Four policy decisions control data exposure. Most organizations combine two or more. Here's what each one does, what it costs, and where it breaks down.

---

### Approach 1: Zero Data Retention

**How it works:** Your data is sent to the LLM provider's servers for processing, but the provider contractually agrees to delete all inputs and outputs immediately after generating a response. Nothing is stored, logged, or used for training. The data passes through but doesn't stick.

**Who uses this:** Morgan Stanley chose this approach when deploying an AI assistant to 16,000 financial advisors. They negotiated a zero-retention agreement with OpenAI, meaning client portfolio data could be sent for analysis but was never stored on OpenAI's servers. For a firm under SEC and FINRA scrutiny, the contractual guarantee was the key enabler.

**Tradeoff:** This is the simplest approach to implement. You get the full capability of frontier models — their best reasoning, their best language quality — without building any infrastructure. But your data *does* leave your network, even if briefly. You are trusting the provider's contractual commitment and their technical implementation of that commitment. For some regulators and some data types, "it was deleted afterward" is not sufficient.

**Best for:** Organizations in regulated industries that need frontier model quality and can negotiate enterprise agreements with providers.

---

### Approach 2: Data Masking and Anonymization

**How it works:** Before query results are sent to the LLM, a data loss prevention (DLP) layer strips out personally identifiable information — names, Social Security numbers, email addresses, account numbers. The LLM sees "Employee_4782 earned $285,000" instead of "Jane Chen earned $285,000." On the return trip, sensitive values can be re-identified for the end user's display.

**What this looks like in practice:** A hospital system wants to use AI to analyze patient outcomes across departments. Before results reach the LLM, patient names are replaced with tokens, dates of birth are generalized to age ranges, and medical record numbers are stripped. The LLM can still calculate readmission rates by department and write a narrative summary — it just can't identify any individual patient.

**Tradeoff:** You preserve most of the LLM's analytical value while sharply reducing exposure. The AI can still find patterns, compute aggregates, and write summaries. But masking adds a processing layer — more latency, more engineering, more things that can go wrong. And some queries break. "Which sales rep closed the most deals last quarter?" is hard to answer when you've masked the sales rep names. You end up maintaining rules for what gets masked and what doesn't, and those rules need ongoing attention.

**Best for:** Organizations that need the LLM to interpret data but can tolerate the overhead of a masking pipeline. Common in healthcare and financial services.

---

### Approach 3: On-Premise Models

**How it works:** Run an open-source LLM (Llama, Mistral, or similar) on your own servers. Data never leaves your network — not for code generation, not for interpretation, not for anything. The LLM sees everything, but "everything" stays inside your security perimeter.

**What it costs:** GPU infrastructure runs $50,000 to $200,000 or more, depending on model size and query volume. You also need ML engineering staff to deploy, maintain, and update the model. This is not a one-time purchase — it's an ongoing operational commitment.

**Tradeoff:** You get complete data sovereignty. No vendor agreements to negotiate, no contractual trust required, no data in transit. But as of early 2026, open-source models are meaningfully less capable than frontier cloud models at multi-step reasoning, SQL generation, and natural language quality. The gap is closing — it was enormous two years ago, and it's narrowing every quarter — but it still matters for complex analytical tasks. You are trading capability for control.

**Best for:** Defense contractors, intelligence agencies, and organizations with data so sensitive that any external transmission is unacceptable regardless of contractual protections.

---

### Approach 4: Role-Based Query Filtering

**How it works:** The AI agent inherits the access permissions of the person using it. When a VP of Sales asks about revenue data, the agent can query it. When the same VP asks about HR compensation, the query is blocked — just as it would be if they tried to access that table directly. A junior analyst might see aggregate metrics (average salary by department) but not individual records.

**What this requires:** Integration with your existing identity and access management system (Active Directory, Okta, or similar). The agent checks who is asking, maps that identity to a permission set, and filters queries before they run. This is not built into most AI tools by default — it has to be configured.

**Tradeoff:** This mirrors the permission structure your organization already has, which makes it intuitive for compliance teams. A CISO can look at the agent's access rules and see the same role-based logic they already understand. But the configuration is detailed and error-prone. Every new data source, every new role, every organizational change requires updates. And the filtering happens at query time, not at the LLM level — the model itself may still be a cloud service, so this approach is often combined with Approach 1 or 2.

**Best for:** Large organizations with mature identity management that want the AI to respect existing data boundaries.

---

### Comparison at a Glance

| Approach | Data Leaves Network? | LLM Sees Real Data? | Implementation Cost | Model Quality |
|---|---|---|---|---|
| **Zero Data Retention** | Yes (temporarily) | Yes | Low | Frontier |
| **Data Masking** | Yes (anonymized) | Partially | Medium | Frontier |
| **On-Premise Models** | No | Yes | High ($50-200K+) | Lower |
| **Role-Based Filtering** | Depends on LLM choice | Filtered by user | Medium | Depends on LLM choice |

---

### The Real Answer Is a Combination

Almost no production deployment relies on a single approach. Morgan Stanley uses zero data retention *and* role-based filtering. A hospital system might use data masking *and* an on-premise model. A manufacturing company might use role-based filtering with a cloud API under a zero-retention agreement.

The question is not whether to adopt AI for enterprise data. The question is which combination of these approaches matches your organization's risk tolerance — and whether that combination still lets the AI do something useful. The tightest security means nothing if the resulting system is too limited for anyone to use.

Come to Session 5 ready to answer: for your use case, which combination fits?
