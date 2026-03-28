# Case Study: Deloitte Australia — When Nobody Checks the AI's Work

*For use in Session 6: "Can You Trust It?" — Failure Modes, Verification, and Data Governance*

---

## The Story

In December 2024, Australia's Department of Employment and Workplace Relations awarded Deloitte a AU$439,000 contract to conduct an "independent assurance review" of its Targeted Compliance Framework — the controversial system the government uses to flag and penalize welfare recipients for missed appointments and reporting failures. The review was meant to be an authoritative, third-party assessment of whether the system was working fairly. It was, by design, a trust document: something a government minister could point to and say, "an independent expert looked at this."

Deloitte delivered a 237-page report, published in July 2025. It was dense, credentialed, and footnoted — exactly what you would expect from a Big Four consulting engagement. What nobody at Deloitte or the department caught before publication was that approximately 20 of those footnotes were fabricated. Twelve citations referred to a made-up report attributed to University of Sydney law professor Lisa Burton Crawford. Additional references pointed to a non-existent study by a Swedish academic at Lund University. Most striking was a direct quote attributed to Federal Court Justice Jennifer Davies from a ruling that never existed. The report had been generated using Microsoft Azure OpenAI (GPT-4o), a fact disclosed nowhere in the original document.

The errors were discovered not by Deloitte's quality assurance process, not by the government department that commissioned the work, but by Dr. Chris Rudge, a University of Sydney law researcher who recognized that the citations attributed to his colleague Professor Burton Crawford did not correspond to any real publication. Rudge alerted media, and the story broke in October 2025. Deloitte acknowledged the failures, refunded AU$97,000 — the final installment of the contract — and published a corrected version with an AI disclosure added after the fact. Critics, including several members of Parliament, argued that a partial refund was insufficient for a report whose fundamental credibility had been destroyed. The case became a global cautionary tale, covered by Fortune, The Register, and CFO Dive as a "wake-up call" for any firm using generative AI in professional deliverables.

---

## What Went Wrong

**Failure mode: AI hallucination in a high-stakes professional deliverable.** GPT-4o fabricated citations, invented academic publications, and generated a fake judicial quote — all presented as real evidence in a government-commissioned report. The hallucinations were not random noise; they were structurally plausible, which made them harder to catch on a casual read.

**The missing verification layer.** Deloitte's quality assurance processes failed at every stage. No one verified the citations against actual academic databases or court records. No one cross-checked the AI-generated references with the named authors. No one flagged that a Federal Court quote could not be traced to a real ruling. The report passed through whatever internal review Deloitte applied and was delivered to the government as finished work product. The firm itself admitted its QA processes failed.

**Undisclosed AI use compounded the damage.** The original report contained no mention that generative AI had been used in its production. When the fabrications surfaced, the missing disclosure turned a quality failure into a transparency crisis. The public learned simultaneously that the report contained invented evidence *and* that the tool responsible had been hidden from the client.

---

## The Governance Lesson

This case is the maker/checker framework at its starkest. AI was the maker — it drafted text, generated citations, and produced what looked like a rigorously sourced consulting report. But nobody was the checker. No human verified the AI's outputs against ground truth before the document left the building.

For executives deploying AI agents on enterprise data, the Deloitte case illustrates three principles. First, AI-generated content that *looks* authoritative is the most dangerous kind — hallucinated citations embedded in a 237-page report are far harder to catch than an obviously wrong number on a dashboard. Second, verification cannot be generic; it must target the specific failure modes of the tool being used, and fabricated references are a known, well-documented failure mode of large language models. Third, disclosure is not optional. When AI contributes to a deliverable, stakeholders need to know — not because AI is inherently untrustworthy, but because knowing the tool was used is what triggers the right verification questions. Deloitte's AU$97,000 refund and reputational damage were the cost of learning these lessons after delivery rather than before.

---

## Discussion Questions

1. **Accountability and contracts.** Deloitte refunded AU$97,000 of the AU$439,000 contract. Critics demanded a full refund. If your organization delivered an AI-assisted report to a client or regulator and fabricated content was later discovered, who would be accountable — the team that used the AI, the partner who signed off, or the firm? How would your current contracts and review processes handle this scenario?

2. **Verification design.** Citation fabrication is a known failure mode of large language models, yet Deloitte's QA process did not catch it. For AI-generated analysis in your organization — financial models, compliance reports, board materials — what specific verification steps would you build into the workflow? How do you verify the parts of AI output that are hardest to check (references, quotes, statistics)?

3. **Disclosure requirements.** Deloitte did not disclose AI use in the original report. Some organizations now require mandatory AI disclosure on all deliverables; others leave it to team discretion. What should your organization's policy be — and would you require the same disclosure from your vendors and consultants?

---

## Sources

- "Deloitte refunds Australian government nearly $290,000 after AI-generated report contained fabricated references." *Fortune*, October 7, 2025. [Link](https://fortune.com/2025/10/07/deloitte-ai-australia-government-report-hallucinations-technology-290000-refund/)
- "Law Professor Catches Deloitte Using Made-Up AI Hallucinations in Government Report." *Above the Law*, October 2025. [Link](https://abovethelaw.com/2025/10/law-professor-catches-deloitte-using-made-up-ai-hallucinations-in-government-report/)
- "Deloitte AI debacle seen as 'wake-up call' for corporate finance." *CFO Dive*, 2025. [Link](https://www.cfodive.com/news/deloitte-ai-debacle-seen-wake-up-call-corporate-finance/802674/)
- "Deloitte AI report for Australian government littered with hallucinations." *The Register*, October 6, 2025. [Link](https://www.theregister.com/2025/10/06/deloitte_ai_report_australia/)
