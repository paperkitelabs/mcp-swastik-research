# Step 2: Literature Catalogue (Q1/Q2 journals first, then top-tier conferences)

**Project:** MCP Tool-Description Poisoning: Detection and Prevention
**Compiled:** 7 October 2026
**Search lens (from Step 1):** primary lens is Direction A (change-aware trust: legitimate vs poisoned tool-definition updates). Supporting lenses are B (whole-metadata surface) and C (declared vs observed runtime behaviour).

---

## 0. How to use this catalogue

### 0.1 Tiers

| Tier | What it contains | Count |
|---|---|---|
| **Tier 1** | Peer-reviewed **journals**, Q1/Q2 (SJR) | 52 |
| **Tier 2** | **Top conferences**, CORE A*/A | 75 |
| **Tier 3** | Workshops and lower-ranked venues (cite for priority/seminal value only) | 13 |
| **Appendix A** | arXiv-only preprints that **threaten novelty**. You do not need to cite them heavily, but you **must read them** before claiming anything new. | 30 |

Totals are approximate.

### 0.2 Entry fields

Every entry gives:
- title, authors (where seen), venue, year, DOI or official link;
- a short summary of **what they did**;
- the **gap or limitation** relevant to us;
- **which layer of our system** it informs: INT = integrity/pinning/signing, SEM = semantic/NLP detection, DRIFT = version-to-version change analysis, POL = capability policy, RT = runtime monitoring, RISK = fusion/thresholds, DATA = dataset/benchmark, EVAL = evaluation methodology, TM = threat model/motivation.

### 0.3 Verification legend

- **Rank ✔**: the SJR 2025 quartile or CORE/ICORE2026 rank was seen in a scimagojr.com or portal.core.edu.au search snippet (see §1).
- **Rank ~**: from an aggregator (JCR via journalmetrics.org) or general knowledge. **Verify before submission.**
- **Bib ✔ / Bib ~**: bibliographic details seen on a publisher/indexer page, or only in a citing paper or repository.
- Anything not seen is marked **UNVERIFIED**.

The search used web-search snippets because direct access to scholarly databases (dblp, Crossref, ScienceDirect, IEEE Xplore full pages) was blocked in this environment. **No paper was invented.** Where a DOI was not seen, a publisher URL, PII or arXiv ID is given so that you can locate the paper.

### 0.4 What to download first

See **§6 "Priority download list"**: about 35 papers you should read in full before Step 4 (deep reading).

---

## 1. Venue-quality reference table (checked 2026-10-07)

### 1.1 Journals (SJR 2025 best quartile unless noted)

| Journal | Quartile | Check |
|---|---|---|
| ACM Computing Surveys (CSUR) | Q1 (SJR 5.985) | ✔ |
| Information Fusion | Q1 (4.197) | ✔ |
| IEEE Trans. Information Forensics & Security (TIFS) | Q1 (2.193) | ✔ |
| ACM Trans. Intelligent Systems & Technology (TIST) | Q1 (2.065) | ✔ |
| Expert Systems with Applications (ESWA) | Q1 (1.939) | ✔ |
| IEEE Trans. Dependable & Secure Computing (TDSC) | Q1 (1.758) | ✔ |
| Knowledge-Based Systems | Q1 (1.753) | ✔ |
| J. Network & Computer Applications (JNCA) | Q1 (1.704) | ✔ |
| Computers & Security | Q1 (1.598); JCR 2024 IF 5.4 (aggregator) | ✔ |
| ACM TOSEM | Q1 (1.590) | ✔ |
| IEEE Trans. Software Engineering (TSE) | Q1 (1.568) | ✔ |
| Communications of the ACM | Q1 (1.540) | ✔ |
| Neurocomputing | Q1 (1.465) | ✔ |
| Applied Soft Computing | Q1 (1.456) | ✔ |
| ACM TKDD | Q1 (1.317) | ✔ |
| Computer Networks | Q1 (1.144) | ✔ |
| Cybersecurity (SpringerOpen) | Q1 (1.056) | ✔ |
| ICT Express | Q1 (0.977) | ✔ |
| J. Information Security & Applications (JISA) | Q1 (0.905) | ✔ |
| IEEE Access | Q1 (0.884), mega-journal | ✔ |
| ACM TOPS (formerly TISSEC) | Q1 (0.783) | ✔ |
| IEEE Security & Privacy (magazine) | Q1 (0.643) | ✔ |
| Information Sciences | JCR 2025 Q1 (IF 6.8) | ~ |
| Neural Networks | JCR 2025 Q1 (IF 6.3) | ~ |
| Artificial Intelligence Review | JCR 2025 Q1 (IF 13.9) | ~ |
| International Journal of Information Security (Springer) | JCR 2025 **Q2** (IF 3.2) | ~ |
| IEEE Software | **Q2** (0.627) | ✔ |
| Computers, Materials & Continua | **Q2** (0.513) | ✔ |
| Electronics (MDPI) | Q2 | ✔ |
| Future Internet (MDPI) | Q2 (2024) | ~ |
| Journal of Cybersecurity and Privacy (MDPI) | Q1/Q2 by OpenAlex subfield (journalmetrics); **SJR not seen** | ~ |
| Information (MDPI), Applied Sciences (MDPI) | not retrieved (commonly Q2) | ~ |
| High-Confidence Computing | not retrieved | ~ |
| Int. J. Network Dynamics & Intelligence (IJNDI) | SJR shows Q1 (3.327), **anomalously high for a 2022 journal; verify** | ~ |

### 1.2 Conferences (CORE / ICORE2026 unless noted; all ✔ via portal.core.edu.au snippets)

- **A\*:** IEEE S&P, USENIX Security, ACM CCS (CORE2023), NDSS, ICSE, FSE, ASE, ICML, NeurIPS, ICLR, ACL, EMNLP, AAAI, IJCAI, WWW, KDD.
- **A:** IEEE EuroS&P, AsiaCCS, ACSAC, RAID, ESORICS, ISSTA, MSR, NAACL, HotOS.
- **B:** DIMVA, COMPSAC.
- **C:** AIES.
- **Unranked / not found:** ACM SAC (multiconference), AISec, CAMLIS, SCORED, SPW.
- **Note:** *Findings of ACL/NAACL* and *Industry Track* papers carry the parent conference's name but are usually weighted below main-track papers. *NeurIPS Datasets & Benchmarks* is part of the main NeurIPS proceedings.

---

# TIER 1: PEER-REVIEWED JOURNALS (Q1/Q2)

## 2.1 MCP-specific journal papers (the most important group; only four exist)

### J-01. Model Context Protocol (MCP): Landscape, Security Threats, and Future Research Directions
- **Authors:** Xinyi Hou, Yanjie Zhao, Shenao Wang, Haoyu Wang (HUST)
- **Venue:** ACM TOSEM. Accepted Feb 2026; shown in the issue-in-progress for Vol. 35, Issue 10 (Oct 2026). Also listed in the FSE 2026 Journal-First track.
- **Quality:** Q1 ✔ | Bib ✔ (ACM DL page via search)
- **Link:** https://doi.org/10.1145/3796519 | arXiv 2503.23278 | code: github.com/security-pride/MCP_Landscape
- **What they did:**
  - Defines the MCP server lifecycle: 4 phases (creation, deployment, operation, maintenance) and 16 activities.
  - Builds a threat taxonomy of 4 attacker types (malicious developers, external attackers, malicious users, security flaws) and 16 threat scenarios. These include tool poisoning, rug pull and name collision.
  - Gives real-world case studies and per-phase safeguards.
- **Gap:** A landscape/position paper with **no detector, no gateway and no quantitative evaluation**. It calls for work on vetting, versioning/integrity and runtime controls.
- **Use for us:** TM. The canonical **journal** taxonomy. Map each of our layers to its lifecycle phases: integrity at install/update, detector at registration, runtime monitor at operation.

### J-02. Bridging AI and Software Security: A Comparative Vulnerability Assessment of LLM Agent Deployment Paradigms
- **Authors:** Tarek Gasmi, Ramzi Guesmi, Ines Belhadj, Jihene Bennaceur
- **Venue:** Information Sciences (Elsevier), 2026. The journal is inferred from ScienceDirect PII S0020025526001623 (ISSN 0020-0255) plus an exact title match. Vol/DOI UNVERIFIED.
- **Quality:** JCR Q1 ~ | Bib ~
- **Link:** https://www.sciencedirect.com/science/article/abs/pii/S0020025526001623 | arXiv 2507.06323
- **What they did:**
  - Compares Function Calling vs MCP deployment paradigms on **3,250 attack scenarios across 7 LLMs**.
  - Attacks: prompt injection, JSON injection, DoS, function-name and parameter attacks.
  - Attack success was 73.5% for Function Calling vs 62.59% for MCP. MCP shows more LLM-centric exposure. Chained attacks reached 91–96%.
  - Advanced reasoning models were *more* exploitable despite better threat detection.
- **Gap:** An attack study only; no defense evaluated.
- **Use for us:** TM/EVAL. A Q1 empirical baseline showing MCP needs dedicated defenses.

### J-03. From Prompt Injections to Protocol Exploits: Threats in LLM-Powered AI Agents Workflows
- **Authors:** Mohamed Amine Ferrag, Norbert Tihanyi, Djallel Hamouda, Leandros Maglaras, Abderrahmane Lakas (absent from some citations), Merouane Debbah
- **Venue:** ICT Express (Elsevier/KICS), 2025 (accepted/in press). Vol/DOI UNVERIFIED.
- **Quality:** Q1 ✔ | Bib ~
- **Link:** https://www.sciencedirect.com/science/article/pii/S2405959525001997 | arXiv 2506.23260
- **What they did:**
  - Builds an end-to-end threat model for LLM-agent ecosystems covering host↔tool and agent↔agent communication.
  - Catalogues 30+ attack techniques in 4 domains: Input Manipulation, Model Compromise, System & Privacy, and **Protocol Vulnerabilities (MCP, ACP, ANP, A2A)**.
  - Includes the GitHub MCP "Toxic Agent Flow" case.
- **Gap:** A taxonomy only; calls for protocol-level defenses.
- **Use for us:** TM. A journal source that explicitly places MCP tool poisoning in a protocol-layer taxonomy.

### J-04. Model Context Protocol Threat Modeling and Analysis of Vulnerabilities to Prompt Injection with Tool Poisoning
- **Authors:** Charoes Huang, Xin Huang, Ngoc Phu Tran, Amin Milani Fard (NYIT Vancouver)
- **Venue:** Journal of Cybersecurity and Privacy (MDPI) 6(3), Art. 84, published 5 May 2026
- **Quality:** SJR not seen; Q1/Q2 by OpenAlex subfield ~ | Bib ✔ (MDPI page via search)
- **Link:** https://doi.org/10.3390/jcp6030084 | arXiv 2603.22489
- **What they did:**
  - STRIDE + DREAD analysis giving **57 threats across 6 MCP components** (host, client, LLM, server, data stores, authorization server).
  - **Tests 7 MCP clients against 4 tool-poisoning attacks:** attack success from 0% (Claude Desktop) to 100% (Cursor).
  - *Proposes* layered defenses: static metadata analysis, decision-path tracking, behavioural anomaly detection, user transparency.
- **Gap:** As far as the abstract shows, the defenses are **proposed, not implemented or evaluated** (no P/R/F1, no labelled dataset, no integrity/drift layer). The authors state that client-side weaknesses were under-studied.
- **Use for us:** TM/EVAL. **The closest journal paper to our proposal.** Our differentiator is an implemented, evaluated gateway with drift analysis on a labelled version-pair corpus. **Read in full first.**

## 2.2 Surveys of LLM-agent security and prompt injection (journal anchors for Related Work)

| ID | Title | Authors | Venue | Quality | Link | What it covers | Gap relevant to us | Layer |
|---|---|---|---|---|---|---|---|---|
| J-05 | The Emerged Security and Privacy of LLM Agent: A Survey with Case Studies | F. He, T. Zhu, D. Ye, B. Liu, W. Zhou, P.S. Yu | ACM CSUR 58(6):162, 2025 | Q1 ✔ / Bib ✔ | https://doi.org/10.1145/3773080 | Threats inherited from LLMs vs agent-specific threats, incl. tool manipulation; defenses; "virtual town" case study | No MCP-specific treatment; defenses lag capabilities | TM |
| J-06 | AI Agents Under Threat: A Survey of Key Security Challenges and Future Pathways | Z. Deng, Y. Guo, et al. | ACM CSUR 57(7):182, 2025 | Q1 ✔ / Bib ✔ | https://doi.org/10.1145/3716628 | 4 knowledge gaps, incl. **interactions with untrusted external entities** | Coverage ends Apr 2024 (pre-MCP); untrusted tools named as an open gap | TM |
| J-07 | Unique Security and Privacy Threats of Large Language Models: A Comprehensive Survey | S. Wang, T. Zhu, et al. | ACM CSUR 58(4):83, 2025 | Q1 ✔ / Bib ✔ | https://doi.org/10.1145/3764113 | Scenario taxonomy: pre-training, fine-tuning, deployment, agents | Tool coverage is one section | TM |
| J-08 | Security and Privacy Challenges of Large Language Models: A Survey | B.C. Das, M.H. Amini, Y. Wu | ACM CSUR 57(6), 2025 | Q1 ✔ / Bib ~ (DOI not seen) | arXiv 2402.00888 | General LLM security/privacy | Background only | TM |
| J-09 | A Comparative Survey of Security Risks in AI Systems: From LLMs to AI Agents and Embodied Agents | B. Wu, Q. Li, C. Zhou, T. Wang, S. Ji | ACM CSUR 58(15):392, 2026 | Q1 ✔ / Bib ~ | DOI likely 10.1145/3837083 (UNVERIFIED) | Risk comparison across system types | Positioning | TM |
| J-10 | Security of LLM-based Agents regarding Attacks, Defenses, and Applications: A Comprehensive Survey | Y. Tang, Y. Liu, J. Lan, Z. Yan, E. Gelenbe (authors from citing refs) | Information Fusion, 2025, art. 103941 | Q1 ✔ / Bib ~ | https://doi.org/10.1016/j.inffus.2025.103941 | Attacks (incl. **unsafe tool use**) and defenses taxonomy | MCP content unknown | TM |
| J-11 | Attack and Defense Techniques in Large Language Models: A Survey and New Perspectives | Z. Liao et al. | Neural Networks, 2025 (from PII) | JCR Q1 ~ / Bib ~ | sciencedirect.com/science/article/abs/pii/S0893608025012699; arXiv 2505.00976 | Prevention- vs detection-based defenses | Calls for **standardized evaluation** and adaptive defenses | TM, EVAL |
| J-12 | Security Concerns for Large Language Models: A Survey | M.Q. Li, B.C.M. Fung | JISA 95:104284, 2025 | Q1 ✔ / Bib ✔ | sciencedirect.com/science/article/abs/pii/S2214212625003217 | Injection, poisoning, agent risks | Says existing taxonomies are "conceptually muddled" (technique vs objective), so define tool poisoning precisely | TM |
| J-13 | Safeguarding Large Language Models: A Survey | Y. Dong, R. Mu, et al. | Artificial Intelligence Review 58(12):382, 2025 | JCR Q1 ~ / Bib ~ | PMC12532640; arXiv 2406.02622 | Guardrail mechanisms (Llama Guard, NeMo, Guardrails AI) | **Input/output-centric, not tool-metadata-centric** | SEM, RISK |
| J-14 | LLM Agents Security Duality: A Comprehensive Survey of Self-Security and Empowered Cybersecurity | Y. Xu, …, H. Hu | Artificial Intelligence Review 59:174, 2026 | JCR Q1 ~ / Bib ✔ | https://doi.org/10.1007/s10462-026-11563-0 | Internal and external attack surfaces of agents; tool use widens the surface | Survey | TM |
| J-15 | When LLMs Meet Cybersecurity: A Systematic Literature Review | J. Zhang, H. Bu, …, D. Meng | Cybersecurity 8(1), 2025 | Q1 ✔ / Bib ✔ | https://doi.org/10.1186/s42400-025-00361-w | 300+ works; jailbreak and injection section | Not tool-focused | TM |
| J-16 | A Survey on LLM Security and Privacy: The Good, the Bad, and the Ugly | Y. Yao, J. Duan, K. Xu, Y. Cai, Z. Sun, Y. Zhang | High-Confidence Computing 4(2):100211, 2024 | ~ / Bib ✔ | https://doi.org/10.1016/j.hcc.2024.100211 | Highly cited overview | Background | TM |
| J-17 | A Domain-Based Taxonomy of Jailbreak Vulnerabilities in LLMs | C. Peláez-González, …, F. Herrera | Neurocomputing 683:133534, 2026 | Q1 ✔ / Bib ✔ | https://doi.org/10.1016/j.neucom.2026.133534 | Classifies attacks by the **alignment weakness exploited** | Template for a poisoning taxonomy by exploited weakness | TM, DATA |
| J-18 | Prompt Injection Attacks in LLMs and AI Agent Systems: A Comprehensive Review of Vulnerabilities, Attack Vectors, and Defense Mechanisms | S. Gulyamov + 6 | Information (MDPI) 17(1):54, 2026 | ~Q2 / Bib ~ | https://doi.org/10.3390/info17010054 | Names **MCP tool poisoning** explicitly; OWASP-based mitigations | Narrative review; inconsistent source counts | TM |
| J-19 | Prompt Injection Attacks on LLMs: A Survey of Attack Methods, Root Causes, and Defense Strategies | T. Geng, Z. Xu, Y. Qu, W.E. Wong | Computers, Materials & Continua 87(1):4, 2026 | Q2 ✔ / Bib ✔ | https://doi.org/10.32604/cmc.2025.074081 | SLR of 128 studies; input-preprocessing defenses reach 60–80% detection | **Gaps against novel attack vectors** (supports unseen-pattern RQ) | TM, EVAL |

## 2.3 Detection-oriented journal papers (baselines)

| ID | Title | Authors | Venue | Quality | Link | What they did | Gap / note | Layer |
|---|---|---|---|---|---|---|---|---|
| J-20 | JailGuard: A Universal Detection Framework for Prompt-based Attacks on LLM Systems | X. Zhang et al. (XJTU, NTU) | ACM TOSEM, 2025 | Q1 ✔ / Bib ✔ | https://doi.org/10.1145/3724393 | Mutates inputs (18 mutators) and measures response divergence; 11k-sample dataset, 15 attack types; 86.14% text accuracy | Model-specific tuning; may fail on unseen attacks; multiple queries per input. **Divergence idea is analogous to drift**, but on prompts, not metadata | SEM, DRIFT |
| J-21 | Enhancing Security in LLM Applications: A Performance Evaluation of Early Detection Systems | V. Gakh, H. Bahsi | Int. J. Information Security, 2026 | JCR Q2 ~ / Bib ✔ | https://doi.org/10.1007/s10207-026-01338-7 | Benchmarks **LLM Guard, Vigil, Rebuff** on prompt-leak attacks | Prompts only. **Use these tools as off-the-shelf baselines on tool descriptions** | SEM, EVAL |
| J-22 | Comparative Evaluation of Machine Learning Methods for Protecting LLMs from Prompt Injection Attacks | Dzhaliuk, Sabodashko, Khoma, et al. | Int. J. Information Security 25:109, 2026 | JCR Q2 ~ / Bib ~ | https://doi.org/10.1007/s10207-026-01264-8 | Compares classical ML classifiers for injection detection | Details UNVERIFIED; likely the journal citation for **TF-IDF+LR-style baselines** | SEM |
| J-23 | Prompt Injection Detection in LLM Integrated Applications | Lan, Kaul, Jones | Int. J. Network Dynamics & Intelligence 4(2), 2025 | ~ (verify) / Bib ~ | https://doi.org/10.53941/ijndi.2025.100013 | Banned-terms list + similarity search + BERT classifier | **Structurally close to our layer 2.** Venue quality uncertain; cite as related work, not as an anchor | SEM |

## 2.4 Supply-chain, integrity and app-ecosystem journal anchors

| ID | Title | Authors | Venue | Quality | Link | What they did | Gap / transfer to MCP | Layer |
|---|---|---|---|---|---|---|---|---|
| J-24 | Research Directions in Software Supply Chain Security | L. Williams, …, W. Enck (15 authors) | ACM TOSEM 34(5), 2025, pp. 1–38 | Q1 ✔ / Bib ~ | https://doi.org/10.1145/3714464 | Research agenda: tainted dependencies, compromised builds, attacks on humans; integrity, provenance, signing | **Strongest Q1 anchor for "MCP servers are supply-chain artifacts"**. No NL-metadata vector | TM, INT |
| J-25 | Large Language Model Supply Chain: A Research Agenda | S. Wang, Y. Zhao, X. Hou, H. Wang | ACM TOSEM, 2025 | Q1 ✔ / Bib ✔ | https://doi.org/10.1145/3708531 | 3-layer LLM supply chain incl. **downstream application ecosystem** | Vision paper | TM |
| J-26 | LLM App Store Analysis: A Vision and Roadmap | Y. Zhao, X. Hou, S. Wang, H. Wang | ACM TOSEM 34(5):125, 2025 | Q1 ✔ / Bib ✔ (J1 agent; the J2 agent saw only a workshop header, so verify) | https://doi.org/10.1145/3708530 | Agenda for app-store mining, security risk identification | Vision only | TM |
| J-27 | Killing Two Birds with One Stone: Malicious Package Detection in NPM and PyPI using a Single Model of Malicious Behavior Sequence (Cerebro) | J. Zhang et al. (Fudan) | ACM TOSEM (2024/25) | Q1 ✔ / Bib ~ | https://doi.org/10.1145/3705304 | Behaviour-sequence abstraction plus fine-tuned BERT across ecosystems; +10% precision | Code, not NL. **Supports a transformer classifier and cross-family generalisation tests** | SEM, EVAL |
| J-28 | Software Supply Chain: A Taxonomy of Attacks, Mitigations and Risk Assessment Strategies | B. Gokkaya, L. Aniello, B. Halak | JISA vol. 97, 2026 | Q1 ✔ / Bib ~ | arXiv 2305.14157 (journal DOI UNVERIFIED) | SLR of 96 papers: 19 attacks, 25 controls, a risk-assessment method | Control catalogue lacks semantic-metadata controls; **risk method informs RISK** | TM, RISK |
| J-29 | Journey to the Center of Software Supply Chain Attacks | P. Ladisa, S.E. Ponta, A. Sabetta, M. Martinez, O. Barais | IEEE Security & Privacy (magazine), 2023 | Q1 ✔ / Bib ✔ | https://doi.org/10.1109/MSEC.2023.3302066 | Practitioner version of the SoK taxonomy; Risk Explorer tool | Code artifacts only | TM |
| J-30 | Reproducible Builds: Increasing the Integrity of Software Supply Chains | C. Lamb, S. Zacchiroli | IEEE Software 39(2):62–70, 2022 | **Q2** ✔ / Bib ✔ | https://doi.org/10.1109/MS.2021.3073045 | Independent re-derivation for integrity | Motivates **canonicalising tool JSON before hashing** | INT |

## 2.5 Methodology journals (evaluation rigour, anomaly detection, fusion)

| ID | Title | Authors | Venue | Quality | Link | Why we cite it | Layer |
|---|---|---|---|---|---|---|---|
| J-31 | Pitfalls in Machine Learning for Computer Security | D. Arp, E. Quiring, F. Pendlebury, A. Warnecke, F. Pierazzi, C. Wressnegger, L. Cavallaro, K. Rieck | Communications of the ACM 67(11):104–112, 2024 | Q1 ✔ / Bib ✔ | https://doi.org/10.1145/3643456 | Journal version of the 10-pitfalls checklist (sampling bias, data snooping, base rate, lab-only evaluation). **Reviewers will apply it to us** | EVAL |
| J-32 | The Base-Rate Fallacy and the Difficulty of Intrusion Detection | S. Axelsson | ACM TISSEC (now TOPS) 3(3):186–205, 2000 | Q1 ✔ / Bib ✔ | https://doi.org/10.1145/357830.357849 | When malicious tools are rare, FPR dominates. **Report precision at 1:100 and 1:1000 prevalence** | EVAL, RISK |
| J-33 | Deep Learning based Vulnerability Detection: Are We There Yet? | S. Chakraborty, R. Krishna, Y. Ding, B. Ray | IEEE TSE, 2021/22 | Q1 ✔ / Bib ~ (vol/DOI UNVERIFIED) | arXiv 2009.07235 | Duplication leakage, unrealistic balance and artefact learning cause >50% performance drop in realistic settings | EVAL, DATA |
| J-34 | Adversarial Attacks on Deep-learning Models in NLP: A Survey | W.E. Zhang, Q.Z. Sheng, A. Alhazmi, C. Li | ACM TIST 11(3):24, 2020 | Q1 ✔ / Bib ✔ (DOI not seen) | arXiv 1901.06796 | Journal anchor for the **paraphrase-evasion threat model** | SEM, EVAL |
| J-35 | A Survey of Adversarial Defenses and Robustness in NLP | S. Goyal, S. Doddapaneni, M.M. Khapra, B. Ravindran | ACM CSUR, 2023 | Q1 ✔ / Bib ✔ | https://doi.org/10.1145/3593042 | Robustness metrics and defenses (adversarial training) | SEM |
| J-36 | Isolation-Based Anomaly Detection | F.T. Liu, K.M. Ting, Z.-H. Zhou | ACM TKDD 6(1):3, 2012 | Q1 ✔ / Bib ✔ | https://doi.org/10.1145/2133360.2133363 | Journal citation for Isolation Forest (runtime layer); needs a justified contamination/threshold | RT |
| J-37 | A Novel Hybrid Intrusion Detection Method Integrating Anomaly Detection with Misuse Detection | G. Kim, S. Lee, S. Kim | ESWA 41(4):1690–1700, 2014 | Q1 ✔ / Bib ✔ | https://doi.org/10.1016/j.eswa.2013.08.066 | Canonical **signature + anomaly** hierarchical fusion. Comparison point for RQ3 | RISK |
| J-38 | Survey of Intrusion Detection Systems: Techniques, Datasets and Challenges | A. Khraisat, I. Gondal, P. Vamplew, J. Kamruzzaman | Cybersecurity 2:20, 2019 | Q1 ✔ / Bib ✔ | https://doi.org/10.1186/s42400-019-0038-7 | Signature-based vs anomaly-based framing (rules vs ML/drift/runtime) | RISK |
| J-39 | Provenance-based Intrusion Detection Systems: A Survey | M. Zipperle, F. Gottwalt, E. Chang, T. Dillon | ACM CSUR 55(7), 2023 | Q1 ✔ / Bib ✔ | https://doi.org/10.1145/3539605 | Journal anchor for runtime behaviour monitoring; causal context beats flat features | RT |
| J-40 | Ensemble Based Collaborative and Distributed Intrusion Detection Systems: A Survey | G. Folino, P. Sabatino | JNCA, 2016 | Q1 ✔ / Bib ~ (DOI not seen) | – | Combining several detectors into one verdict | RISK |
| J-41 | Network Intrusion Detection System: A Systematic Study of ML and DL Approaches | Z. Ahmad et al. | Trans. Emerging Telecommunications Technologies 32(1):e4150, 2021 | ~ / Bib ✔ | https://doi.org/10.1002/ett.4150 | Metric choices (secondary citation) | EVAL |
| J-42 | A Comprehensive Survey on Ensemble Learning-Based Intrusion Detection Approaches in Computer Networks | Lucas et al. | IEEE Access, 2023 | Q1 ✔ / Bib ~ (vol/DOI UNVERIFIED) | – | 188 works on voting, stacking and weighting fusion | RISK |

## 2.6 Closest natural-language analogues (malicious or deceptive text detection, journals)

No Q1/Q2 journal paper on detecting prompt injection *in tool metadata* was found. The nearest journal-level analogues are detectors of deceptive or malicious instructions aimed at humans (phishing, social engineering) and LM-based anomaly detection.

| ID | Title | Authors | Venue | Quality | Link | Why it is an analogue | Layer |
|---|---|---|---|---|---|---|---|
| J-43 | Devising and Detecting Phishing Emails Using Large Language Models | F. Heiding, B. Schneier, A. Vishwanath, J. Bernstein, P.S. Park | IEEE Access 12:42131–42146, 2024 | Q1 ✔ / Bib ✔ | https://doi.org/10.1109/ACCESS.2024.3375882 | LLMs as classifiers of **malicious intent in text**, sometimes better than humans. Precedent for an LLM-judge layer | SEM |
| J-44 | Evaluating Large Language Models' Ability to Automate Spear Phishing | F. Heiding, S. Lermen, …, B. Schneier, A. Vishwanath | ESWA vol. 314, art. 131546, 2026 | Q1 ✔ / Bib ~ (DOI UNVERIFIED) | schneier.com/academic/archives/2026/06/… | LLM detection improves when "primed for suspicion", which informs detector prompt design | SEM |
| J-45 | An Explainable Transformer-based Model for Phishing Email Detection: A Large Language Model Approach | M.A. Uddin, M. Mahiuddin, I.H. Sarker | Computer Networks 277:112061, 2026 | Q1 ✔ / Bib ✔ | https://doi.org/10.1016/j.comnet.2026.112061 | Fine-tuned RoBERTa plus LIME/Transformers-Interpret explanations, a model for **explaining REVIEW/BLOCK verdicts** | SEM |
| J-46 | A Systematic Literature Review on Phishing Email Detection Using NLP Techniques | S. Salloum, T. Gaber, S. Vadera, K. Shaalan | IEEE Access 10:65703–65727, 2022 | Q1 ✔ / Bib ✔ | https://doi.org/10.1109/ACCESS.2022.3183083 | TF-IDF + linear/SVM is the most common baseline, which **justifies our TF-IDF+LR baseline** | SEM |
| J-47 | Deep Learning for Phishing Detection: Taxonomy, Current Challenges and Future Directions | N.Q. Do, A. Selamat, O. Krejcar, E. Herrera-Viedma, H. Fujita | IEEE Access 10:36429–36463, 2022 | Q1 ✔ / Bib ✔ | https://doi.org/10.1109/ACCESS.2022.3151903 | Reports **poor detection of unknown attacks**, which motivates our unseen-pattern RQ | SEM, EVAL |
| J-48 | Utilizing CNNs and Word Embeddings for Early-Stage Recognition of Persuasion in Chat-Based Social Engineering Attacks | N. Tsinganos, I. Mavridis, D. Gritzalis | IEEE Access 10:108517–108529, 2022 | Q1 ✔ / Bib ✔ | https://doi.org/10.1109/ACCESS.2022.3213681 | Detects **persuasion/urgency cues**, the human-targeted analogue of "IMPORTANT: before using this tool…" | SEM |
| J-49 | Leveraging Dialogue State Tracking for Zero-Shot Chat-Based Social Engineering Attack Recognition | N. Tsinganos, P. Fouliras, I. Mavridis | Applied Sciences 13(8):5110, 2023 | ~Q2 / Bib ✔ | https://doi.org/10.3390/app13085110 | **Zero-shot** malicious-intent detection; the same group's annotated corpus is a model for dataset annotation | SEM, DATA |
| J-50 | GramBeddings: A New Neural Network for URL Based Identification of Phishing Web Pages Through N-gram Embeddings | A.S. Bozkir, F.C. Dalgic, M. Aydos | Computers & Security 124:102964, 2023 | Q1 ✔ / Bib ~ (DOI UNVERIFIED) | – | Embedding detector for short adversarial strings (tool names) | SEM |
| J-51 | LAnoBERT: System Log Anomaly Detection based on BERT Masked Language Model | Y. Lee, J. Kim, P. Kang | Applied Soft Computing 146:110689, 2023 | Q1 ✔ / Bib ~ | sciencedirect S156849462300707X; arXiv 2111.09564 | **Unsupervised LM scoring trained on "normal" text only**. Directly transferable to scoring a received description against a trusted baseline | DRIFT, RT |
| J-52 | Semi-supervised Log Anomaly Detection based on Bidirectional Temporal Convolution Network | authors UNVERIFIED | Computers & Security 140:103808, 2024 | Q1 ✔ / Bib ~ | sciencedirect S0167404824001093 | BERT vectors plus pseudo-labelling under label scarcity | SEM, DATA |

---

# TIER 2: TOP CONFERENCES (CORE A*/A)

Ranks below are ✔ unless noted. Track caveats are given where relevant.

## 3.1 MCP-specific peer-reviewed conference papers

### C-01. MCPTox: A Benchmark for Tool Poisoning Attack on Real-World MCP Servers
- **Venue:** AAAI 2026 (A\*), Vol. 40 No. 42 (pp. 35811–35819 per a citing reference list)
- **Authors:** Wang et al. (full list UNVERIFIED)
- **Link:** https://doi.org/10.1609/aaai.v40i42.40895 | arXiv 2508.14925
- **What they did:**
  - The first large tool-poisoning benchmark, with malicious instructions in tool metadata at registration.
  - Built on **45 live servers and 353 real tools**; **1,497 test cases** from 3 attack templates × 10 risk categories; evaluates **20 LLM agents**.
  - o1-mini attack success rate was **72.8%**. The highest refusal rate (Claude-3.7-Sonnet) was **<3%**. More capable models are often *more* susceptible.
- **Gap:** An attack benchmark only; **no defense**. Shows that model refusal is not a defense.
- **Use for us:** DATA/EVAL. **The benchmark you must evaluate on**, or at least compare to.

### C-02. MPMA: Preference Manipulation Attack Against Model Context Protocol
- **Venue:** AAAI 2026 (A\*) | **Link:** https://ojs.aaai.org/index.php/AAAI/article/view/40898 | arXiv 2505.11154
- **What they did:** Names and descriptions are crafted so that agents prefer the attacker's server. DPMA inserts persuasive words directly; GAPMA uses advertising strategies plus a genetic algorithm for stealth.
- **Gap:** Attack only.
- **Use for us:** DATA. A distinct **"persuasive/advertising" poisoned subclass** (not imperative commands) that a detector must cover.

### C-03. MCP-SafetyBench: A Benchmark for Safety Evaluation of LLMs with Real-World MCP Servers
- **Venue:** ICLR 2026 (A\*) | **Authors:** X. Zong, Z. Shen, L. Wang, Y. Lan, C. Yang
- **Link:** proceedings.iclr.cc (2026, hash d46f127a…) | arXiv 2512.15163
- **What they did:** Real servers across 5 domains; taxonomy of 20 MCP attack types (server, host, user side); execution-based task success rate and attack success rate.
- **Gap:** Evaluates models, not defenses.
- **Use for us:** DATA/EVAL.

### C-04. MCP Security Bench (MSB): Benchmarking Attacks Against MCP in LLM Agents
- **Venue:** ICLR 2026 (A\*) | **Authors:** D. Zhang et al. (BUPT, UCSB)
- **Link:** https://iclr.cc/virtual/2026/poster/10007929 | arXiv 2510.15994 | code github.com/dongsenzhang/MSB
- **What they did:**
  - 12 attack types, incl. **name collision, preference manipulation, prompt injection in descriptions**, out-of-scope parameters and false-error escalation.
  - 10 domains, 405 tools, 2,000 attack instances; introduces the Net Resilient Performance (NRP) metric.
  - Stronger models are more vulnerable.
- **Use for us:** DATA/EVAL. Reuse its NRP utility–security metric for RQ4.

### C-05. MCIP: Protecting MCP Safety via Model Contextual Integrity Protocol
- **Venue:** EMNLP 2025 Main (A\*), pp. 1177–1194 | **Authors:** H. Jing et al. (HKUST, Huawei)
- **Link:** https://doi.org/10.18653/v1/2025.emnlp-main.62 | arXiv 2505.14590
- **What they did:** MAESTRO-guided analysis of missing safety mechanisms; a refined protocol with tracking logs; a taxonomy of unsafe MCP behaviours; a guard model trained on the logs.
- **Gap:** Guards **interaction traces**; does not address integrity or drift of tool definitions.
- **Use for us:** SEM/RT. A learned-guard comparison point.

### C-06. Securing the Tool Layer: A Threat Taxonomy and Runtime Defense Framework for MCP Deployments (ShieldMCP)
- **Venue:** ACL 2026 **Industry Track** (parent A\*; industry track is weighted lower) | **Author:** S. Yergattikar
- **Link:** preview.aclanthology.org/ingest-acl/2026.acl-industry.58 (DOI not seen)
- **What they did:**
  - A runtime interception layer checking MCP calls and responses (structural + semantic intent checks).
  - Taxonomy from 80+ SAFE-MCP techniques in 14 tactics; red-teamed on 5 LLM backends.
  - Tool-poisoning attack success fell **74% → <9%**; tool-response indirect prompt injection fell **47% → <6%**; **<120 ms median latency** per call.
- **Gap:** From the abstract, there is no evidence of version-to-version drift analysis, labelled FPR on benign updates, or per-layer ablation. **Verify in the full text.**
- **Use for us:** **Highest-overlap peer-reviewed competitor.** Its latency figure is the number to beat or match (RQ5).

## 3.2 Attacks on LLM-integrated apps and tool-using agents

| ID | Title | Venue (rank) | Authors | Link | What they did | Gap relevant to us | Layer |
|---|---|---|---|---|---|---|---|
| C-07 | Formalizing and Benchmarking Prompt Injection Attacks and Defenses | USENIX Sec 2024 (A\*), pp. 1831–1847 | Y. Liu, Y. Jia, R. Geng, J. Jia, N.Z. Gong | usenix.org/conference/usenixsecurity24/presentation/liu-yupei | Formal framework; 5 attacks × 10 defenses × 10 LLMs × 7 tasks; Open-Prompt-Injection toolkit | Data channel only; **formalise tool poisoning as injection via the metadata channel** | TM, SEM, EVAL |
| C-08 | Prompt Injection Attack to Tool Selection in LLM Agents (ToolHijacker) | **NDSS 2026 (A\*)** | J. Shi, Z. Yuan, G. Tie, P. Zhou, N.Z. Gong, L. Sun | ndss-symposium.org/ndss-paper/prompt-injection-attack-to-tool-selection-in-llm-agents | Malicious **tool document** inserted into the library; 96.43% attack success; no-box | **StruQ, SecAlign, known-answer detection, DataSentinel and perplexity detectors all insufficient**. The strongest A\* evidence that prompt-injection defenses do not transfer to tool metadata | TM, SEM |
| C-09 | AgentDojo: A Dynamic Environment to Evaluate Prompt Injection Attacks and Defenses for LLM Agents | NeurIPS 2024 D&B (A\*) | E. Debenedetti, J. Zhang, M. Balunović, L. Beurer-Kellner, M. Fischer, F. Tramèr | https://doi.org/10.52202/079017-2636 | 97 tasks, 629 security cases, extensible | Injection via tool *outputs*, not definitions. **Extend it with poisoned definitions** | DATA, EVAL |
| C-10 | Agent Security Bench (ASB) | ICLR 2025 (A\*) | H. Zhang, …, Y. Zhang | proceedings.iclr.cc 2025 (hash 5750f91d…) | 10 scenarios, 400+ tools, 27 attack/defense methods; 84.30% attack success | Defenses limited at every stage; utility–security metric | DATA, EVAL |
| C-11 | ToolSword: Unveiling Safety Issues of LLMs in Tool Learning Across Three Stages | ACL 2024 (A\*), pp. 2181–2211 | J. Ye et al. | aclanthology.org/2024.acl-long.119 | 6 safety scenarios across input, execution and output stages; 11 LLMs | Tool use erodes alignment | TM |
| C-12 | InjecAgent: Benchmarking Indirect Prompt Injections in Tool-Integrated LLM Agents | Findings of ACL 2024 | Q. Zhan, Z. Liang, Z. Ying, D. Kang | https://doi.org/10.18653/v1/2024.findings-acl.624 | 1,054 cases; direct-harm vs **data-exfiltration** goals; GPT-4 ReAct 24% attack success | Single-turn, simulated. **Use its goal categories as payload templates** | DATA |
| C-13 | Adaptive Attacks Break Defenses Against Indirect Prompt Injection Attacks on LLM Agents | Findings of NAACL 2025 | Q. Zhan, R. Fang, H.S. Panchal, D. Kang | aclanthology.org 2025.findings-naacl.395 | Broke **8/8** IPI defenses at >50% attack success | **We must test against adaptive poisoning**; favours non-ML layers | EVAL |
| C-14 | WASP: Benchmarking Web Agent Security Against Prompt Injection Attacks | NeurIPS 2025 D&B (A\*) | I. Evtimov, …, K. Chaudhuri | papers.nips.cc 2025 (hash 1c981838…) | Hijack 16–86% but attacker-goal completion only 0–17% | **Report hijack and harmful completion separately** | EVAL |
| C-15 | BadAgent: Inserting and Activating Backdoor Attacks in LLM Agents | ACL 2024 (A\*), pp. 9811–9827 | Y. Wang, D. Xue, S. Zhang, S. Qian | https://doi.org/10.18653/v1/2024.acl-long.530 | Backdoors via fine-tuning data | Use to **scope model backdoors out** of the threat model | TM |
| C-16 | Watch Out for Your Agents! Investigating Backdoor Threats to LLM-Based Agents | NeurIPS 2024 (A\*) | W. Yang, X. Bi, Y. Lin, S. Chen, J. Zhou, X. Sun | https://doi.org/10.52202/079017-3201 | Agent backdoor framework | Same as C-15 | TM |
| C-17 | AgentPoison: Red-teaming LLM Agents via Poisoning Memory or Knowledge Bases | NeurIPS 2024 (A\*) | Z. Chen, Z. Xiang, C. Xiao, D. Song, B. Li | neurips.cc/virtual/2024/poster/94715 | >80% attack success at <0.1% poison rate | Memory/RAG channel, not metadata | TM |
| C-18 | EIA: Environmental Injection Attack on Generalist Web Agents for Privacy Leakage | ICLR 2025 (A\*) | Z. Liao et al. | proceedings.iclr.cc 2025 (hash a73474c3…) | Up to 70% PII-theft success | Web environment channel | TM |
| C-19 | Identifying the Risks of LM Agents with an LM-Emulated Sandbox (ToolEmu) | ICLR 2024 (A\*) | Y. Ruan et al. | iclr.cc/virtual/2024/poster/19037 | 36 toolkits, 144 cases; LM-emulated tools | Emulation, not real servers | EVAL |
| C-20 | AgentHarm: A Benchmark for Measuring Harmfulness of LLM Agents | ICLR 2025 (A\*) | M. Andriushchenko et al. | proceedings.iclr.cc 2025 (hash c493d23a…) | 110 (440 augmented) malicious tasks | Harmful *user* requests, not poisoned tools | EVAL |
| C-21 | Benchmarking and Defending Against Indirect Prompt Injection Attacks on LLMs (BIPIA) | KDD 2025 (A\*) | J. Yi, Y. Xie, B. Zhu, E. Kiciman, G. Sun, X. Xie, F. Wu | https://doi.org/10.1145/3690624.3709179 | First IPI benchmark plus defenses | Data channel only | DATA, SEM |
| C-22 | Prompt-to-SQL Injections in LLM-Integrated Web Applications: Risks and Defenses | ICSE 2025 (A\*) | R. Pedro et al. | https://doi.org/10.1109/ICSE55347.2025.00007 | P2SQL in 5 real apps; middleware defenses | Supports **defense placement at middleware** (our gateway) | TM |
| C-23 | GPTracker: A Large-Scale Measurement of Misused GPTs | IEEE S&P 2025 (A\*) | X. Shen, Y. Shen, M. Backes, Y. Zhang | https://doi.org/10.1109/SP61157.2025.00118 | Builders evaded review by **"hiding intention in descriptions"** | A\* precedent for **metadata-level deception** in LLM app stores | TM |
| C-24 | UntrustIDE: Exploiting Weaknesses in VS Code Extensions | NDSS 2024 (A\*), Distinguished Paper | E. Lin, I. Koishybayev, T. Dunlap, W. Enck, A. Kapravelos | ndss-symposium.org/ndss-paper/untrustide-exploiting-weaknesses-in-vs-code-extensions | 25,402 extensions; 21 with verified code injection (>6M installs) | IDE extensions ≈ MCP servers in IDE agents (broad privileges, auto-update) | TM |
| C-25 | Hulk: Eliciting Malicious Behavior in Browser Extensions | USENIX Sec 2014 (A\*) | A. Kapravelos, C. Grier, N. Chachra, C. Kruegel, G. Vigna, V. Paxson | usenix.org/conference/usenixsecurity14/technical-sessions/presentation/kapravelos | Dynamic analysis of 48K extensions: 130 malicious | Precedent for a **sandboxed dynamic-analysis runtime layer** | RT |

## 3.3 Defenses (detection, training, system-level, runtime)

| ID | Title | Venue (rank) | Authors | Link | What they did | Gap relevant to us | Layer / baseline |
|---|---|---|---|---|---|---|---|
| C-26 | DataSentinel: A Game-Theoretic Detection of Prompt Injection Attacks | IEEE S&P 2025 (A\*), pp. 2190–2208 | Y. Liu, Y. Jia, J. Jia, D. Song, N.Z. Gong | arXiv 2504.11358; par.nsf.gov/biblio/10633541 | Minimax-fine-tuned known-answer detector | Fails on poisoned tool docs (C-08); prompts only | SEM, **baseline** |
| C-27 | Attention Tracker: Detecting Prompt Injection Attacks in LLMs | Findings of NAACL 2025, pp. 2309–2322 | K.-H. Hung, C.-Y. Ko, A. Rawat, I-H. Chung, W.H. Hsu, P.-Y. Chen | https://doi.org/10.18653/v1/2025.findings-naacl.123 | Training-free attention-based detector | **White-box only**; not usable behind closed models | SEM |
| C-28 | PIGuard (InjecGuard): Prompt Injection Guardrail via Mitigating Over-defense for Free | ACL 2025 (A\*) | H. Li, X. Liu, C. Xiao | aclanthology.org/2025.acl-long.1468; HF leolee99/PIGuard | NotInject benchmark: SOTA guards fall to **~60% accuracy on benign trigger-word inputs**; MOF training | **Over-defense = our FPR problem**; tool descriptions legitimately contain "must/always/ignore" | SEM, **strong baseline**, EVAL |
| C-29 | StruQ: Defending Against Prompt Injection with Structured Queries | USENIX Sec 2025 (A\*) | S. Chen, J. Piet, C. Sitawarin, D. Wagner | usenix.org/conference/usenixsecurity25/presentation/chen-sizhe | Instruction/data channel separation via fine-tuning | Tool descriptions sit in the **instruction channel**, so not covered | TM |
| C-30 | SecAlign: Defending Against Prompt Injection with Preference Optimization | ACM CCS 2025 (A\*) | S. Chen, A. Zharmagambetov, S. Mahloujifar, K. Chaudhuri, D. Wagner, C. Guo | https://doi.org/10.1145/3719027.3744836 | Preference optimisation; attack success <10% | Model-side; fails on C-08 | TM |
| C-31 | IsolateGPT: An Execution Isolation Architecture for LLM-Based Agentic Systems | NDSS 2025 (A\*) | Y. Wu, F. Roesner, T. Kohno, N. Zhang, U. Iqbal | https://doi.org/10.14722/ndss.2025.241131 | Hub-and-spoke per-app isolation; <30% overhead | **Broken by malicious app descriptions** (C-32) | POL, RT |
| C-32 | ACE: A Security Architecture for LLM-Integrated App Systems | **NDSS 2026 (A\*)** | (authors UNVERIFIED; Northeastern) | arXiv 2504.20984 | Shows **"Planner Manipulation via malicious app descriptions"** against IsolateGPT; abstract-concrete-execute plus static information-flow checks | **Strongest A\* evidence that description poisoning defeats architectural defenses**; still reads third-party descriptions at instantiation | TM, POL |
| C-33 | DRIFT: Dynamic Rule-Based Defense with Injection Isolation for Securing LLM Agents | NeurIPS 2025 (A\*) | H. Li, X. Liu, H.-C. Chiu, D. Li, N. Zhang, C. Xiao | neurips.cc/virtual/2025/poster/116028; code SaFoLab-WISC/DRIFT | Secure planner, dynamic validator, injection isolator | Tool-metadata trust not discussed | POL, RT, **baseline** |
| C-34 | MELON: Provable Defense Against Indirect Prompt Injection Attacks in AI Agents | ICML 2025 (A\*), PMLR 267:80310–80329 | K. Zhu, X. Yang, J. Wang, W. Guo, W.Y. Wang | proceedings.mlr.press/v267/zhu25z.html | Re-execute with the user prompt masked; flag tool calls that do not depend on the user task | ~2× inference cost (RQ5) | RT, **baseline** |
| C-35 | The Task Shield: Enforcing Task Alignment to Defend Against Indirect Prompt Injection | ACL 2025 (A\*), pp. 29680–29697 | F. Jia, T. Wu, X. Qin, A. Squicciarini | https://doi.org/10.18653/v1/2025.acl-long.1435 | Checks each tool call against user goals; AgentDojo attack success 2.07%, utility 69.79% | LLM cost; adaptive-attackable | RT, POL |
| C-36 | GuardAgent: Safeguard LLM Agents via Knowledge-Enabled Reasoning | ICML 2025 (A\*) | Z. Xiang, L. Zheng, et al. | icml.cc/virtual/2025/poster/46569 | Policy → executable guardrail code | Access-control benchmarks, not injection | POL |
| C-37 | ShieldAgent: Shielding Agents via Verifiable Safety Policy Reasoning | ICML 2025 (A\*), PMLR 267:8313–8344 | Z. Chen, M. Kang, B. Li | icml.cc/virtual/2025/poster/45989 | Verifiable rule extraction; recall 90.1% | Web-policy compliance | POL, RISK |
| C-38 | AgentSpec: Customizable Runtime Enforcement for Safe and Reliable LLM Agents | ICSE 2026 (A\*) | H. Wang, C.M. Poskitt, J. Sun | arXiv 2503.18666 | Trigger → predicate → enforcement DSL (block / ask / reflect) | **Maps to ALLOW/REVIEW/BLOCK**; rules need authoring | POL, RT |
| C-39 | Defense Against Prompt Injection Attack by Leveraging Attack Techniques | ACL 2025 (A\*) | Y. Chen, H. Li, Z. Zheng, D. Wu, Y. Song, B. Hooi | aclanthology 2025.acl-long.897 | Attack structures reused as defensive prompts | Prompt-level, brittle | SEM |
| C-40 | Defeating Prompt Injections by Design (CaMeL) | **Reported as IEEE SaTML 2026** (J1 agent; the P3 agent saw arXiv only, so verify; SaTML CORE rank not checked) | E. Debenedetti et al. (Google, DeepMind, ETH) | arXiv 2503.18813; code google-research/camel-prompt-injection | Privileged/quarantined LLMs plus capability-tracking interpreter; AgentDojo 77% vs 84% undefended | **Tool descriptions are trusted by the planner**, so poisoned metadata reaches the privileged LLM (our reading; verify) | POL, **baseline** |

## 3.4 Supply-chain integrity and malicious-package detection (conceptual foundation for INT and DRIFT)

| ID | Title | Venue (rank) | Authors | Link | What they did | Transfer to MCP / gap | Layer |
|---|---|---|---|---|---|---|---|
| C-41 | Survivable Key Compromise in Software Update Systems (TUF) | ACM CCS 2010 (A\*) | J. Samuel, N. Mathewson, J. Cappos, R. Dingledine | uptane.org PDF (DOI UNVERIFIED) | Role separation, threshold signing, freshness and rollback protection | **Rug pull = malicious update.** Shows that SHA-256 pinning lacks freeze/rollback protection | INT |
| C-42 | in-toto: Providing Farm-to-Table Guarantees for Bits and Bytes | USENIX Sec 2019 (A\*), pp. 1393–1410 | S. Torres-Arias, H. Afzali, T.K. Kuppusamy, R. Curtmola, J. Cappos | usenix.org/conference/usenixsecurity19/presentation/torres-arias | Signed supply-chain steps plus layout policy; would have prevented ≥83% of 30 incidents | Provenance "layout" for who may publish which tool | INT, POL |
| C-43 | Sigstore: Software Signing for Everybody | ACM CCS 2022 (A\*) | Z. Newman, J.S. Meyers, S. Torres-Arias | https://doi.org/10.1145/3548606.3560596 | Keyless OIDC signing plus transparency log | Transparency log of tool-definition versions detects split-view and silent changes | INT |
| C-44 | Speranza: Usable, Privacy-friendly Software Signing | ACM CCS 2023 (A\*) | K. Merrill, Z. Newman, S. Torres-Arias, K. Sollins | https://doi.org/10.1145/3576915.3623200 | Anonymous authorised signing | Registry signing design | INT |
| C-45 | CHAINIAC: Proactive Software-Update Transparency via Collectively Signed Skipchains and Verified Builds | USENIX Sec 2017 (A\*), pp. 1271–1287 | K. Nikitin et al. | usenix.org/conference/usenixsecurity17/…/nikitin | Witness co-signing plus a release log | Multiple scanners co-sign that a definition passed checks | INT |
| C-46 | Signing in Four Public Software Package Registries: Quantity, Quality, and Influencing Factors | IEEE S&P 2024 (A\*) | T.R. Schorlemmer et al. | arXiv 2401.14635 (DOI UNVERIFIED) | Optional signing gets low adoption; mandatory signing gets near-perfect rates | **Signing of tool metadata must be mandated** | INT |
| C-47 | SoK: Taxonomy of Attacks on Open-Source Software Supply Chains | IEEE S&P 2023 (A\*), pp. 1509–1526 | P. Ladisa, H. Plate, M. Martinez, O. Barais | DOI 10.1109/SP46215.2023.10179304 (seen only in citing papers) | 107 attack vectors, 94 incidents, 33 safeguards | **Template for an MCP attack tree**; no NL-metadata vector | TM |
| C-48 | Small World with High Risks: A Study of Security Threats in the npm Ecosystem | USENIX Sec 2019 (A\*) | M. Zimmermann, C.-A. Staicu, C. Tenny, M. Pradel | usenix.org/conference/usenixsecurity19/presentation/zimmerman | A package implicitly trusts 79 packages and 39 maintainers | Cross-server influence → per-server trust | TM |
| C-49 | Towards Measuring Supply Chain Attacks on Package Managers for Interpreted Languages | NDSS 2021 (A\*) | R. Duan et al. | https://doi.org/10.14722/ndss.2021.23055 | Metadata + static + dynamic pipeline; 339 new malicious packages | **Template for layering** (RQ3) | RISK, RT |
| C-50 | LastPyMile: Identifying the Discrepancy between Sources and Packages | ESEC/FSE 2021 (A\*), pp. 780–792 | D.-L. Vu, F. Massacci, I. Pashchenko, H. Plate, A. Sabetta | github.com/assuremoss/lastpymile | Diff artifact vs source; analyse **only the delta**; most deltas are benign | **Closest classical analogue of our DRIFT layer**: delta-focused analysis where benign change is common | DRIFT |
| C-51 | Containing Malicious Package Updates in npm with a Lightweight Permission System | ICSE 2021 (A\*), **details UNVERIFIED** (title seen) | G. Ferreira, L. Jia, J. Sunshine, C. Kästner (UNVERIFIED) | par.nsf.gov/biblio/10302333 | Updates requesting new capabilities are flagged | **"Capability drift"** analogue of description drift | POL, DRIFT |
| C-52 | Practical Automated Detection of Malicious npm Packages (Amalfi) | ICSE 2022 (A\*), pp. 1681–1692 | A. Sejfia, M. Schäfer | https://doi.org/10.1145/3510003.3510104 | Classifier → reproducibility check → clone detection; 95 new malware | A cheap classifier plus integrity check cuts FPs (RQ3/RQ4) | SEM, INT, RISK |
| C-53 | A Needle is an Outlier in a Haystack: Hunting Malicious PyPI Packages with Code Clustering (MPHunter) | ASE 2023 (A\*), pp. 307–318 | W. Liang, X. Ling, J. Wu, T. Luo, Y. Wu | ASE 2023 program | Unsupervised outlier ranking; 60 new malicious packages | **Unsupervised baseline** for novel poisoning | SEM |
| C-54 | SpiderScan: Practical Detection of Malicious NPM Packages Based on Graph-Based Behavior Modeling and Matching | ASE 2024 (A\*) | R. Wang et al. | ASE 2024 program | LLM plus graph matching plus dynamic confirmation | Escalate to the sandbox only when needed (latency) | RT, RISK |
| C-55 | EA4MP: integrating code behaviours with metadata features (title partly UNVERIFIED) | ASE 2024 (A\*) | UNVERIFIED | ASE 2024 program | Fuses metadata and behaviour in an ensemble | Precedent for **text + behaviour fusion** | RISK |
| C-56 | Malicious Package Detection using Metadata Information (MeMPtec) | WWW 2024 (A\*) | S. Halder, M. Bewong, et al. | arXiv 2402.07444 | **Easy- vs difficult-to-manipulate features**; −97.56% FP | **Most transferable robustness idea**: weight provenance/history over description text | RISK, SEM |
| C-57 | On the Feasibility of Cross-Language Detection of Malicious Packages in npm and PyPI | ACSAC 2023 (A) | P. Ladisa, S.E. Ponta, N. Ronzoni, M. Martinez, O. Barais | acsac.org/2023/program/final/s69.html | Lexical features transfer across ecosystems | Supports TF-IDF baseline and cross-family tests | SEM, EVAL |
| C-58 | Leveraging Large Language Models to Detect npm Malicious Packages (SocketAI) | ICSE 2025 (A\*) | N. Zahan, P. Burckhardt, M. Lysenko, F. Aboukhadijeh, L. Williams | arXiv 2403.12196 | LLM review plus static pre-screen (−78% LLM load); GPT-4 ~97% F1 | **Warning: an LLM judge can be injected by the description it reviews** (MCP-specific risk) | SEM, RISK |
| C-59 | MalGuard: Towards Real-Time, Accurate, and Actionable Detection of Malicious Packages in PyPI | USENIX Sec 2025 (A\*) | X. Gao et al. | usenix.org/conference/usenixsecurity25/presentation/gao-xingan | Classical ML is competitive in real time | Justifies a fast classical-ML layer | SEM |

## 3.5 Methodology (top conferences)

| ID | Title | Venue (rank) | Authors | Link | Why we cite it | Layer |
|---|---|---|---|---|---|---|
| C-60 | Dos and Don'ts of Machine Learning in Computer Security | USENIX Sec 2022 (A\*), pp. 3971–3988, Distinguished Paper | D. Arp et al. | usenix.org/conference/usenixsecurity22/presentation/arp | 10 pitfalls; reviewers' checklist (see J-31) | EVAL |
| C-61 | TESSERACT: Eliminating Experimental Bias in Malware Classification across Space and Time | USENIX Sec 2019 (A\*), pp. 729–746 | F. Pendlebury, F. Pierazzi, R. Jordaney, J. Kinder, L. Cavallaro | usenix.org/conference/usenixsecurity19/presentation/pendlebury | **Spatial bias** (unrealistic class ratio) and **temporal bias**; use **chronological splits for rug-pull data** | EVAL |
| C-62 | Transcend: Detecting Concept Drift in Malware Classification Models | USENIX Sec 2017 (A\*), pp. 625–642 | R. Jordaney et al. | usenix.org/…/jordaney | Classification with rejection, a principled **REVIEW** band | RISK |
| C-63 | Transcending Transcend: Revisiting Malware Classification in the Presence of Concept Drift | IEEE S&P 2022 (A\*) | F. Barbero, F. Pendlebury, F. Pierazzi, L. Cavallaro | https://doi.org/10.1109/SP46214.2022.9833659 | Cheaper conformal evaluators; calibrated rejection | RISK |
| C-64 | CADE: Detecting and Explaining Concept Drift Samples for Security Applications | USENIX Sec 2021 (A\*) | L. Yang, W. Guo, Q. Hao, A. Ciptadi, A. Ahmadzadeh, X. Xing, G. Wang | usenix.org/conference/usenixsecurity21/presentation/yang | **Learned contrastive distance** beats raw distance for drift. Closest analogue to embedding drift | DRIFT |
| C-65 | Outside the Closed World: On Using Machine Learning for Network Intrusion Detection | IEEE S&P 2010 (A\*), Test-of-Time | R. Sommer, V. Paxson | https://doi.org/10.1109/SP.2010.25 | "Anomalous ≠ malicious" warning for the runtime layer | RT |
| C-66 | Sentence-BERT: Sentence Embeddings using Siamese BERT-Networks | EMNLP 2019 (A\*), pp. 3982–3992 | N. Reimers, I. Gurevych | https://doi.org/10.18653/v1/D19-1410 | Basis of the embedding-drift layer | SEM, DRIFT |
| C-67 | SimCSE: Simple Contrastive Learning of Sentence Embeddings | EMNLP 2021 (A\*), pp. 6894–6910 | T. Gao, X. Yao, D. Chen | https://doi.org/10.18653/v1/2021.emnlp-main.552 | Alternative encoder. **Caution:** whole-text cosine misses short injected clauses | DRIFT |
| C-68 | Is BERT Really Robust? (TextFooler) | AAAI 2020 (A\*), pp. 8018–8025 | D. Jin, Z. Jin, J.T. Zhou, P. Szolovits | https://doi.org/10.1609/aaai.v34i05.6311 | Paraphrase/synonym evasion test | EVAL |
| C-69 | BERT-ATTACK: Adversarial Attack Against BERT Using BERT | EMNLP 2020 (A\*), pp. 6193–6202 | L. Li, R. Ma, Q. Guo, X. Xue, X. Qiu | https://doi.org/10.18653/v1/2020.emnlp-main.500 | Second evasion family | EVAL |
| C-70 | TextAttack: A Framework for Adversarial Attacks, Data Augmentation, and Adversarial Training in NLP | EMNLP 2020 Demos | J. Morris et al. | https://doi.org/10.18653/v1/2020.emnlp-demos.16 | Tool for running the above attacks reproducibly | EVAL |
| C-71 | Isolation Forest | ICDM 2008, pp. 413–422 | F.T. Liu, K.M. Ting, Z.-H. Zhou | https://doi.org/10.1109/ICDM.2008.17 | Runtime anomaly algorithm (journal version J-36) | RT |
| C-72 | Predicting Good Probabilities with Supervised Learning | ICML 2005 (A\*), pp. 625–632 | A. Niculescu-Mizil, R. Caruana | https://doi.org/10.1145/1102351.1102430 | **Calibrate each layer before fusion**; a weighted sum of raw scores is not meaningful | RISK |
| C-73 | The Foundations of Cost-Sensitive Learning | IJCAI 2001 (A\*), pp. 973–978 | C. Elkan | – | **Derive thresholds from costs and priors**, replacing the arbitrary 0–30/31–70/71–100 bands | RISK |
| C-74 | UNICORN: Runtime Provenance-Based Detector for Advanced Persistent Threats | NDSS 2020 (A\*) | X. Han, T. Pasquier, A. Bates, J. Mickens, M. Seltzer | ndss-symposium.org/ndss-paper/unicorn-… | Causal provenance vs flat features: "read then send" matters | RT |
| C-75 | Sometimes Simpler is Better: A Comprehensive Analysis of State-of-the-Art Provenance-Based Intrusion Detection Systems | USENIX Sec 2025 (A\*) | T. Bilot et al. | usenix.org/conference/usenixsecurity25/presentation/bilot | Simple baselines match complex systems. **The ablation must beat a strong simple baseline** | EVAL |

---

# TIER 3: WORKSHOPS AND LOWER-RANKED VENUES (cite for seminal or priority value)

| ID | Title | Venue | Link | Why |
|---|---|---|---|---|
| W-01 | Not What You've Signed Up For: Compromising Real-World LLM-Integrated Applications with Indirect Prompt Injection (Greshake et al.) | AISec@CCS 2023, pp. 79–90 (workshop) | arXiv 2302.12173 (ACM DOI UNVERIFIED) | **Seminal** indirect-injection paper; tool poisoning = IPI via metadata |
| W-02 | Ignore Previous Prompt: Attack Techniques for Language Models (Perez & Ribeiro) | NeurIPS 2022 ML Safety Workshop | arXiv 2211.09527 | Origin of goal hijacking; lexical rules |
| W-03 | LLM Platform Security: Applying a Systematic Evaluation Framework to OpenAI's ChatGPT Plugins (Iqbal, Kohno, Roesner) | AIES 2024 (**CORE C**), 7(1):611–623 | https://doi.org/10.1609/aies.v7i1.31664 | **Direct pre-MCP predecessor**: untrusted third-party plugins with NL manifests |
| W-04 | Contextual Agent Security: A Policy for Every Purpose (Conseca) | HotOS 2025 (workshop, CORE A) | https://doi.org/10.1145/3713082.3730378 | Where policies come from; just-in-time policies |
| W-05 | Neural Exec: Learning (and Learning from) Execution Triggers for Prompt Injection Attacks | AISec 2024, pp. 89–100 | arXiv 2403.03792 | Learned triggers; evasion of keyword rules |
| W-06 | How Not to Detect Prompt Injections with an LLM | ACM proceedings 2025 (likely AISec 2025; UNVERIFIED) | https://doi.org/10.1145/3733799.3762980 | Structural weakness of known-answer detection: **don't rely solely on LLM detectors** |
| W-07 | Backstabber's Knife Collection: A Review of Open Source Software Supply Chain Attacks | DIMVA 2020 (CORE B) | https://doi.org/10.1007/978-3-030-52683-2_2 | 174 malicious packages; dataset-curation template |
| W-08 | SoK: Analysis of Software Supply Chain Security by Establishing Secure Design Properties | SCORED@CCS 2022 | https://doi.org/10.1145/3560835.3564556 | Transparency / validity / separation properties: a framing for the gateway |
| W-09 | Embedding-based Classifiers Can Detect Prompt Injection Attacks (Ayub & Majumdar) | CAMLIS 2024 (CEUR Vol-3920) | arXiv 2410.22284 | **Closest analogue to our embedding+classifier layer** (RF on embeddings, AUC 0.764); single text, no drift |
| W-10 | Defending Against Indirect Prompt Injection Attacks With Spotlighting (Hines et al.) | arXiv 2403.14720; CEUR Vol-3920 (CAMLIS link UNVERIFIED) | arXiv 2403.14720 | Cheap prompt-level ablation arm ("spotlight" descriptions) |
| W-11 | Fine-tuned LLMs: Improved Prompt Injection Attacks Detection | IEEE COMPSAC 2025 (CORE B) | https://doi.org/10.1109/COMPSAC65507.2025.00134 | 99% in-distribution: an example of the unrealistic-evaluation pitfall |
| W-12 | Troubleshooting an Intrusion Detection Dataset: the CICIDS2017 Case Study | IEEE SPW 2021, pp. 7–12 | https://doi.org/10.1109/SPW53761.2021.00009 | Dataset-construction errors inflate results; publish a labelling protocol |
| W-13 | The Adverse Effects of Code Duplication in ML Models of Code (Allamanis) | Onward! @SPLASH 2019 | arXiv 1812.06469 | Near-duplicates inflate metrics by up to 100%: **group-aware splits** |

Also relevant but not peer-reviewed (cite as standards or grey literature, see Step 1): OWASP MCP Top 10 (MCP03), OWASP LLM Top 10 2025, MITRE ATLAS AML.T0110/T0109, NIST AI 100-2e2025, the CoSAI MCP white paper, and the NSA CSI on MCP.

---

# APPENDIX A: arXiv-only works that threaten novelty (read before claiming novelty; cite sparingly)

These are **not** peer-reviewed as far as could be verified, but reviewers will know them. "Overlap" means overlap with our proposal.

| ID | Work | arXiv | What it does | Overlap / threat |
|---|---|---|---|---|
| A-01 | Jamshidi et al., *Securing the MCP: Defending LLMs Against Tool Poisoning and Adversarial Attacks* (later retitled "Semantic Attacks on Tool-Augmented LLMs…") | 2512.06556 | Descriptor poisoning, shadowing and **post-approval change**; defense = **signed manifests + LLM descriptor review + runtime guardrails** | **HIGH**: 3 of our 5 layers. Our edge must be drift scoring, calibrated fusion, labelled version-pair data and ablation |
| A-02 | Xing et al., *MCP-Guard: A Multi-Stage Defense-in-Depth Framework* | 2508.10991 | Pattern scan → fine-tuned E5 (96.01% accuracy) → LLM arbiter; **MCP-AttackBench, 70,448 samples** | **HIGH** for the detector layer |
| A-03 | ETDI: *Mitigating Tool Squatting and Rug Pull Attacks in MCP using OAuth-Enhanced Tool Definitions and Policy-Based Access Control* | 2506.01333 (reported IEEE CARS; UNVERIFIED) | Signed, immutable, versioned definitions; OAuth scopes; Cedar/OPA policy; re-approval on change | **HIGH** for INT + POL. Hashing/signing cannot be our novelty |
| A-04 | Mattsson, Nyberg, Borg, Britto, *Machine Learning-Based Detection of MCP Attacks* | 2604.10534 | SVC/BERT/BiLSTM on **1,440 tool descriptions**; binary F1 = 100% | **HIGH** for the classifier. A saturated score suggests an easy dataset, so **our contribution must be harder generalisation** |
| A-05 | Huang et al. (Fudan), *From Component Manipulation to System Compromise: Understanding and Detecting Malicious MCP Servers* (detector "Connor") | 2604.01905 | Pre-execution checks + **runtime behaviour vs declared intent**; F1 94.6%; 114 malicious servers | **HIGH** for the RT layer |
| A-06 | MindGuard: *Tracking, Detecting, and Attributing MCP Tool Poisoning Attack* | 2508.20412 | Attention-based Decision Dependence Graph; AP 94–99% | MEDIUM; white-box only |
| A-07 | Li et al., *MCP-ITP: Automated Framework for Implicit Tool Poisoning* | 2601.07395 | Detector-evading poison optimisation; the poisoned tool is never called | Adversary for our robustness tests |
| A-08 | *TRUSTDESC: Preventing Tool Poisoning via Trusted Description Generation* | 2604.07536 | Regenerates trusted descriptions instead of detecting | MEDIUM–HIGH: an alternative paradigm, must be discussed |
| A-09 | Sneh et al., *ToolTweak: An Attack on Tool Selection* | 2510.02554 | Rewrites name/description; selection rises from ~20% to 81% | Persuasive subclass; paraphrase/perplexity defenses partly work |
| A-10 | Mo et al., *Attractive Metadata Attack* | 2508.02110 | Name, description and **schema** manipulation | Hash must cover the whole definition |
| A-11 | Yang et al., *MCPSecBench* | 2508.13220 | 17 attacks × 4 surfaces; protections <30% success | Benchmark |
| A-12 | Radosevich & Halloran, *MCP Safety Audit* | 2504.03767 | MCPSafetyScanner agentic auditor | Offline audit |
| A-13 | Narajala & Habler, *Enterprise-Grade Security for MCP* | 2504.08623 (IEEE Xplore 11395723, venue UNVERIFIED) | Conceptual layered zero-trust framework, **no evaluation** | Reviewers may cite it as a prior "layered MCP defense" |
| A-14 | Metere, *Attested Tool-Server Admission* (SEP-2809) | 2605.24248 | Signed admission, pinned trust root, deny-by-default allowlist | INT + POL |
| A-15 | Li & Gao, *A First Look at the Security Issues in the MCP Ecosystem* | 2510.16558 (venue UNVERIFIED; acknowledges a shepherd) | **67,057 servers** from 6 registries; hijacking and metadata manipulation | Motivation; possibly a source of real tool definitions |
| A-16 | *When MCP Servers Attack: Taxonomy, Feasibility, and Mitigation* | 2509.24272 | 12 categories of malicious-server PoCs; scanners miss deceptive text | Motivation |
| A-17 | Song et al., *Beyond the Protocol: Attack Vectors in the MCP Ecosystem* | 2506.02040 | Ecosystem attack vectors | Taxonomy |
| A-18 | *MCP-38* threat taxonomy | 2603.18063 | 38 categories mapped to STRIDE/OWASP | Taxonomy |
| A-19 | *MCP-DPT: Defense-Placement Taxonomy* | 2604.07551 | Coverage of defenses by placement | **Read**: it may map the same gap |
| A-20 | *MCPSHIELD formal framework* | 2604.05969 | Formal threat/verification model | MEDIUM |
| A-21 | *ChainWatch: Kill-Chain-Aligned Sequential Detection* | 2607.19432 | Multi-step runtime detection; critiques single-call defenses | RT |
| A-22 | *Content-Aware Attack Detection in Agent Tool-Call Traffic* | 2605.11053 | Black-box detection on tool-call content | SEM |
| A-23 | Guo et al., *Systematic Analysis of MCP Security* (MCPLib → MCPXKIT) | 2508.12538 | 31 attacks in 4 classes; agents rely blindly on descriptions | Motivation |
| A-24 | *Invisible Threats from MCP* (stealthy payloads in tool responses) | 2603.24203 | TDSC template header only; **acceptance UNVERIFIED** | Watch for publication |
| A-25 | Beurer-Kellner et al., *Design Patterns for Securing LLM Agents against Prompt Injections* | 2506.08837 | 6 architectural patterns | Design rationale |
| A-26 | Shi et al., *Progent: Programmable Privilege Control for LLM Agents* | 2504.11703 | Tool-call policy DSL | POL baseline |
| A-27 | Shi et al., *PromptArmor* | 2507.15219 | LLM pre-filter; <1% FPR/FNR on AgentDojo | LLM-judge baseline |
| A-28 | Costa et al., *FIDES: Securing AI Agents with Information-Flow Control* | 2505.23643 | IFC planner | POL |
| A-29 | Wallace et al., *The Instruction Hierarchy* | 2404.13208 | Privilege hierarchy | Descriptions inherit high privilege (our analysis) |
| A-30 | Inan et al., *Llama Guard* (Meta) | 2312.06674 | Safety classifier | Off-the-shelf baseline |

Other related preprints, by title only, are in the annex files: Imprompter, MalTool, ContextLeak, ToolFlood, "Select Me!", PIShield, PromptSleuth, RTBAS, f-secure IFC, Meta SecAlign, *On the (In)Security of LLM App Stores* (arXiv 2407.08422; 786,036 apps, 15,146 with misleading descriptions).

---

# 5. Leads NOT yet verified (do not cite until checked)

1. **IEEE Access 2026 SLR by Woesle & Buettner** (IEEE Xplore document 11551573).
   - A search snippet says it coded 81 papers and found **83.9% target the prompt interface and *zero* the tool/connector boundary**.
   - This would be excellent gap evidence, but the title could not be confirmed in a second search.
   - **Open the IEEE Xplore page yourself.**
2. **Hou et al. TOSEM article number** (DOI 10.1145/3796519 seen; issue in progress).
3. **CaMeL at IEEE SaTML 2026**: confirm.
4. **ETDI at IEEE CARS**: confirm.
5. **Ladisa et al. SoK DOI** 10.1109/SP46215.2023.10179304: confirm on IEEE Xplore.
6. **"LLM App Store Analysis" (J-26)**: the agents disagree (TOSEM 34(5):125 vs SE-2030 workshop header). Confirm at doi.org/10.1145/3708530.
7. Quartiles marked "~" in §1.1, especially IJNDI (anomalous), JCP (MDPI), IJIS and High-Confidence Computing.
8. **Direct database sweep still recommended.** Web search indexes these journals poorly, so run your own queries on ScienceDirect, IEEE Xplore and Springer. Suggested queries:
   - ScienceDirect: `"Model Context Protocol" OR "tool poisoning" OR "prompt injection"`, filtered to *Computers & Security*, *JISA*, *ESWA*, *KBS*, *FGCS*, *Computer Networks* (2024–2026).
   - IEEE Xplore: the same, filtered to TIFS, TDSC, TSE, IEEE Access, IoT-J.
   - Springer: *Empirical Software Engineering*, *Int. J. Information Security*, *Cybersecurity*.

   No such article was confirmed in Computers & Security, TIFS, TDSC, TSE, ESWA, KBS, FGCS or JSS **by web search**. That is a coverage limitation, not proof of absence.

---

# 6. Priority download list (read these in full for Step 4)

**A. Must read: direct competitors and closest works**
1. J-04 Huang et al., JCP 2026 (MCP threat model + client tests) — https://doi.org/10.3390/jcp6030084
2. C-06 ShieldMCP, ACL 2026 Industry — preview.aclanthology.org/ingest-acl/2026.acl-industry.58
3. A-01 Jamshidi et al. — arXiv 2512.06556
4. A-02 MCP-Guard — arXiv 2508.10991
5. A-03 ETDI — arXiv 2506.01333
6. A-04 ML-Based Detection of MCP Attacks — arXiv 2604.10534
7. A-05 Connor (malicious MCP servers) — arXiv 2604.01905
8. A-08 TRUSTDESC — arXiv 2604.07536
9. C-01 MCPTox, AAAI 2026 — https://doi.org/10.1609/aaai.v40i42.40895
10. C-04 MSB, ICLR 2026 — iclr.cc/virtual/2026/poster/10007929

**B. Must read: Q1 journal anchors**
11. J-01 Hou et al., TOSEM — https://doi.org/10.1145/3796519
12. J-02 Gasmi et al., Information Sciences — ScienceDirect PII S0020025526001623
13. J-03 Ferrag et al., ICT Express — ScienceDirect PII S2405959525001997
14. J-06 Deng et al., ACM CSUR — https://doi.org/10.1145/3716628
15. J-05 He et al., ACM CSUR — https://doi.org/10.1145/3773080
16. J-24 Williams et al., TOSEM — https://doi.org/10.1145/3714464
17. J-20 JailGuard, TOSEM — https://doi.org/10.1145/3724393
18. J-21 Gakh & Bahsi, IJIS — https://doi.org/10.1007/s10207-026-01338-7
19. J-31 Arp et al., CACM — https://doi.org/10.1145/3643456
20. J-32 Axelsson, TISSEC — https://doi.org/10.1145/357830.357849

**C. Must read: A\* conference anchors**
21. C-08 ToolHijacker, NDSS 2026
22. C-32 ACE, NDSS 2026 (arXiv 2504.20984)
23. C-07 Liu et al., USENIX Sec 2024
24. C-13 Adaptive Attacks, NAACL Findings 2025
25. C-28 PIGuard, ACL 2025
26. C-09 AgentDojo, NeurIPS 2024
27. C-50 LastPyMile, FSE 2021
28. C-56 MeMPtec, WWW 2024
29. C-61 TESSERACT, USENIX Sec 2019
30. C-64 CADE, USENIX Sec 2021
31. C-41 TUF, CCS 2010, and C-43 Sigstore, CCS 2022
32. C-23 GPTracker, S&P 2025
33. C-34 MELON, ICML 2025, and C-38 AgentSpec, ICSE 2026
34. W-03 Iqbal et al., AIES 2024 (ChatGPT plugins)
35. W-09 Ayub & Majumdar, CAMLIS 2024 (embedding classifier)

---

## 7. Annex (full detail per area, with every verification note)

Folder: `annex_detailed_area_reports/`
- `P1_MCP_specific_literature.md`: 26 MCP works with a coverage matrix
- `P2_attacks_prompt_injection_tool_selection.md`
- `P3_defenses_agents_guardrails.md`: includes the baselines-with-code table
- `P4_supply_chain_integrity.md`: includes 16 transferable ideas
- `P5_methodology_evaluation.md`: includes 12 methodological pitfalls in the current proposal
- `J1_journal_sweep.md`
- `J2_quartiles_ranks_analogues_verification.md`
