# Course Design v5: From BI to AI — Data-Driven Decision Making with Agentic AI
## An 8-Session Executive Program (4 weeks, 90 min each, Zoom)

### Course Description

AI agents that understand plain English are transforming how professionals work — generating charts, writing documents, building Excel analyses, automating reporting pipelines, and querying enterprise data. In this four-week program, you will use AI tools to boost your personal productivity from day one, then extend those skills to enterprise data systems, deployment architecture, and governance. You will leave equipped with tools you can immediately use in your daily work and a concrete strategy for bringing AI-powered capabilities to your organization.

### Pre-Program Video

Before Session 1, participants watch a 15-20 minute video covering:
- What AI agents are and why they matter — both for personal productivity and enterprise decision making
- Course tools: Claude (claude.ai), Claude Desktop, and Claude Code — which tool for which task
- The Meridian Corp simulation: a $500M distributor with 10 enterprise systems (introduced in Week 2)
- The Linux VM: an optional hands-on environment for those who want to build agents themselves
- The course arc: personal productivity → enterprise data → deployment and trust → strategy
- How to log in and what to expect in Session 1

This allows Session 1 to begin immediately with hands-on work.

---

## Course Resources

### Claude AI Tools (browser and desktop, no installation required for claude.ai)

Students use three AI interfaces throughout the course:

- **Claude.ai** (browser) — The primary tool for Sessions 1-2. Conversational AI with artifacts: interactive charts, documents, calculators, and code. Think of it as a fast junior analyst who drafts, you direct and verify.
- **Claude Desktop** (optional install) — Extends Claude with local file access and MCP integrations. Useful for working with your own spreadsheets and documents.
- **Claude Code** (terminal) — An AI coding assistant that builds tools from English descriptions. Used by the instructor in demos; available to students on the Linux server.

### The Meridian Corp App (browser-based, no installation)

A web-based AI data assistant that simulates a real enterprise data environment. Students open a browser, log in, and ask questions in plain English. The app connects to **10 enterprise systems** for a fictional $500M B2B industrial supplies distributor with three operating divisions:

- **Industrial Division** (~$250M): Salesforce CRM, NetSuite Finance, SAP Operations
- **Energy Division** (~$150M): Legacy CRM (custom-built), QuickBooks Finance, Oracle SCM
- **Safety Division** (~$100M): HubSpot CRM, shared NetSuite Finance
- **Corporate HQ**: Workday HR (all divisions), NetSuite Consolidation, Zendesk Support

The data includes realistic cross-system friction: Salesforce uses CamelCase column names while the Legacy CRM uses snake_case; the Legacy CRM stores dates as text strings ("MM/DD/YYYY") instead of proper dates; and ~25 customers appear under different names across divisions (e.g., "General Electric" in Salesforce, "GE Industrial Solutions" in the Legacy CRM, "GE Safety Division" in HubSpot).

The AI agent queries each system separately — it cannot join across systems in a single query. For cross-system questions, it pulls data from each system, then uses Python to merge, reconcile, and analyze the combined results. This mirrors how a real enterprise AI tool would work.

Beyond answering questions, the agent generates deliverables: charts, written analyses, Word documents, Excel workbooks, and PowerPoint decks — all grounded in the fictional company's data.

**41 tables, 26,000+ rows, 3 years of data (2023-2025).** Students can query sales pipelines, financial statements, employee compensation, supply chain performance, and support tickets — and combine data across all of them.

Introduced in Session 3, the Meridian Corp app is the primary hands-on environment for Sessions 3-7.

### The Linux Server (optional, for hands-on building)

A shared Linux server with individual student accounts, pre-installed with Claude Code (an AI coding assistant). Students who want hands-on experience can SSH in and build working data agents with AI assistance — they type directions in English, and the AI writes the Python code.

Four scaffolded exercises are pre-loaded:
- **Exercise 1**: Build a 50-line agent that queries one database (~30 min)
- **Exercise 2**: Extend it to query two systems and merge results (~30 min)
- **Exercise 3**: Wrap it in a web interface (~45 min)
- **Exercise 4**: Red-team the agent for security vulnerabilities (~30 min)

The server exercises are optional throughout the course. They are demonstrated by the instructor in Session 4 and available for self-paced exploration. Students who complete them gain a deeper understanding of how agents work, but the course does not require terminal or coding experience.

### Recorded Demos (optional, for deeper understanding)

Seven pre-recorded demos show the full build journey from a blank file to a production-style system. Each is recorded on the Linux VM using the same environment students have access to. Students who want to replicate any demo can SSH in and follow along. Links are provided in the homework for the paired session.

**Demo 1: "Hello World Agent" (~15 min)** — *pairs with Session 4*
Start from an empty file. Tell Claude Code in English to build a Python script that takes a question, sends it to Claude with a schema description, gets back SQL, runs it against a parquet file, and prints the answer. Show the ~50 lines it produces. Run it. Ask a question. Get an answer. The student sees the entire agent loop created from a plain English description.

**Demo 2: "Adding a Second System" (~15 min)** — *pairs with Sessions 3-4*
Start from the Demo 1 agent. Tell Claude Code to add a second database (Workday HR) so the agent can query both and merge. Show the agent deciding to query CRM + Workday for "revenue per employee by division." Show the fuzzy matching problem when customer names don't align. The cross-system merge from Session 3 becomes visible in code the student can read.

**Demo 3: "Wrapping It in a Web App" (~15 min)** — *pairs with Session 4*
Start from the Demo 2 agent. Tell Claude Code to wrap it in a simple web app with a chat interface. Claude Code generates a FastAPI backend + HTML frontend. Open a browser, type a question, get an answer with a chart. The student goes from a script to something that looks like the Meridian app in under an hour of total work.

**Demo 4: "Building a Reporting Pipeline" (~20 min)** — *pairs with Session 4*
Tell Claude Code to build a script that queries revenue by division, compares to prior quarter, generates a chart, writes a narrative summary, and saves it as a formatted report. Show the pipeline running end to end. Then show scheduling it to run weekly and adding a human review gate — the report is drafted but held for approval before sending. The "ad hoc to automated" transition from Session 4 becomes concrete.

**Demo 5: "Red-Teaming Your Agent" (~15 min)** — *pairs with Session 6*
Start from the Demo 2 agent (no guardrails). Try SQL injection, ask for salary data, ask about nonexistent divisions. Show what fails — the agent returns individual salaries, doesn't validate SQL, hallucinates when data doesn't exist. Then add guardrails one by one: SQL validation, row limits, access control checks, "I don't know" responses. Guardrails aren't automatic — seeing the vulnerabilities firsthand makes the Session 6 governance discussion real.

**Demo 6: "Building a RAG System" (~20 min)** — *pairs with Session 7*
Start fresh with a folder of Meridian Corp documents (employee handbook, vendor contracts, compliance policies). Tell Claude Code to build a document Q&A system: chunk the PDFs, embed them, store in a vector database, and answer questions with cited passages. Show the full pipeline: PDF parsing → chunking → embedding → vector store. Ask questions and get answers with page citations. Then show a failure: a question where chunking split a relevant passage, demonstrating how chunk size affects retrieval quality.

**Demo 7: "Combining Database + Document AI" (~15 min)** — *pairs with Session 7*
Combine the Demo 2 database agent with the Demo 6 RAG system. Ask: "What's our contractual commitment to GE, and how does their actual spending compare?" RAG retrieves the contract terms; the database agent pulls spending data; the LLM synthesizes both. Show the orchestration: two retrieval paths (vector search vs. SQL), results merged by the LLM. This is the full vision — structured and unstructured company knowledge, accessible through one interface.

### Instructor Note: Demo Fallbacks

Pre-record fallback versions of the highest-risk live demos (Session 1 SaaSpocalypse chart generation, Session 3 Cross-System Merge, Session 4 Full Pipeline, Session 7 RAG Q&A). If Claude or the Meridian app is down during a Zoom session, switch to the recording and narrate over it.

---

## Session-by-Session Outline

---

### SESSION 1: "What AI Can Do for You"
**Monday, May 4 — Personal Productivity with AI**

**Learning objectives:**
- Understand why AI agents matter now — the market signal and the personal opportunity
- Experience AI as a personal productivity tool: charts, documents, analysis
- Begin developing a "fast junior analyst" mindset — AI drafts, you direct and verify

**Session flow:**

| Min | Segment | Format |
|---|---|---|
| 0-15 | **Welcome and the "Why Now."** Quick recap of what the pre-program video covered — the tools, the arc, what you'll be able to do by Session 8. Then the context: in February 2026, AI agents wiped $2 trillion from software company valuations. The "SaaSpocalypse" — investors decided that AI can replace large categories of enterprise software. Whether or not you agree with the market's verdict, the technology behind it is real. But this course doesn't start with enterprise software. It starts with you. Before AI transforms your organization, it can transform your Tuesday afternoon. That's where we begin. | Lecture + Q&A |
| 15-25 | **Demo: AI as Your Analyst.** Open Claude.ai. Ask it to generate a quarterly sales comparison chart from a pasted table of numbers. Show the interactive artifact — hover, filter, export. Then: "Turn this into an executive summary memo." Then: "Now make this a PowerPoint-ready slide with bullet points." Three deliverables in 3 minutes. Students see the speed and the format flexibility. Key framing: this is a fast junior analyst. It drafts; you direct and verify. | Live demo |
| 25-35 | **The Tool Landscape.** Claude.ai for conversational work and artifacts. Claude Desktop for local file access (your spreadsheets, your documents). Claude Code for building tools from English descriptions (the instructor will use this in later sessions). Which tool for which task: browser tab for quick analysis, Desktop for working with your own files, Code for automation. Students will use claude.ai today; Desktop is introduced next session. | Lecture |
| 35-55 | **Hands-on: Your First Artifacts.** Students open Claude.ai and work through guided exercises: (1) Paste a sample dataset and ask for a chart — bar, line, or scatter. Iterate: change colors, add labels, switch chart types. (2) Ask Claude to build an interactive calculator — e.g., a break-even analysis or ROI estimator. (3) Ask Claude to draft a one-page executive summary from a provided briefing document. Each exercise demonstrates a different artifact type: visualization, interactive tool, written document. | Hands-on |
| 55-65 | **Open Exploration.** Students try their own tasks. Challenge: bring something from your actual work — a dataset, a document to summarize, an analysis you need. Instructor highlights interesting use cases in real time. | Hands-on |
| 65-82 | **Breakout Discussion (groups of 3-4).** What surprised you? What would you use this for tomorrow? What tasks do you spend time on that follow a pattern AI could accelerate? Each group shares one insight. | Breakout rooms |
| 82-87 | **The Maker/Checker Preview.** Quick framing for the course: everything AI produces needs verification. The level of verification depends on the stakes. A chart for your own understanding? Glance at the axes. A board presentation? Check every number. This "maker/checker" mindset runs through the entire course. We'll formalize it next session. | Lecture |
| 87-90 | Homework assignment | Wrap |

**Homework:** (1) Use Claude.ai for at least 3 real work tasks this week — a chart, a document draft, an analysis, a summary, whatever fits your workflow. Screenshot or save the outputs. (2) For each task, note: what was good, what needed editing, how long it would have taken you without AI. Bring your best example and your worst example to Session 2.

---

### SESSION 2: "Iterate, Critique, Trust"
**Wednesday, May 6 — The Maker/Checker Framework**

**Learning objectives:**
- Master the iteration cycle: draft → critique → revise → verify
- Understand calibrated trust: low/medium/high stakes require different verification
- Use skills and structured prompts to get consistently better output

**Session flow:**

| Min | Segment | Format |
|---|---|---|
| 0-12 | **Homework debrief.** 3-4 students share their best and worst AI outputs from the week. What worked? What didn't? Pattern recognition: where did AI save time, and where did it need heavy editing? | Discussion |
| 12-27 | **Demo: The Art of Iteration.** Take a mediocre first draft from the homework debrief (or a prepared example). Show the iteration cycle: "This is too generic — make it specific to our Q4 results." "The chart is misleading — use a zero baseline." "Rewrite the executive summary in half the length." Then the power move: ask Claude to critique its own work. "What's weak about this analysis? What would a skeptical CFO push back on?" Watch it identify its own gaps. Then: "Fix those issues." Two rounds of self-critique produce dramatically better output. | Live demo |
| 27-40 | **The Maker/Checker Framework.** Formalize what they experienced in Session 1. AI is the maker; you are the checker. The skill shift: from producing analysis to directing and verifying it. Calibrated trust: **(1) Low stakes** — internal notes, brainstorming, personal charts → quick sanity check. **(2) Medium stakes** — team presentations, internal reports → verify numbers, check sources. **(3) High stakes** — board decks, regulatory filings, public-facing documents → independent verification of every claim. The right level of checking depends on what happens if the output is wrong. | Lecture + discussion |
| 40-50 | **Demo: Skills and Structured Prompts.** Show how to create reusable instructions — a "skill" or system prompt that produces consistent output. Example: a weekly status report template that always includes the same sections, formatting, and tone. Write it once, reuse it every week. Show how sub-agents can work in parallel — one drafts, one critiques, one fact-checks. The /critique pattern: 3 parallel reviewers provide independent feedback. | Live demo |
| 50-65 | **Hands-on: Build Your Own Workflow.** Students pick a recurring task from their work and build a reusable prompt or workflow for it. Options: (1) A weekly report template with specific sections and tone. (2) A data analysis workflow: "Given a CSV, always produce these 5 charts and a summary." (3) A document review checklist: "Read this document and flag issues in these categories." Students iterate and refine using the critique technique from the demo. | Hands-on |
| 65-78 | **Breakout: Your Productivity Portfolio (groups of 3-4).** Each person shares the workflow they built. Compare: what types of tasks came up? What patterns are common? What level of trust (low/medium/high) does each task require? Each group identifies their top 3 use cases where AI saves the most time with acceptable risk. | Breakout rooms |
| 78-85 | **Bridge to Enterprise Data.** "Everything you've done so far uses data you paste in or documents you upload. But most of the data that drives business decisions lives in enterprise systems — CRMs, ERPs, HR platforms. Starting next session, we connect AI to those systems. You'll use the same skills — iteration, critique, verification — but now the AI is querying real databases instead of working from what you paste in." Preview the Meridian Corp simulation. | Lecture |
| 85-90 | Homework | Wrap |

**Homework:** (1) Continue using Claude.ai for real work tasks. Build at least one reusable workflow and test it 2-3 times. (2) Read the enterprise systems background document (provided) — what Salesforce, SAP, Workday, NetSuite, and other enterprise systems actually do. (3) Think about your company's data landscape: what are the top 3-5 systems your organization relies on? What cross-system questions can nobody answer easily today? Bring your list to Session 3.

---

### SESSION 3: "AI Meets Your Data"
**Monday, May 11 — Enterprise Data Access**

**Learning objectives:**
- Experience conversational data access vs. traditional dashboards on enterprise systems
- Watch AI query multiple systems and merge results in real time
- Map their own company's data landscape and identify high-value use cases

**Session flow:**

| Min | Segment | Format |
|---|---|---|
| 0-8 | **Bridge.** "You've spent a week using AI for personal productivity — charts, documents, workflows. Now we scale up. The same AI that drafts your memos can also query your company's databases. But enterprise data is scattered across 5, 10, sometimes 20 systems. Let's see what that looks like." | Lecture |
| 8-13 | **Cold open: the 3-week email chain.** A CEO asks "which of our customers buy from multiple divisions?" The BI team says 3 weeks. Show the email chain. Ask: has this happened to you? | Provocation + discussion |
| 13-23 | **Demo: Dashboard vs. Chat.** Open the Meridian Corp app and ask the same question. Get an instant answer. Ask follow-ups the dashboard can't handle. Students see SQL, charts, narrative — all from a chat interface. | Live demo |
| 23-33 | **The Business Lens.** Connect the demo back to the SaaSpocalypse from Session 1. The technology you just saw — querying enterprise data in plain English, getting instant charts and narratives — is what the market believes will displace dashboards, reporting teams, and data integration tools. If anyone in your company could do what you just saw, what changes? | Lecture + discussion |
| 33-53 | **Hands-on: Your First Enterprise Queries.** Students log into the Meridian app and work through guided prompts. Start with single-system queries — Salesforce pipeline, NetSuite financials, Workday headcount. Then cross-system: "Which customers buy from multiple divisions?" Watch the agent query Salesforce, Legacy CRM, HubSpot separately, merge with Python using fuzzy matching. Then: "Revenue per employee by division?" — queries CRMs + Workday, merges. Include a timed challenge: "Which division's top customer is most at risk of churning?" (requires CRM + Zendesk data). | Hands-on |
| 53-63 | **Workshop: Your Company's Data Map.** Each student sketches their company's 3-5 core systems and identifies one cross-system question nobody can answer easily today. Who answers it now? How long does it take? This data map carries forward — it becomes the foundation for your capstone strategy. | Individual work |
| 63-78 | **Breakout: How Scattered Is Your Data? (groups of 3-4).** Compare data maps. What systems do you have in common? Where is integration hardest? What cross-system questions would have the most business value? Each group reports: one common pattern and one surprising idiosyncrasy. | Breakout rooms |
| 78-87 | **What We're Skipping.** Before any agent can query real systems, someone must: catalog the data, document schemas, provision API access, classify PII. This is 60-90 days of pre-work that the demo does not show. Name it now so expectations are calibrated. Also: how data moves today — APIs, integration platforms (MuleSoft), ETL/data warehouses, CSV exports. The traditional answer is a warehouse ($500K-5M, 6-18 months). The alternative: query each system where it lives. Both have tradeoffs. | Lecture |
| 87-90 | Homework | Wrap |

**Homework:** (1) Log into the Meridian app and ask 10 business questions — at least 3 cross-system. Write down one question the agent answered well and one where it was unsatisfying or wrong. Bring both to Session 4. (2) Complete your data map: list at least 5 systems your company uses and the top 3 cross-system questions you can't answer today.

---

### SESSION 4: "From Data to Deliverable"
**Wednesday, May 13 — Reporting Pipelines and the Agent Loop**

**Learning objectives:**
- See the full pipeline: data → chart → narrative → board-ready memo
- Understand the agent loop as an orchestrated test-and-review cycle
- Produce a complete deliverable and iterate on quality using the maker/checker skills from Session 2

**Session flow:**

| Min | Segment | Format |
|---|---|---|
| 0-10 | **Homework debrief.** Students share best and worst answers from Meridian exploration. Why was the bad answer bad? What verification would have caught it? Apply the maker/checker framework from Session 2: what level of trust does each answer deserve? | Discussion |
| 10-25 | **Demo: The Full Pipeline.** Ask the Meridian app: "Prepare a quarterly executive summary of Meridian Corp performance — revenue by division, headcount efficiency, top customer risks, and supply chain issues." Watch it query 6 systems, merge data, generate charts, and produce a structured memo. Then iterate using Session 2 techniques: "Make this a traffic-light format with red/yellow/green." "Make this one page and lead with the biggest risk." Prompt specificity drives output quality. | Live demo |
| 25-38 | **How the Agent Loop Works.** Pull back the curtain. Show what happens behind the scenes: the system prompt (schema description), the tool call (SQL), the result, the merge (Python), the final response. Walk through the 50-line core loop on screen. Key insight: this is a test-and-review cycle — the LLM writes code, the system executes it, the LLM reviews the results, decides if they're correct, and either delivers the answer or tries again. Then show how changing the schema description changes the SQL — the prompt is the "institutional knowledge" layer. | Live demo + code walkthrough |
| 38-48 | **From Ad Hoc to Automated.** In production, these pipelines run on schedules: Monday morning dashboard refresh, monthly board deck, weekly sales forecast. Architecture: the same agent loop, triggered by a cron job instead of a chat message. What changes: error handling, version control, human review gates. **Real-world example:** HPE's CFO Marie Myers used an AI agent ("Alfred") to replace a 100-slide weekly performance review that consumed hundreds of person-hours. Results: 40% faster reporting cycle, 25% lower processing costs, 90% reduction in manual prep. This is exactly the pipeline you just saw — and it's a benchmark for what's realistic in your capstone. | Lecture |
| 48-53 | **Live Walkthrough: Building an Agent from Scratch.** The instructor builds a simple agent in real time on the Linux server using Claude Code, narrating each step. Students watch the 50-line agent come to life in minutes — from English instructions to working code. This is the "your developer could do this" moment. | Live demo (instructor-driven) |
| 53-68 | **Hands-on: Build Your Own Report.** Students use the Meridian app to produce specific deliverables. Three guided exercises: (1) "Create a customer risk report combining CRM pipeline data with support ticket trends." (2) "Produce a division-level P&L comparison with commentary on headcount efficiency." (3) "Generate a board-ready memo comparing Q3 and Q4 performance across all divisions with charts." Iterate on prompts using the techniques from Sessions 1-2. | Hands-on |
| 68-80 | **Workshop: Your Reporting Candidates.** Each student identifies 2-3 recurring reports at their company that follow this pattern (data → analysis → deliverable). For each: what systems feed it, who builds it today, how long does it take, what would automation look like? | Workshop |
| 80-85 | **Where Does the Code Run?** Brief overview: three options for code execution — cloud LLM sandbox, your own containers, SQL-only. Our demo uses synthetic data in the cloud; production deployments keep data on-premise. This preview sets up Session 5. | Lecture |
| 85-90 | Homework | Wrap |

**Homework:** (1) Use the Meridian app to produce one complete deliverable of your choosing — a memo, a comparison, a risk assessment. Save or screenshot the output. Bring it to Session 5. (2) **Pre-reading for Session 5** (~35 min total): (a) Morgan Stanley case study (provided) — a regulated financial firm's deployment decision. Come prepared to discuss: what constraints did they face, what did they choose, and what surprised them? (b) [AIMultiple: "Cloud LLM vs Local LLMs"](https://aimultiple.com/cloud-llm) — the three deployment options and their tradeoffs. (c) "What Does Your AI Actually See?" (provided) — four approaches to data security when AI agents access enterprise data. A 5-minute read but the core concept for Session 5. (3) *Optional reading:* [a16z: "How 100 Enterprise CIOs Are Building and Buying Gen AI in 2025"](https://a16z.com/ai-enterprise-2025/) and [DUNNIXER: "6 AI Vendor Evaluation Dimensions for Enterprise RFPs"](https://www.dunnixer.com/insights/articles/the-six-dimensions-of-ai-vendor-evaluation-that-matter-most). Keep the DUNNIXER scorecard — it's the vendor evaluation tool you'll use in Session 5. (4) *Optional: Linux server Exercises 1-2 (hello-world agent and multi-system agent). Claude Code will help. Optional viewing: Demos 1-4.*

---

### SESSION 5: "What Does Deployment Look Like?"
**Monday, May 18 — Architecture, Data Security, and Build vs. Buy**

**Learning objectives:**
- Understand LLM deployment options and their tradeoffs (cloud API vs. on-premise)
- Grasp the data security problem: what the LLM sees and how to control it
- Evaluate build vs. buy vs. extend for AI capabilities

**Pre-reading assigned in Session 4 homework (~35 min required, plus optional):**
- Morgan Stanley case study — deployment decisions in regulated finance
- AIMultiple: "Cloud LLM vs Local LLMs" — the three deployment options and their tradeoffs
- "What Does Your AI Actually See?" — four data security approaches as a policy menu
- a16z: "How 100 Enterprise CIOs Are Building and Buying Gen AI in 2025" — landscape data (optional)
- DUNNIXER: "6 AI Vendor Evaluation Dimensions for Enterprise RFPs" — vendor scorecard (optional; used in-session)

Students arrive having read the deployment options, data security approaches, and a real case. Session time is discussion, demo, and application — not lecture.

**Session flow:**

| Min | Segment | Format |
|---|---|---|
| 0-8 | **Homework debrief.** Students share the deliverable they produced in the Meridian app. What looked right? What would you want to verify before sending to your board? Reinforce the maker/checker framework. | Discussion |
| 8-20 | **Case Study: Morgan Stanley.** Debrief the pre-reading. Morgan Stanley chose cloud API with a zero data retention agreement for 16,000 financial advisors under SEC/FINRA constraints. Key questions to the room: Was this the right call? The a16z survey says 90% of enterprises are testing third-party AI for customer support — does that match your experience? What would your company have done differently, and why? | Discussion |
| 20-25 | **Bridge.** "In Session 4 we asked: where does the code that queries your database run? Today: where does the *LLM that interprets those results* run? These are two separate decisions. You can run code on your servers and still send query results to the vendor's servers for interpretation. Or you can keep both local — but with a smaller model and lower quality. You read about the three options. Let's see the security problem in action." | Lecture |
| 25-33 | **Demo: Data Security in Action.** Ask the Meridian app for individual salary data — watch it return results. Then switch to a version with guardrails enabled: the same question is blocked or returns only aggregates. Pause: "This is the problem the four data security approaches address. Which approach did Morgan Stanley use?" | Live demo + discussion |
| 33-45 | **Discussion: Deployment Options and Data Security.** Quick poll: which deployment option fits your company? Which data security approach? What was the most surprising insight from the readings? What's the gap between where the a16z data says the market is heading and where your company actually is? Instructor clarifies and adds cost context as needed (cloud ~$0.01-0.05/query vs. on-premise $50-200K+ upfront). | Discussion |
| 45-58 | **Build vs. Buy: Applying the DUNNIXER Framework.** Walk through one specific vendor (Salesforce Agentforce) together — what it does today, what it costs, where it falls short. Score it on 2-3 of the DUNNIXER dimensions as a group exercise. Then: the real decision matrix — buy from incumbent (lowest risk), buy from AI-native startup (highest capability), build internally (highest control), or hybrid. Most enterprises land on hybrid. | Discussion + group exercise |
| 58-72 | **Breakout: Your Deployment Decisions (groups of 3-4).** For your identified use case: which LLM deployment option fits? Which data security approach? Build, buy, or hybrid? Use the DUNNIXER dimensions to justify your choice. Each group reports back: what constraints were common, and where did industry differences lead to different answers? | Breakout rooms |
| 72-85 | **Hands-on: Your Deployment Profile.** Each student writes down their deployment profile for their capstone use case: LLM deployment option, data security approach, build-vs-buy decision with rationale. Instructor circulates and advises. | Individual work |
| 85-90 | Preview: trust and verification | Wrap |

**Homework:** (1) For your identified use case: what governance requirements would your compliance team impose? Write down your top 3 concerns. (2) Think about who in your organization would need to approve an AI agent deployment — and what objections they'd raise. *Optional viewing: Demo 5 shows red-teaming an agent and adding guardrails.*

---

### SESSION 6: "Can You Trust It?"
**Wednesday, May 20 — Red-Teaming, Reliability, and Governance**

**Learning objectives:**
- Identify failure modes of AI agents (hallucination, wrong joins, misleading aggregations, overconfident document citations)
- Apply the maker/checker framework from Session 2 to enterprise data scenarios
- Understand data governance and regulatory requirements for AI agents

**Session flow:**

| Min | Segment | Format |
|---|---|---|
| 0-10 | **Homework debrief.** Students share their top governance concerns and the objections they anticipate from approvers. What patterns emerge across industries? | Discussion |
| 10-12 | **Bridge from Session 5.** "Last session you chose how to deploy — cloud, on-premise, hybrid. You picked a data security approach. But even with the right architecture, the agent can still get things wrong. Deployment decisions protect your data; verification protects your decisions." | Lecture |
| 12-28 | **Demo: When the Agent Gets It Wrong.** Three pre-prepared failures: (a) averages across won and lost deals without filtering — technically correct SQL, misleading answer; (b) cross-division revenue comparison with date format mismatch — Legacy CRM VARCHAR dates cause wrong aggregation; (c) customer count that double-counts due to fuzzy matching failures. Walk through each, show the SQL, identify the error. Key point: every one of these looks plausible. Without verification, any of them could end up in a board presentation. | Live demo |
| 28-38 | **Maker/Checker at Enterprise Scale.** Revisit the framework from Session 2, now with enterprise data context. The calibrated trust spectrum still applies, but the stakes and verification methods change. What to check for data agents: source system, filters, join logic, date ranges, NULL handling, row counts. The agent shows SQL for a reason — transparency is a feature. Who in your organization has the judgment to be an effective checker? Beyond individual verification: automated validation (row counts, range checks), dual-agent architectures (one agent queries, another verifies), and human-in-the-loop approval gates for high-stakes outputs. | Lecture + discussion |
| 38-55 | **Hands-on: Red-Team the Meridian App.** Students try to break the agent through the chat interface. Guided attack scenarios plus open exploration: (a) ask for data you shouldn't see (individual salaries by name), (b) ask a question where the data doesn't exist (2027 revenue), (c) try to trick it into hallucinating ("What was our revenue from the Atlantis division?"), (d) ask a question with a plausible but misleading framing ("Which division is most profitable?" without defining profit), (e) ask the same question twice and compare answers for consistency. Then 5 minutes of open red-teaming: try anything. | Hands-on |
| 55-60 | **Debrief: What Did You Find?** Quick share-out: what attacks worked? What surprised you? Any creative attacks beyond the guided list? | Discussion |
| 60-73 | **Data Governance and Regulatory Exposure.** Who is liable when the agent gives wrong financial data? Does agent output count as a "record" under SOX? GDPR implications of cross-system queries that combine PII from multiple sources. Role-based access control: the VP of Sales should not see HR compensation data, even if the agent can query both systems. Governance is not a technology problem — it's an organizational decision about acceptable risk, enforced through technical controls. | Lecture + Q&A |
| 73-85 | **Breakout: Your Governance Requirements (groups of 3-4).** Given your industry and regulatory environment, what guardrails would you require before deploying an AI agent? What's the minimum viable governance framework? Each group reports: what governance requirements were universal vs. industry-specific? Where would adoption stall without executive air cover? | Breakout rooms |
| 85-90 | Homework | Wrap |

**Homework:** (1) Read the Atherton Financial case study (provided). A wealth management firm deployed document AI and hit chunking, access control, and staleness failures. Come prepared to discuss: what would you have done differently? (2) Begin drafting your capstone strategy (template and evaluation rubric provided): problem statement, proposed solution, deployment approach, 90-day pilot plan. (3) For your identified use case: write down the three most likely failure modes and how you'd mitigate each. *Optional: Linux server Exercise 4 (red-teaming) directly applies to today's session. Optional viewing: Demo 5.*

---

### SESSION 7: "Document AI — Answers from Your Own Files"
**Wednesday, May 27 — Retrieval-Augmented Generation (RAG)**

**Learning objectives:**
- Understand how AI can answer questions grounded in company documents with citations
- Distinguish database AI (structured data queries) from document AI (unstructured text retrieval)
- Experience RAG hands-on and understand deployment decisions

**Session flow:**

| Min | Segment | Format |
|---|---|---|
| 0-10 | **Bridge + Atherton Case Debrief.** "You've learned to deploy agents (Session 5) and verify their output (Session 6). Both sessions focused on structured data — databases and SQL. But most company knowledge isn't in databases. It's in policies, contracts, emails, and slide decks. Today we add a second capability — and the Atherton case shows what can go wrong." Quick debrief: Atherton deployed document AI and hit chunking failures, access control gaps, and stale documents. What would you have done differently? | Lecture + discussion |
| 10-22 | **Demo: Document-Based Q&A.** Pre-loaded document collection for Meridian Corp: employee handbook, vendor contracts, compliance policies, board minutes. Ask: "What is our policy on remote work for the Energy Division?" "Which vendor contracts are up for renewal in Q2?" "What did the board approve regarding the Safety Division expansion?" Answers come with citations — page numbers and quoted passages. Then the combined question: "What's our contractual commitment to GE, and how does their actual spending compare?" — RAG for the contract, database agent for the spending. | Live demo |
| 22-32 | **How RAG Works.** The retrieval-augmented generation pipeline: (1) documents are chunked into passages, (2) an embedding model converts each chunk into a numerical vector, (3) chunks are stored in a vector database, (4) the user's question is embedded the same way and matched against stored chunks, (5) the top matches are sent to the LLM as context, (6) the LLM answers using only the retrieved context. Compare to database agents: RAG handles *unstructured* text; database agents handle *structured* data. Both are tools in the same toolkit. | Lecture |
| 32-52 | **Hands-on: Query the Document Collection.** Students ask questions of the Meridian document set. Three rounds: (1) Simple retrieval — "What are the safety training requirements?" "What's the PTO policy for the Energy Division?" (2) Cross-document — "How do the vendor contract terms for our top 3 suppliers compare?" (3) Cross-system — "Does our vendor contract with Acme align with what we're actually ordering from them?" (combining document AI with database queries). Students note which answers include citations and which don't. | Hands-on |
| 52-62 | **Reliability of Document AI.** RAG-specific failure modes: retrieval misses (the answer exists but wasn't retrieved), hallucinated citations (the AI cites a passage that doesn't say what it claims), context window limits, and stale documents. Live demo: ask a question where chunking split a relevant passage — show the partial answer and explain why. Verification protocol: always check the cited passage, not just the summary. The maker/checker framework applies to documents just as it does to data. | Lecture + demo |
| 62-75 | **Deploying RAG.** The deployment framework from Session 5 applies — we won't repeat it. What's new for document AI: **Document ingestion** — PDF parsing, chunking strategy (by section for policies, by clause for contracts — not one-size-fits-all), and freshness management. **Access control** — the RAG system must enforce the same document permissions as your file server. Atherton's oversharing problem is the cautionary tale. **Build-vs-buy for document AI:** turnkey RAG platforms (Glean, Guru, Microsoft Copilot for M365) handle ingestion and permissions out of the box but limit customization. Custom builds offer more control but require engineering resources. | Lecture + Q&A |
| 75-87 | **Breakout: Where Is Knowledge Trapped? (groups of 3-4).** What knowledge in your company is trapped in documents — policies, contracts, procedures, regulatory filings, past analyses? Each person names 2-3 document collections that would benefit from AI-powered Q&A. Compare: what types of documents came up repeatedly? What access control challenges are common? Each group reports: the most valuable document AI use case and the biggest deployment obstacle. | Breakout rooms |
| 87-90 | Capstone preview and homework | Wrap |

**Homework:** Finalize your strategy document (1-2 pages using the capstone template). Prepare a 5-minute presentation. The evaluation rubric is included with the template — use it to self-check before presenting. *Optional viewing: Demos 6-7 show building a RAG system and combining it with a database agent.*

---

### SESSION 8: "Your AI Strategy"
**Monday, June 1 — Capstone and Synthesis**

**Learning objectives:**
- Present a credible, scoped AI adoption strategy to peers
- Synthesize the personal productivity, enterprise data, and organizational dimensions
- Leave with concrete next steps for both personal use and organizational deployment

**Session flow (30 students):**

| Min | Segment | Format |
|---|---|---|
| 0-3 | **Setup.** You are presenting to your executive team. Your breakout group is your board of advisors. | Framing |
| 3-30 | **Breakout pitches.** 5 groups of 6. Each person gives a 2-minute pitch to their group, followed by 1 minute of quick feedback. Group then votes on the strongest strategy to represent them in the plenary. (Every student presents; 5 advance to the full class.) | Breakout rooms |
| 30-70 | **Plenary presentations.** 5 winning strategies presented to the full class (5 min each + 3 min Q&A/feedback). Instructor feedback on: is the pilot scoped tightly enough? Is the business case credible? Is the governance plan adequate? Does the Day 1 action actually happen on Day 1? | Presentations |
| 70-78 | **Synthesis: What You Now Know.** (1) AI is a personal productivity multiplier — charts, documents, analyses, automated workflows — available to you right now. (2) AI agents turn plain English into enterprise data answers — replacing dashboards, manual reports, and the wait for analyst time. (3) The technology is simpler than you expected (50 lines), but production requires governance, verification, and organizational readiness. (4) Document AI and database AI are complementary — together they cover structured and unstructured company knowledge. (5) The critical skill is not building AI tools — it's asking the right questions, iterating on output, and verifying the answers. The maker/checker mindset is the throughline. | Lecture |
| 78-86 | **Beyond Data: AI as Thinking Partner.** One final capability. Live demo: ask the Meridian app not "What were Q4 sales?" but "I'm considering expanding the Energy Division into the Southeast — based on our pipeline, customer concentration, and support ticket trends, what are the top 3 risks?" Watch the agent reason across multiple systems. Then push back: "You're assuming our supply chain can handle Southeast volume — what if it can't?" The agent adjusts its analysis. Key insight: AI will anchor on whatever framing you provide. The same data with different framing produces different recommendations. The human role is providing context, challenging assumptions, and deciding — not outsourcing judgment. | Live demo + discussion |
| 86-88 | **Monday Morning Actions.** Five things every participant can do regardless of role: (a) Use AI for your personal workflow — the tools from Sessions 1-2 are available now, no IT approval needed. (b) Audit your reporting workflows — which ones follow the data → analysis → deliverable pattern and could be automated? (c) Scope a 30-day discovery sprint on one data access use case. (d) Inventory the document collections that would benefit from AI-powered Q&A. (e) Establish an AI governance framework before shadow IT does it for you. | Lecture |
| 88-90 | Close. Resources for continued learning. Optional 30-day follow-up session to report on progress. | Wrap |

---

## Cross-Session Summary

| Session | Title | Primary Activity | Theme |
|---|---|---|---|
| 1 | What AI Can Do for You | Claude artifacts: charts, docs, calculators | Personal productivity |
| 2 | Iterate, Critique, Trust | Maker/checker framework + reusable workflows | Iteration and calibrated trust |
| 3 | AI Meets Your Data | Meridian app: single + cross-system queries | Enterprise data access |
| 4 | From Data to Deliverable | Full pipeline demo + agent loop + hands-on reporting | Reporting pipelines |
| 5 | What Does Deployment Look Like? | LLM deployment + data security + build vs. buy | Architecture and deployment |
| 6 | Can You Trust It? | Failure demos + red-teaming + governance | Reliability and compliance |
| 7 | Document AI | RAG demo + hands-on document Q&A + RAG deployment | Unstructured knowledge |
| 8 | Your AI Strategy | Capstone presentations + synthesis | Integration |

## Course Arc

- **Week 1 (Sessions 1-2): What AI Can Do for You** — Personal productivity with AI. Generate charts, documents, Excel analyses. Iterate and critique. The maker/checker mindset from day one.
- **Week 2 (Sessions 3-4): AI Meets Your Data** — Meridian Corp simulation and enterprise data. Cross-system queries, reporting pipelines, the agent loop.
- **Week 3 (Sessions 5-6): Deployment and Trust** — Architecture, data security, build vs. buy, red-teaming, governance.
- **Week 4 (Sessions 7-8): Document AI and Strategy** — RAG, capstone presentations.

## Recurring Elements

- **Maker/Checker Thread:** Introduced in Session 1 (preview), formalized in Session 2 (calibrated trust framework), applied in Session 4 (enterprise data verification), deepened in Session 6 (red-teaming and governance), extended in Session 7 (document AI verification). This is the throughline of the course.
- **Data Map → Capstone:** Students sketch their company's data landscape in Session 3 and build on it through the capstone strategy in Session 8.
- **Breakout Rooms:** Sessions 1, 2, 3, 5, 6, 7, 8. Sessions 3/5/6/7 use a "how does this work at your company?" format where students compare corporate realities and report patterns back to the group.
- **Hands-on:** Every session includes hands-on interaction — Claude.ai in Sessions 1-2, the Meridian app in Sessions 3-4 and 6-7, individual work in Sessions 5 and 8.
- **Linux Server:** Available throughout for self-paced exploration; live build demo in Session 4; exercises are optional homework.
- **Iteration Skills:** Introduced with Claude.ai in Session 1, formalized in Session 2 (self-critique, reusable prompts), applied to enterprise data in Sessions 3-4, applied to governance in Session 6.
- **Deployment Architecture Thread:** Code execution preview (Session 4), LLM deployment and data security (Session 5), RAG deployment (Session 7) — builds a complete picture of what production requires.
- **Case Studies:** Morgan Stanley AI Assistant (Session 5 — deployment decisions in regulated finance), Atherton Financial RAG deployment (Session 7 — document AI challenges). Each assigned as pre-reading and debriefed at the start of the paired session.
- **HPE Success Story:** Session 4 — Marie Myers / "Alfred" agent replacing 100-slide weekly review. Provides a real-world benchmark for automated reporting pipelines.

## Capstone Template (provided to students)

1. **The Problem:** What question can't be answered today? What's the business impact?
2. **The Solution:** Personal AI productivity, database AI, document AI, or a combination — which tools, systems, and document collections; build/buy/extend decision
3. **Deployment Approach:** Cloud vs. on-premise vs. hybrid; data security approach; for document AI, managed platform vs. custom build
4. **The 90-Day Pilot:** Team (who), data (which systems/documents), timeline (week-by-week), governance minimum
5. **Success Metrics:** Time-to-insight, decisions enabled, error reduction, adoption rate
6. **Risks and Mitigations:** Data quality, data security, regulatory requirements, AI reliability
7. **The Ask:** Budget, headcount, executive sponsor
8. **Day 1 Action:** The one thing you will do Monday morning

## Capstone Evaluation Rubric (shared with students in Session 6 homework)

| Dimension | Strong | Needs Work |
|---|---|---|
| **Pilot scope** | One use case, 1-3 systems, clear success metric | Too broad ("transform our data culture") or too vague |
| **Deployment approach** | Specific choice (cloud/on-premise/hybrid) with rationale tied to their industry | Generic or no justification |
| **Success metrics** | Measurable KPIs tied to business impact (e.g., "reduce forecast time from 3 days to 2 hours") | Vague ("improve efficiency") or no metrics |
| **Governance** | Minimum viable framework identified (access control, verification, audit) | Governance mentioned but not specific |
| **Risk mitigation** | Specific mitigations with clear owners, not just named risks | Risks listed without actionable mitigations |
| **Day 1 action** | Specific person, task, and date | Aspirational ("we should explore...") |

## Alignment with Advertised Outcomes

| Advertised Outcome | Where Covered |
|---|---|
| Use AI for personal productivity — charts, documents, analyses | Sessions 1-2 (Claude artifacts, iteration, reusable workflows) |
| Apply the maker/checker framework for AI verification | Sessions 1-2 (introduced and formalized), Sessions 4-7 (applied) |
| Analyze data and produce reports using AI agents | Sessions 3-4 (enterprise queries, reporting pipelines) |
| Connect AI to corporate databases | Session 4 (agent loop, code execution, database connections) |
| Build automated reporting pipelines | Session 4 (full pipeline, hands-on report building, HPE case) |
| Deploy document-based AI with citations | Session 7 (RAG implementation, hands-on, deployment) |
| Evaluate reliability, compliance, and governance | Session 6 (red-teaming, governance), Session 2 (calibrated trust) |
| Understand deployment and data security | Session 4 (code execution preview), Session 5 (LLM deployment, data security, build vs. buy), Session 7 (RAG deployment) |

## Supplementary Materials

### Pre-Session Readings

The following readings are assigned as homework before the indicated session. Total async reading load is approximately 90 minutes across the full program.

#### Before Session 3

- **Enterprise Systems Background Document** (provided) — What Salesforce, SAP, Workday, NetSuite, and other enterprise systems actually do. Why every company has 5-15 systems.

#### Before Session 5 (assigned in Session 4 homework)

Required (~35 min):

- **Morgan Stanley Case Study** (provided) — How a regulated financial firm deployed AI for 16,000 advisors under SEC/FINRA constraints. Cloud API with zero data retention agreement.
- **AIMultiple: "Cloud LLM vs Local LLMs"** — The three deployment options (cloud API, on-premise, hybrid) and their tradeoffs. Free at: [aimultiple.com/cloud-llm](https://aimultiple.com/cloud-llm)
- **"What Does Your AI Actually See?"** (provided) — Four approaches to data security when AI agents access enterprise data. A 5-minute read covering the core policy decision.

Optional (assigned Session 4, useful by Session 5):

- **a16z: "How 100 Enterprise CIOs Are Building and Buying Gen AI in 2025"** — Survey data on deployment trends and the shift from building to buying. Free at: [a16z.com/ai-enterprise-2025](https://a16z.com/ai-enterprise-2025/)
- **DUNNIXER: "6 AI Vendor Evaluation Dimensions for Enterprise RFPs"** — A practical scorecard framework for evaluating AI vendors. Keep this as a reference tool. Free at: [dunnixer.com](https://www.dunnixer.com/insights/articles/the-six-dimensions-of-ai-vendor-evaluation-that-matter-most)

#### Before Session 7 (assigned in Session 6 homework)

- **Atherton Financial Case Study** (provided) — A wealth management firm deployed document AI and hit chunking failures, access control gaps, and stale documents. Composite case based on real deployments.

### Case Studies

| Case Study | Session | Theme |
|---|---|---|
| Morgan Stanley AI Assistant | 5 | Deployment decisions in regulated finance |
| Atherton Financial (composite) | 7 | Document AI deployment challenges |

### Recorded Demo Videos

| Demo | Title | Runtime | Pairs With |
|---|---|---|---|
| 1 | Hello World Agent | 15 min | Session 4 |
| 2 | Adding a Second System | 15 min | Sessions 3-4 |
| 3 | Wrapping It in a Web App | 15 min | Session 4 |
| 4 | Building a Reporting Pipeline | 20 min | Session 4 |
| 5 | Red-Teaming Your Agent | 15 min | Session 6 |
| 6 | Building a RAG System | 20 min | Session 7 |
| 7 | Combining Database + Document AI | 15 min | Session 7 |
