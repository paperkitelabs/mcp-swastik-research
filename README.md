# MCP Tool-Description Poisoning: Literature Review and Gap Analysis

This repository holds the literature-review work for a planned research paper (target: a Q1/Q2 journal or a top-tier conference) on **detecting and preventing tool-definition poisoning in Model Context Protocol (MCP) environments**.

Compiled on 7 October 2026. Each main document is provided as **Markdown (.md)** and **Word (.docx)**.

## Structure

| Folder / file | What it is |
|---|---|
| `00_Proposal/MCP_Security_Research_Proposal_original.docx` | The original research idea document |
| `01_Step1_Problem_Landscape/Step1_Problem_Landscape_and_Research_Direction` (.md / .docx) | **Step 1:** threat evidence (incidents, CVEs, standards), what the MCP spec provides today, what practitioners say is missing (ranked), what existing tools do, and the research directions derived from this |
| `01_Step1_Problem_Landscape/annex/` | Full working notes: 41 practitioner sources (GitHub/spec repo) and an industry landscape with a 30-row incident timeline and a 16-tool feature matrix |
| `02_Step2_Literature/Step2_Literature_Catalogue_Q1Q2_Journals_and_Top_Conferences` (.md / .docx) | **Step 2:** the citable literature, ordered **Q1/Q2 journals → A\*/A conferences → workshops**, plus an appendix of arXiv-only works that threaten novelty. Each entry gives the venue, quartile/rank, DOI or link, what the authors did, the gap, and which layer of our system it informs. Includes a **priority download list** of 35 papers. |
| `02_Step2_Literature/annex_detailed_area_reports/` | Detailed per-area reports (MCP-specific; attacks; defenses; supply chain; methodology; journal sweep; quartile and rank verification) |
| `03_Step3_Gap_Analysis/Step3_Gap_Analysis_and_Refined_Problem_Statement` (.md / .docx) | **Step 3:** coverage matrix, nine evidence-backed gaps, a critique of the original proposal, the **refined problem statement, revised RQs, hypotheses and contributions**, positioning against competitors, target venues, and a Step-4 verification checklist |

## Key findings in brief

1. **The broad "layered MCP security gateway" idea is already crowded.**
   - Peer-reviewed: ShieldMCP (ACL 2026 Industry) and Huang et al. (J. Cybersecurity & Privacy 2026).
   - Preprints: MCP-Guard, Jamshidi et al., and ETDI.
   - Hashing, signing, policy and sandboxing are **not** novel.
2. **The clearest open gap is change-awareness.** No academic work or product decides whether a *change* to a trusted tool definition is a legitimate update or a poisoning (rug pull).
3. **Practitioners rank this as their #1 missing capability.** Exact-hash pinning is reported to be noisy, and an independent measurement found 8–10.9% of public MCP endpoints changing their definitions within days.
4. **Existing detector evaluations are saturated and unrealistic.** They report up to 100% F1, use balanced synthetic data, test no adaptive attacker, and report no false-positive rate at realistic base rates.
5. **Only four MCP-specific Q1/Q2 journal papers exist, and none evaluates an implemented defense.** A Q1 journal is therefore a natural first target.

## Verification notes

- **How the search was done.** Direct access to Reddit, Hacker News, dblp, Crossref, ScienceDirect, IEEE Xplore and the SCImago/CORE pages was blocked in the research environment. Literature was identified through web-search results, and checked against publisher, proceedings and repository listings as they appeared in those results. Practitioner evidence comes from GitHub, which was readable.
- **What was checked.** Quartiles (SJR 2025) and CORE/ICORE2026 ranks were taken from scimagojr.com and portal.core.edu.au search snippets. These are marked ✔. Anything else is marked "~" or **UNVERIFIED**.
- **No paper, DOI or number was invented.** Where a detail was not seen, the documents say so.
- **Papers were assessed from abstracts and summaries, not full texts.** Step 3 §8 lists what to verify once the PDFs are downloaded.
