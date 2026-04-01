# XYZ Corp's Document AI Deployment: Three Governance Failures

*Pre-reading for Session 7 | Assigned as homework from Session 6*

> **Note:** This is a composite case based on patterns observed across real enterprise AI deployments. XYZ Corp is fictional.

---

## Background

XYZ Corp is a $500 million B2B industrial supplies distributor with three operating divisions — Industrial, Energy, and Safety — and a corporate headquarters that houses Legal, HR, Finance, and Compliance. Like most companies its size, XYZ Corp has accumulated a substantial body of internal documents: vendor contracts, compliance policies, employee handbooks, board meeting minutes, benefits guides, and safety protocols. These documents live across SharePoint, a contract management system, and several shared drives that no single person fully understands.

For years, when an employee had a question about a vendor contract or an HR policy, the process was the same: search SharePoint, fail to find what you need, and email Legal or HR. Legal's small team of three attorneys and a paralegal fielded roughly 80 of these requests per week — everything from "What's the termination clause in our Grainger contract?" to "Does our remote work policy cover the Houston office?" The average response time was two business days. During contract renewal season, it stretched to five.

In mid-2025, XYZ Corp's Chief Information Officer proposed a solution: deploy a document AI system that would let employees ask questions in plain English and receive answers with citations to specific document sections. The system would use retrieval-augmented generation (RAG) — the same architecture covered in this course. Documents would be parsed, split into chunks, embedded in a vector database, and retrieved when a user asked a question. A large language model would synthesize the retrieved passages into a coherent answer and cite the source document, section, and page number.

The project had strong executive sponsorship. The CIO pitched it as a way to "democratize access to institutional knowledge" and free Legal from answering routine questions. The CFO liked the projected time savings: 80 questions per week at two hours each, times an average fully loaded cost of $95 per hour for Legal staff, came to roughly $790,000 per year in recaptured capacity. The project was approved in August 2025 with a $150,000 budget and a 90-day timeline.

## The Deployment

The IT team selected a commercial RAG platform and began ingesting documents in September 2025. The corpus included approximately 1,200 documents: 340 active vendor contracts, 85 compliance and regulatory policies, the employee handbook (142 pages), board meeting minutes from the past three years, benefits enrollment guides, and safety certification records. Total volume was roughly 28,000 pages.

The platform's default settings were used for most configuration decisions. Documents were chunked into 512-token segments with 50-token overlap. A single vector index was created for the entire corpus. The system was connected to XYZ Corp's single sign-on (SSO) for authentication, meaning any employee with a company login could access it. The platform vendor provided a two-day onboarding session for the IT team and a one-page user guide for employees.

The system went live on November 3, 2025, announced via a company-wide email from the CIO titled "Ask Anything: Your New AI Research Assistant." Within the first week, usage was strong — over 400 queries. Legal reported an immediate drop in inbound emails. The project was considered a success.

Within 60 days, three failures surfaced that would put the project on hold and trigger a full governance review.

## Failure 1: The Missing Penalty

In December 2025, a procurement manager in the Energy Division was renegotiating XYZ Corp's contract with a major valve supplier. She asked the document AI system: "What are the termination provisions in the ValveTech Industries contract?"

The system returned a clear, well-formatted answer:

> *The ValveTech Industries Master Supply Agreement (Section 8.2) requires 90 days' written notice for termination without cause. The notice period begins on the first business day following receipt of written notification. See: ValveTech MSA, Section 8.2, page 14.*

The answer was accurate — Section 8.2 does specify a 90-day notice period. The procurement manager used this information in her negotiation planning and communicated to the ValveTech account team that XYZ Corp could exit the contract with 90 days' notice.

What the system did not return was Section 8.4, which appeared on page 16 of the same contract: an early termination penalty of 15% of the remaining contract value. On a contract with 18 months remaining and $2.4 million in committed spend, that penalty was $360,000. Section 8.4 had been split into a separate chunk during document processing. When the system retrieved passages relevant to "termination provisions," the chunk containing Section 8.2 (notice period) scored high in vector similarity. The chunk containing Section 8.4 (penalty calculation) scored lower — it used language about "liquidated damages" and "remaining commitment value" rather than the word "termination" — and fell below the retrieval threshold.

The procurement manager didn't know the answer was incomplete. The system presented it with a specific section citation and page number. It looked authoritative. It was authoritative — for the part it included. The gap was discovered only when ValveTech's legal team responded to the termination notice by citing Section 8.4 and invoicing the penalty. XYZ Corp ultimately renegotiated rather than terminated, but the episode cost three weeks of executive time and damaged the vendor relationship.

**What went wrong technically:** The default chunk size (512 tokens) split a multi-section termination clause across two chunks. The overlap window (50 tokens) was too small to bridge them. The retrieval step returned the top 3 most similar chunks, and the penalty clause ranked fourth. The system had no mechanism to detect that its answer covered only part of a multi-section topic, and no mechanism to warn the user that related content existed but fell below the retrieval threshold.

## Failure 2: The Oversharing Problem

In January 2026, a supply chain analyst in the Industrial Division asked the system: "What are the standard payment terms for our top 10 vendors?"

The system returned a summary of net-30 and net-45 payment terms from several vendor contracts — a reasonable answer. But appended to the response, under a heading "Related Context," the system also surfaced a passage from the October 2025 board meeting minutes:

> *The Compensation Committee approved a revised incentive structure tying 30% of executive bonuses to vendor cost reduction targets. The CEO's target for FY2026 is a 4% reduction in total vendor spend, with a maximum bonus payout of $340,000 against this metric...*

The analyst had asked about vendor payment terms. The system, performing semantic search across the entire document corpus, found that the board minutes discussing vendor cost reduction were semantically related to vendor payment terms. It retrieved the passage and included it in the response.

The analyst shared the response with two colleagues. Within a day, the executive compensation details were circulating informally in the Industrial Division. HR learned about the leak when a manager asked a pointed question about "whether the bonus structure creates a conflict of interest in vendor negotiations" during a town hall meeting.

**What went wrong technically:** The system was deployed with a single permissions level. Every authenticated user could query every document in the corpus. No one had classified the documents by sensitivity or mapped them to access tiers. Board meeting minutes — containing executive compensation data, strategic plans, M&A discussions, and personnel matters — sat in the same index as the employee handbook and vendor contracts. The deployment team consisted of IT staff and one attorney from Legal. HR was not consulted. No one reviewed the corpus to identify documents that should be restricted by role or department.

## Failure 3: The Stale Policy

XYZ Corp updated its remote work policy effective January 15, 2026, increasing the in-office requirement from two days per week to three. The updated policy was approved by the executive team in December 2025, communicated via an all-hands meeting on January 10, and posted to the HR section of the company intranet on January 15.

No one notified the IT team to re-index the document corpus.

For the next two months, employees who asked the document AI system about the remote work policy received the old version — the one requiring only two days in office. The system cited the Employee Handbook, Section 4.3, and returned the outdated text with confidence. There was no version indicator, no date stamp in the response, and no flag that a newer version might exist.

Two new hires who joined in February 2026 — one in the Safety Division (Houston) and one in Corporate Finance (headquarters) — asked the system about remote work flexibility as part of their onboarding research. Both received the outdated two-day policy. The Houston hire, who had negotiated a relocation package based partly on the expectation of a two-day in-office schedule, was told during his second week that the policy was actually three days. The resulting conversation involved HR, his hiring manager, and eventually the division VP.

**What went wrong technically:** The document AI system had no automated refresh mechanism. The initial document ingestion was a one-time batch process. The deployment plan did not include a procedure for updating the index when documents changed, did not assign ownership for keeping the corpus current, and did not establish a refresh cadence. The old version of the policy remained in the vector database because no one removed it or replaced it. The system had no way to know that a newer version existed on the intranet, because the intranet and the document AI system were not connected.

## What Went Wrong: Root Causes

The three failures appear different on the surface — a retrieval gap, an access control violation, a stale document. But they share common root causes that apply to any AI system deployed on enterprise data, not just document AI.

**No governance framework before deployment.** The project moved from approval to production in 90 days with no governance review. There was no data classification step, no access control design, no document lifecycle plan, no testing protocol that simulated realistic failure scenarios. The team optimized for speed to launch.

**Default configurations treated as sufficient.** The 512-token chunk size, the single-index architecture, the absence of role-based access — these were all default settings on the platform. The deployment team did not evaluate whether the defaults were appropriate for XYZ Corp's specific document corpus, which included long-form legal contracts and sensitive board materials.

**No cross-functional input.** The project was owned by IT with light involvement from Legal. HR, Compliance, and Procurement were not consulted. Each of the three failures would likely have been identified if the affected department had reviewed the deployment plan. HR would have flagged the board minutes. Procurement would have tested contract questions. HR would have asked about the document update process.

**No ongoing operations plan.** The deployment was treated as a project with a launch date, not a system with an operating lifecycle. There was no monitoring of answer quality, no process for document updates, no feedback mechanism for users to flag incorrect answers, and no periodic review of what the system was surfacing.

**Misplaced trust in citations.** The system's ability to cite specific sections and page numbers created an illusion of completeness. Users reasonably assumed that a cited answer was a thorough answer. The citations were accurate for the content retrieved — but accuracy and completeness are different things, and the system provided no signal about the latter.

## Discussion Questions

1. **Prioritizing the failures.** Which of the three failures do you consider most dangerous to the organization, and why? Consider both the immediate impact and the precedent each failure sets if left unaddressed.

2. **Pre-deployment governance.** If you had been asked to review the deployment plan before launch, what specific gates or checkpoints would you have required? Who would need to be in the room, and what questions would they need to answer before the system went live?

3. **The completeness problem.** The chunking failure produced an answer that was accurate but incomplete — arguably more dangerous than an obviously wrong answer. How would you design a system or process to detect when an AI answer might be missing critical context? Is this a technical problem, a process problem, or both?

4. **Beyond document AI.** Each of these failures — incomplete retrieval, access control gaps, stale data — can occur in any AI system that queries enterprise data (including the database agents we have built in this course). For the XYZ Corp data assistant you have been using, identify one scenario where each failure type could occur. What governance controls would prevent it?

5. **The 90-day timeline.** The project was approved with a 90-day timeline and $150,000 budget. Assume the governance review now adds 30 days and $40,000. How would you make the case to the CFO that the additional investment is justified? What is the cost of *not* doing it?
