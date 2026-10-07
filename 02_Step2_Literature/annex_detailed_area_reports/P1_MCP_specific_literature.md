# Step 2 — Area P1: MCP-specific academic literature (2024 – Oct 2026)

Compiled 2026-10-07.

## Read this first: what was checked, and how

- **How things were checked.** Every entry below was confirmed through WebSearch result snippets: titles, authors, arXiv IDs, venue listings and abstract text. Direct page fetches were blocked by the egress proxy for arxiv.org, alphaxiv.org, huggingface.co, aclanthology.org (including preview.), ojs.aaai.org, conf.researchr.org, semanticscholar.org and themoonlight.io. So **I could not open any full text.** Numbers come from abstracts as the search engine quoted them. Numbers from third-party summaries are labelled **[secondary]**.
- **Searching stopped early.** Partway through, the shared WebSearch budget (200 per turn, shared by all agents) ran out. Several known leads could not be checked. They appear in Section E as **UNVERIFIED leads**, with no details claimed. This file therefore lists **26 confirmed works plus about 15 unverified leads**, not a complete census. A follow-up pass should check Section E.
- **Venue tiers.** CORE ranks and SJR quartiles below are **per general knowledge — verify**. scimagojr.com and portal.core.edu.au were not reachable.

---

## Section A — Peer-reviewed journals

### [P1-01] Model Context Protocol (MCP): Landscape, Security Threats, and Future Research Directions
- **Authors and year:** Xinyi Hou, Yanjie Zhao, Shenao Wang, Haoyu Wang (Huazhong University of Science and Technology). arXiv v1 March 2025; v3 revised 7 Oct 2025.
- **Publication status:**
  - Listed in the **FSE 2026 Journal-First track** (conf.researchr.org listing seen in search results).
  - A bibliography entry in another paper cites it as *ACM Transactions on Software Engineering and Methodology (TOSEM), 2025*.
  - The ACM DOI, volume and issue are **UNVERIFIED**. The arXiv v3 ACM header is still a placeholder ("1, 1 (October 2025)").
- **Tier:** TOSEM is **Q1** (SJR, Software) per general knowledge — verify. FSE is CORE **A\*** per general knowledge.
- **Links:** arXiv 2503.23278 (https://arxiv.org/abs/2503.23278). Code: github.com/security-pride/MCP_Landscape.
- **What they did:**
  - A systematic study of MCP from both architecture and security angles.
  - Defines the MCP server lifecycle: 4 phases (creation, deployment, operation, maintenance) broken into 16 key activities.
  - Builds a threat taxonomy over 4 attacker types (malicious developers, external attackers, malicious users, security flaws), covering 16 threat scenarios.
  - Discusses adoption, integration patterns and future research directions.
- **Key numbers:** 4 phases, 16 activities, 4 attacker types, 16 threat scenarios. It is a survey, so there are no detection metrics.
- **Limitations and future work:** It frames future research directions; the details were not seen.
- **Overlap with our proposal:** Survey and taxonomy only. It names tool poisoning and rug-pull-style threats but builds no detector.
- **Novelty threat:** **Low.** Most useful as a citation that motivates the problem.
- **Sources seen:** arXiv abstract pages v1 and v3 in search results; FSE 2026 journal-first listing; citation snippet naming TOSEM.

*No other MCP-specific journal article (IEEE Access, Computers & Security, Future Internet, Electronics, TDSC and similar) could be confirmed before the search budget ran out. See Section E.*

---

## Section B — Peer-reviewed conferences (A\*/A first)

### [P1-02] MCPTox: A Benchmark for Tool Poisoning Attack on Real-World MCP Servers
- **Authors and year:** Not captured in the snippets — **UNVERIFIED**. AAAI 2026, presented 22 Jan 2026 in Singapore (underline.io listing).
- **Publication status:** Conference, **AAAI 2026** (AAAI-26 proceedings, Vol. 40 No. 42). DOI 10.1609/aaai.v40i42.40895. arXiv 2508.14925.
- **Tier:** AAAI is CORE **A\*** per general knowledge.
- **Links:** https://ojs.aaai.org/index.php/AAAI/article/view/40895 and https://arxiv.org/abs/2508.14925. Dataset: anonymous.4open.science/r/AAAI26-7C02.
- **What they did:**
  - Presented as the first systematic, large-scale benchmark of tool poisoning, where malicious instructions sit in tool metadata at registration time.
  - Built on 45 live, real-world MCP servers and 353 authentic tools.
  - Test cases were generated from 3 attack templates using few-shot learning, across 10 risk categories.
  - Evaluated 20 LLM agents.
- **Key numbers (from the abstract):**
  - 1,497 malicious test cases in the AAAI version; the arXiv v1 says 1,348.
  - o1-mini attack success rate (ASR) of 72.8%.
  - The highest refusal rate (Claude-3.7-Sonnet) was below 3%.
  - More capable models were often more susceptible.
  - [secondary blog] Average ASR of 36.5% — not confirmed against the paper.
- **Limitations:** Attack and benchmark only; no defense is proposed. Shows that model-side refusal is not enough.
- **Overlap:** Dataset/benchmark (poisoned tool descriptions on real servers).
- **Novelty threat:** **Medium.** It is the de-facto poisoned-description benchmark we must evaluate on or compare against. It does not detect or defend.
- **Sources seen:** AAAI OJS listing and arXiv abstract in search results; underline.io.

### [P1-03] MPMA: Preference Manipulation Attack Against Model Context Protocol
- **Authors and year:** Authors not captured by name — **UNVERIFIED**. Affiliations: UESTC and City University of Hong Kong. arXiv May 2025; AAAI 2026.
- **Publication status:** Conference, **AAAI 2026** (OJS article 40898; CityU scholars page). arXiv 2505.11154.
- **Tier:** AAAI is CORE **A\*** per general knowledge.
- **Links:** https://ojs.aaai.org/index.php/AAAI/article/view/40898 and https://arxiv.org/abs/2505.11154.
- **What they did:**
  - A third party writes a tool's name and description so that LLM agents prefer its MCP server over competitors (economic motive: revenue or ads).
  - DPMA inserts persuasive words directly; it is effective but not stealthy.
  - GAPMA uses 4 advertising strategies plus a genetic algorithm to stay stealthy.
- **Key numbers:** None seen in the snippets.
- **Limitations:** Attack paper.
- **Overlap:** It is a description-level manipulation class our NLP detector should cover: persuasive or advertising language, which is distinct from injected commands.
- **Novelty threat:** **Low.** It is an attack. Useful as an extra "poisoned" subclass for our dataset.
- **Sources seen:** AAAI OJS listing, arXiv v1/v2 abstract, and CityU page in search results.

### [P1-04] MCP-SafetyBench: A Benchmark for Safety Evaluation of Large Language Models with Real-World MCP Servers
- **Authors and year:** Xuanjun Zong, Zhiqi Shen, Lei Wang, Yunshi Lan, Chao Yang. 2026.
- **Publication status:** Conference, **ICLR 2026** (poster; proceedings.iclr.cc; mlanthology entry). arXiv 2512.15163.
- **Tier:** ICLR is CORE **A\*** per general knowledge.
- **Links:** https://proceedings.iclr.cc/paper_files/paper/2026/hash/d46f127a80dc58cbc0732a717285c43a-Abstract-Conference.html. Code: github.com/xjzzzzzzzz/MCPSafety.
- **What they did:**
  - Benchmark built on real MCP servers across 5 domains: browser automation, financial analysis, navigation, repository management, web search.
  - Unified taxonomy of 20 MCP attack types spanning server, host and user sides.
  - Tasks require multi-step reasoning and cross-server coordination.
  - Scoring is execution-based, reporting task success rate (TSR) and ASR.
- **Key numbers:**
  - Abstract: all models remain vulnerable, with a safety–utility trade-off.
  - [secondary] 245 test cases; ASR 29.80%–48.16%.
- **Limitations:** Evaluates models, not defenses.
- **Overlap:** Benchmark only.
- **Novelty threat:** **Low–Medium.** Possible evaluation set; no detector.
- **Sources seen:** ICLR proceedings and virtual-site listing; mlanthology; arXiv HTML snippet.

### [P1-05] MCP Security Bench (MSB): Benchmarking Attacks Against Model Context Protocol in LLM Agents
- **Authors and year:** Dongsen Zhang et al. (BUPT and UC Santa Barbara). arXiv 14 Oct 2025; ICLR 2026.
- **Publication status:** Conference, **ICLR 2026** (iclr.cc poster 10007929; OpenReview PDF; mlanthology). arXiv 2510.15994.
- **Tier:** ICLR is CORE **A\*** per general knowledge.
- **Links:** https://iclr.cc/virtual/2026/poster/10007929. Code: github.com/dongsenzhang/MSB.
- **What they did:**
  - End-to-end benchmark covering planning, invocation and response handling.
  - 12 attack types, including name collision, preference manipulation, prompt injection in tool descriptions, out-of-scope parameters, user-impersonating responses, false-error escalation, tool transfer, retrieval injection, and mixed attacks.
  - Real tools are run through MCP.
  - Introduces the Net Resilient Performance (NRP) metric.
- **Key numbers:**
  - 10 domains, 405 tools, 2,000 attack instances.
  - 9 agents in the ICLR version; 10 in arXiv v1.
  - Stronger models are more vulnerable.
- **Overlap:** Benchmark that includes description-injection and name-collision cases (shadowing / squatting).
- **Novelty threat:** **Low–Medium.** Benchmark, not a gateway.
- **Sources seen:** ICLR listing, OpenReview, arXiv abstract snippets.

### [P1-06] MCIP: Protecting MCP Safety via Model Contextual Integrity Protocol
- **Authors and year:** Huihao Jing et al. (HKUST and Huawei). 2025.
- **Publication status:** Conference, **EMNLP 2025 Main**, pp. 1177–1194. DOI 10.18653/v1/2025.emnlp-main.62. arXiv 2505.14590.
- **Tier:** EMNLP is CORE **A** per general knowledge (some lists say A\*) — verify.
- **Links:** https://aclanthology.org/2025.emnlp-main.62. Code: HKUST-KnowComp GitHub.
- **What they did:**
  - Used the MAESTRO framework to find safety mechanisms MCP is missing.
  - Proposes MCIP, a refined protocol with tracking logs.
  - Builds a fine-grained taxonomy of unsafe MCP behaviours, plus benchmark and training data.
  - Trains a safety-aware guard model on the logs.
- **Key numbers:** None seen. The abstract says safety performance "substantially improved".
- **Overlap:** LLM-guard detection over interaction logs; runtime monitoring/tracking; dataset.
- **Novelty threat:** **Medium.** It is a learned guard for MCP, but over interaction traces rather than integrity or drift of tool definitions.
- **Sources seen:** ACL Anthology entry, underline EMNLP 2025, arXiv in search results.

### [P1-07] Securing the Tool Layer: A Threat Taxonomy and Runtime Defense Framework for Model Context Protocol Deployments (ShieldMCP)
- **Authors and year:** Saurabh Yergattikar. 2026.
- **Publication status:** Conference industry track, **ACL 2026 Industry Track** (Anthology ID 2026.acl-industry.58; San Diego, July 2026).
- **Tier:** ACL main conference is CORE **A\*** per general knowledge. **Note:** this is the Industry Track, which carries less weight than the main track.
- **Links:** https://preview.aclanthology.org/ingest-acl/2026.acl-industry.58/ (preview page). DOI not seen — UNVERIFIED.
- **What they did:**
  - ShieldMCP, a runtime interception layer that checks MCP tool calls and responses in real time.
  - Threat taxonomy built from 80+ attack techniques in the SAFE-MCP (OpenSSF / Linux Foundation) catalogue, organised into 14 MITRE ATT&CK-style tactics.
  - Red-teamed across 5 LLM backends.
- **Key numbers (abstract):**
  - Tool-poisoning ASR fell from 74% to under 9%.
  - Indirect prompt injection via tool responses fell from 47% to under 6%.
  - Median added latency under 120 ms per tool call.
- **Limitations:** Discusses the tension between security and agent utility. Full text not seen.
- **Overlap:** A gateway/interceptor; runtime monitoring; tool-poisoning detection; latency measurement.
- **Novelty threat:** **HIGH.** Closest peer-reviewed match to our gateway concept, with latency figures. We must differentiate on integrity pinning and signatures, semantic drift between versions, explicit capability policy, a public labelled dataset, and ablation — if ShieldMCP lacks these (unverified, as the full text was not seen).
- **Sources seen:** ACL Anthology preview page (search snippet).

---

## Section C — Workshops

None could be confirmed before the search budget ran out. Leads are in Section E.

---

## Section D — arXiv-only preprints (no peer-reviewed venue found; they still threaten novelty)

### [P1-08] MCP Safety Audit: LLMs with the Model Context Protocol Allow Major Security Exploits
- **Authors and year:** Brandon Radosevich, John Halloran (Leidos). April 2025.
- **Status:** arXiv 2504.03767 (v2). No venue found.
- **What they did:**
  - Showed that Claude and Llama-class LLMs can be coerced through MCP servers (for example, the filesystem server) into malicious code execution, remote access control and credential theft.
  - Proposes **MCPSafetyScanner**, an agentic multi-agent auditor of arbitrary MCP servers. It generates adversarial samples, searches for related vulnerabilities and remediations, and produces a report.
- **Numbers:** None seen.
- **Overlap:** Pre-deployment auditing / scanning.
- **Novelty threat:** **Low–Medium.** It audits servers offline; there is no gateway, pinning or drift.
- **Sources seen:** arXiv v2 abstract (search snippet).

### [P1-09] Enterprise-Grade Security for the Model Context Protocol (MCP): Frameworks and Mitigation Strategies
- **Authors and year:** Vineeth Sai Narajala, Idan Habler. April 2025 (v2 2 May 2025).
- **Status:** arXiv 2504.08623.
- **What they did:**
  - Threat model that includes tool poisoning.
  - Multi-layered defense-in-depth / zero-trust framework: tool vetting, continuous monitoring, input/output validation, and network/app/host/data/identity controls.
  - Implementation patterns and a qualitative risk table.
- **Numbers:** None. The paper is conceptual.
- **Overlap:** Conceptual version of a layered gateway, but **no empirical evaluation**.
- **Novelty threat:** **Medium.** Reviewers will cite it as a prior "layered MCP defense". Our edge is the implementation plus quantitative evaluation.
- **Sources seen:** arXiv abstract and conclusion snippet.

### [P1-10] ETDI: Mitigating Tool Squatting and Rug Pull Attacks in MCP by using OAuth-Enhanced Tool Definitions and Policy-Based Access Control
- **Authors and year:** Affiliations listed as Amazon, OWASP and Intuit. A secondary source names Cisco — use the paper. June 2025. Author names UNVERIFIED in the snippets seen.
- **Status:** arXiv 2506.01333.
  - A related Python SDK pull request exists (modelcontextprotocol/python-sdk #845); merge status unverified.
  - A third-party PyPI package `mcp-etdi` also exists.
- **What they did:**
  - Cryptographic identity verification.
  - **Immutable, versioned, signed tool definitions** (OAuth 2.0 / JWT).
  - Explicit permission management.
  - Policy-based access control with Cedar or OPA.
  - A version or hash mismatch forces re-approval, which is the rug-pull defense.
- **Numbers:** None seen.
- **Overlap:** **Integrity, signatures and capability policy** — layers 1 and 3 of our design.
- **Novelty threat:** **HIGH for layers 1 and 3.** Signing and version-pinning against rug pulls is already proposed. Our hash-pinning and Ed25519 cannot be the novelty claim. Novelty must come from semantic-drift scoring, combined detection and empirical evaluation; ETDI reports no detection metrics, as far as seen.
- **Sources seen:** arXiv abstract snippet; GitHub PR #845 title; PyPI listing.

### [P1-11] MCP-Guard: A Multi-Stage Defense-in-Depth Framework for Securing Model Context Protocol in Agentic AI
- **Authors and year:** Wenpeng Xing, Zhonghao Qi, Yupeng Qin, Yilin Li, Caini Chang, Jiahui Yu, Changting Lin, Zhenzhen Xie, Meng Han. v1 14 Aug 2025; v4 8 Jan 2026.
- **Status:** arXiv 2508.10991. No venue seen.
- **What they did:** A 3-stage pipeline:
  1. A pattern-based fast scan.
  2. A fine-tuned E5 neural detector for semantic attacks.
  3. An LLM arbitrator for the final decision.
  - Releases **MCP-AttackBench**: 70,448 samples, augmented with GPT-4.
- **Numbers:** The E5 detector reaches 96.01% accuracy.
- **Overlap:** **Rule, ML and LLM-judge layered detection, plus a large dataset.** This is exactly our layer 2.
- **Novelty threat:** **HIGH.** It already shows multi-stage rule → neural → LLM detection for MCP. We differ on version-drift, pinning, capability policy, runtime sandbox and risk fusion.
- **Sources seen:** arXiv v4 abstract snippet.

### [P1-12] MCPSecBench: A Systematic Security Benchmark and Playground for Testing Model Context Protocols
- **Authors and year:** Yixuan Yang, Cuifeng Gao, Daoyuan Wu, Yufan Chen, Yingjiu Li, Shuai Wang (v3 author list; it varies by version). Aug 2025.
- **Status:** arXiv 2508.13220 (v3).
- **What they did:**
  - 17 attack types across 4 surfaces: client, protocol, server, host.
  - A modular playground with prompt datasets, servers, clients, attack scripts, a GUI harness, and protection mechanisms.
  - Tested Claude, OpenAI and Cursor.
- **Numbers:**
  - v2: over 85% of attacks compromise at least one platform.
  - v3: existing protections average under 30% success.
- **Overlap:** Benchmark; evaluates existing defenses.
- **Novelty threat:** **Low–Medium.**
- **Sources seen:** arXiv v2/v3 abstract snippets.

### [P1-13] MindGuard: Tracking, Detecting, and Attributing MCP Tool Poisoning Attack
- **Later title:** "MindGuard: Intrinsic Decision Inspection for Securing LLM Agents Against Metadata Poisoning".
- **Authors and year:** USTC and Beihang University; names UNVERIFIED. 2025 (v1–v3).
- **Status:** arXiv 2508.20412.
- **What they did:**
  - A decision-level guard.
  - Builds a Decision Dependence Graph from LLM attention and detects poisoned invocations with an "Anomalous Influence Rate".
  - Attributes each invocation to the poisoned tool.
- **Numbers:**
  - v1/v3: 94–99% average precision; 95–100% attribution accuracy.
  - v3 adds: under 1 s, no extra token cost.
  - Another version: AP above 97.6%; attribution above 98.6%.
- **Limitations:** Needs model internals (open weights only), as noted by later papers.
- **Overlap:** Detection of tool poisoning, but white-box.
- **Novelty threat:** **Medium.** A different mechanism; it does not apply to closed models behind a gateway.
- **Sources seen:** arXiv v1/v2/v3 abstract snippets.

### [P1-14] MCP-ITP: An Automated Framework for Implicit Tool Poisoning in MCP
- **Authors and year:** Ruiqi Li, Zhiqiang Wang, Yunhao Yao, Xiang-Yang Li (USTC). 12 Jan 2026.
- **Status:** arXiv 2601.07395.
- **What they did:**
  - Implicit poisoning: the poisoned tool is never called, but its metadata steers the agent to misuse a legitimate high-privilege tool.
  - An attacker / detector / evaluator LLM loop optimises the poison to evade detectors (black-box optimisation).
- **Numbers:** [secondary, CSA note] 84.2% ASR, with detection suppressed to 0.3% across 12 agents.
- **Overlap:** Adversarial, detector-evasion data. A strong stress test for our "unseen pattern" RQ.
- **Novelty threat:** **Low** as competition; **high relevance** as an adversary.
- **Sources seen:** arXiv abstract snippet; Promptfoo DB; CSA research note.

### [P1-15] Securing the Model Context Protocol: Defending LLMs Against Tool Poisoning and Adversarial Attacks
- **Later title:** "Semantic Attacks on Tool-Augmented LLMs: Securing the MCP Against Descriptor-Level Manipulation".
- **Authors and year:** Saeid Jamshidi and 5 co-authors (Polytechnique Montréal, Concordia, Brock). 6 Dec 2025.
- **Status:** arXiv 2512.06556.
- **What they did:**
  - Defines 3 semantic attacks: descriptor poisoning, shadowing via shared context, and **post-approval descriptor change (rug pull)**.
  - Defense with three parts: (1) **cryptographic signing of tool manifests**; (2) an **LLM-based descriptor review**; (3) lightweight runtime guardrails.
- **Numbers:** [secondary] 72.2% block rate against tool poisoning; about 1.5 s added latency — unconfirmed.
- **Overlap:** **Signatures + LLM-judge + runtime guardrails + rug pull.** This covers 3 of our 5 layers.
- **Novelty threat:** **HIGH.** The closest preprint to our architecture. We must show what it lacks: version-to-version semantic drift scoring, an explicit capability policy, a sandbox behaviour monitor with anomaly detection, weighted risk fusion, ablation, and a public labelled dataset. Verify against the full text.
- **Sources seen:** arXiv abs v1 and retitled PDF listing (search snippets).

### [P1-16] Machine Learning-Based Detection of MCP Attacks
- **Authors and year:** Tobias Mattsson, Samuel Nyberg, Anton Borg, Ricardo Britto (BTH and Ericsson). 12 Apr 2026.
- **Status:** arXiv 2604.10534.
- **What they did:**
  - Supervised traditional and deep models (SVC, BERT, BiLSTM, etc.) to classify **malicious MCP tool descriptions**.
  - Binary task, plus a multiclass task that identifies the attack type.
  - Compared against a rule-based YARA baseline.
- **Numbers:**
  - Dataset: 1,440 unique tool descriptions; 10 attack types + benign.
  - Abstract: binary F1 of 100% for several models; multiclass F1 of 90.56% (SVC) and 88.33% (BERT).
  - [secondary] YARA: 69.01% accuracy, 31.25% F1.
- **Overlap:** **Exactly our ML-classifier baseline and labelled SAFE/POISONED dataset.**
- **Novelty threat:** **HIGH for layer 2 alone.** A simple classifier on descriptions is already done and saturated (100% F1). That suggests the dataset is easy. Our contribution must be harder generalisation (unseen patterns, adversarial MCP-ITP-style) plus drift and fusion.
- **Sources seen:** arXiv abstract snippet; secondary review.

### [P1-17] Model Context Protocol Threat Modeling and Analyzing Vulnerabilities to Prompt Injection with Tool Poisoning
- **Authors and year:** Charoes Huang, Xin Huang, Ngoc Phu Tran, Amin Milani Fard (NYIT). 23 Mar 2026.
- **Status:** arXiv 2603.22489.
- **What they did:**
  - STRIDE and DREAD threat modelling over 5 components (host/client, LLM, server, data stores, authorization server).
  - Client-side focus, using tool poisoning as the main attack.
  - Proposes (but does not implement, as far as seen) a multi-layer defense: static metadata analysis, decision-path tracking, behavioural anomaly detection, user transparency.
- **Numbers:** Not seen.
- **Overlap:** Proposes a layered design close to ours (static, behavioural anomaly).
- **Novelty threat:** **Medium.** It is a proposal; check whether it has an implementation.
- **Sources seen:** arXiv abstract snippet; emergentmind.

### [P1-18] When MCP Servers Attack: Taxonomy, Feasibility, and Mitigation
- **Authors and year:** Names UNVERIFIED in the snippets. Sept 2025.
- **Status:** arXiv 2509.24272. Press coverage in Help Net Security, 16 Oct 2025.
- **What they did:**
  - Treats MCP servers as active threat actors.
  - Component-based taxonomy of 12 attack categories, with proof-of-concept servers per category.
  - Tested across hosts and LLMs.
  - Shows malicious servers can be generated at scale at almost no cost, and that existing scanners are insufficient. Scanners missed deceptive text and fake metadata.
- **Overlap:** Evidence that metadata/code consistency checks are needed.
- **Novelty threat:** **Low–Medium.**
- **Sources seen:** arXiv HTML snippet; Help Net Security article snippet.

### [P1-19] From Component Manipulation to System Compromise: Understanding and Detecting Malicious MCP Servers
- **Authors and year:** Huang et al. (Fudan University). 2026.
- **Status:** arXiv 2604.01905.
- **What they did:**
  - Proof-of-concept dataset of 114 malicious servers.
  - Tested on 2 hosts and 5 LLMs; multi-component attack chains beat single-component attacks.
  - Detector **Connor**: stage 1 performs pre-execution shell-command checks and extracts each tool's intended function; stage 2 traces runtime behaviour and flags **deviation from that intent**.
- **Numbers:**
  - F1 of 94.6%, beating prior state of the art by 8.9–59.6%.
  - Found 2 malicious servers in the wild.
- **Overlap:** **Static analysis + runtime behaviour monitoring (intent vs behaviour)**; dataset.
- **Novelty threat:** **HIGH for layer 4.** Runtime-behaviour-vs-declared-intent is done. Our Docker sandbox plus Isolation Forest must be positioned against Connor.
- **Sources seen:** alphaxiv/huggingface abstract snippets.

### [P1-20] Beyond the Protocol: Unveiling Attack Vectors in the Model Context Protocol (MCP) Ecosystem
- **Authors and year:** Hao Song, Yiming Shen, et al. June 2025.
- **Status:** arXiv 2506.02040.
- **What they did:** Presented as the first systematic study of MCP-ecosystem attack vectors, including malicious external resources and invisible prompts in fetched web content.
- **Numbers:** Not seen.
- **Overlap:** Taxonomy and attacks.
- **Novelty threat:** **Low.**
- **Sources seen:** arXiv and papers.cool snippets.

### [P1-21] A First Look at the Security Issues in the Model Context Protocol Ecosystem
- **v1 title:** "Toward Understanding Security Issues in the MCP Ecosystem".
- **Authors and year:** Xiaofan Li, Xing Gao (University of Delaware). 18 Oct 2025.
- **Status:** arXiv 2510.16558. The later PDF thanks a "shepherd and anonymous reviewers", which implies acceptance at a peer-reviewed venue, but the **venue is UNVERIFIED**.
- **What they did:**
  - Ecosystem measurement of 67,057 servers from 6 registries: mcp.so, MCP Market, MCP Store, Pulse MCP, Smithery, npm.
  - Unvetted submission enables server hijacking.
  - Credential leakage; attacker-controlled metadata shapes LLM reasoning.
- **Overlap:** Ecosystem measurement; motivates integrity and provenance.
- **Novelty threat:** **Low.** A motivation citation.
- **Sources seen:** arXiv snippets.

### [P1-22] Attested Tool-Server Admission: A Security Extension to the Model Context Protocol
- **Authors and year:** Alfredo Metere (Enclawed LLC). 2026.
- **Status:** arXiv 2605.24248. Mentions a companion SEP #2809 — unverified.
- **What they did:**
  - Offline-signed clearance statement at a well-known URI, checked against a pinned trust root.
  - Deny-by-default per-server tool allowlist.
  - An enforcement mode, and a tamper-evident audit log.
  - Implemented as `mcp-attested`.
- **Overlap:** **Signatures, pinning, allowlist policy.**
- **Novelty threat:** **Medium–High for layers 1 and 3.** Another signed-admission design.
- **Sources seen:** arXiv and chatpaper snippets.

### [P1-23] MCP-38: A Comprehensive Threat Taxonomy for Model Context Protocol Systems (v1.0)
- **Status:** arXiv 2603.18063. Authors UNVERIFIED.
- **What they did:** 38 threat categories, mapped to STRIDE and OWASP.
- **Novelty threat:** **Low** (taxonomy only).
- **Sources seen:** arXiv snippet.

### [P1-24] MCP-DPT: A Defense-Placement Taxonomy and Coverage Analysis for Model Context Protocol Security
- **Status:** arXiv 2604.07551. Authors and content details UNVERIFIED; title only seen.
- **Novelty threat:** **Low–Medium** — it may map which layers existing defenses cover. Read it.

### [P1-25] A Formal Security Framework for MCP-Based AI Agents: Threat Taxonomy, Verification Models, and Defense Mechanisms ("MCPSHIELD")
- **Status:** arXiv 2604.05969.
- **What they did:** Notes that MCP security research is fragmented across individual attack papers, isolated benchmarks and point defenses, and proposes a formal framework.
- **Novelty threat:** **Medium** (unverified details).
- **Sources seen:** alphaxiv and catalyzex snippets.

### [P1-26] Other MCP-detection preprints surfaced (titles seen; details UNVERIFIED)
- **ChainWatch: A Kill Chain-Aligned Sequential Detection Framework for Multi-Step Attacks in MCP-Based AI Agent Systems** — arXiv 2607.19432. A snippet says it critiques MindGuard, MCPShield and MCP-Guard for single-call threat models. Runtime sequential detection. Threat: **Medium**.
- **Content-Aware Attack Detection in LLM Agent Tool-Call Traffic: An Empirical Study of Features, Architectures, and Evaluation Protocols** — arXiv 2605.11053. Black-box detection on tool-call content. Threat: **Medium** for the ML layer.
- **Stealthy injection payloads through MCP tool responses** — arXiv 2603.24203 (Fudan). The snippet shows an IEEE TDSC template header; **acceptance in TDSC is UNVERIFIED**.
- **MCPShield** — named in the ChainWatch snippet as an existing MCP defense. Paper identity UNVERIFIED.

---

## Section E — Leads not verified (search budget ran out; check these next)

Each of these is a plausible MCP-security work named in the task brief or seen only in passing. **Nothing about them is claimed.**

| Lead | What still needs checking |
|---|---|
| MCPLib | Existence, authors, venue |
| "Systematic analysis of MCP security" | Exact title and arXiv ID |
| ToolHijacker (prompt injection on tool selection) | Reported as NDSS 2026 — verify |
| "Attractive Metadata Attack" (tool-metadata manipulation) | Possibly NeurIPS 2025 — verify |
| ToolTweak / tool-selection manipulation papers | Existence and venue |
| MCP ecosystem/registry studies at MSR / ICSE / FSE / ASE 2026 | Titles, e.g. maintainability and security of MCP servers on GitHub |
| SMCP / "Secure MCP" protocol extensions | Existence |
| MCP-RiskCue | Existence |
| MCP-Shield or MCP-Scan academic write-ups | Existence |
| MCP papers in IEEE Access, Computers & Security, Future Internet, Electronics, Information, Applied Sciences | Any matching article |
| MCP-Universe / MCP-Bench | Not security work; skip unless needed for utility baselines |
| arXiv 2512.08290 | Seen only as an ID; title unknown |
| CSA "ShareLock: Stealthy Multi-Tool Threshold Poisoning in MCP" (June 2026) | Industry research note, not peer-reviewed; may cite an underlying paper |
| Shiqiang Chen, "Empirical Study of MCP Server Security: 6 Attack Surfaces from 30+ Audits" | HuggingFace artifact, not peer-reviewed |

---

## Coverage matrix

**Legend:** ✔ = covered (per abstract); ~ = partial or proposed without evaluation; blank = not seen.

**Columns:**
- **INT** = integrity / hash or version pinning
- **SIG** = signatures
- **RULE/ML** = rule or classifier / semantic detection
- **LLMJ** = LLM-judge detection
- **DRIFT** = semantic drift between versions
- **POL** = capability policy
- **RT** = runtime monitoring / sandbox
- **RISK** = risk scoring / fusion
- **DATA** = dataset or benchmark
- **ABL** = ablation
- **LAT** = latency measured

| ID | Work | Venue | INT | SIG | RULE/ML | LLMJ | DRIFT | POL | RT | RISK | DATA | ABL | LAT |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| P1-01 | Hou et al. landscape | TOSEM / FSE-JF | | | | | | | | | | | |
| P1-02 | MCPTox | AAAI'26 | | | | | | | | | ✔ | | |
| P1-03 | MPMA | AAAI'26 | | | | | | | | | ~ | | |
| P1-04 | MCP-SafetyBench | ICLR'26 | | | | | | | | | ✔ | | |
| P1-05 | MSB | ICLR'26 | | | | | | | | | ✔ | | |
| P1-06 | MCIP | EMNLP'25 | | | ✔ (guard model) | | | | ~ (tracking logs) | | ✔ | | |
| P1-07 | ShieldMCP | ACL'26 Ind. | ? | ? | ✔ | ? | | ? | ✔ | ? | | | ✔ |
| P1-08 | MCP Safety Audit | arXiv | | | | ~ (agentic audit) | | | | | | | |
| P1-09 | Enterprise-Grade MCP | arXiv | ~ | ~ | ~ | | | ~ | ~ | ~ | | | |
| P1-10 | ETDI | arXiv | ✔ | ✔ | | | | ✔ | | | | | |
| P1-11 | MCP-Guard | arXiv | | | ✔ | ✔ | | | | | ✔ (70k) | ? | ? |
| P1-12 | MCPSecBench | arXiv | | | | | | | ~ | | ✔ | | |
| P1-13 | MindGuard | arXiv | | | ✔ (white-box) | | | | ✔ | | | | ✔ |
| P1-14 | MCP-ITP | arXiv | | | (evasion) | | | | | | ✔ (adv.) | | |
| P1-15 | Jamshidi et al. | arXiv | ✔ (rug pull) | ✔ | | ✔ | | | ✔ | | ? | ? | ✔ (secondary) |
| P1-16 | ML-based detection | arXiv | | | ✔ | | | | | | ✔ (1,440) | | |
| P1-17 | Huang et al. STRIDE | arXiv | | | ~ | | | | ~ | | | | |
| P1-18 | When MCP Servers Attack | arXiv | | | | | | | | | ✔ (PoCs) | | |
| P1-19 | Connor | arXiv | | | ✔ (static) | ✔ (intent extraction) | | | ✔ | | ✔ (114) | | |
| P1-20 | Beyond the Protocol | arXiv | | | | | | | | | | | |
| P1-21 | Li & Gao ecosystem | arXiv (venue?) | | | | | | | | | ✔ (measurement) | | |
| P1-22 | Attested admission | arXiv | ✔ | ✔ | | | | ✔ | | | | | |
| P1-23 | MCP-38 | arXiv | | | | | | | | | | | |
| P1-25 | MCPSHIELD formal | arXiv | ? | ? | ? | ? | | ? | ? | | | | |
| P1-26 | ChainWatch | arXiv | | | ✔ | | | | ✔ (sequential) | | | | |

"?" = not determinable from the abstract snippets; check the full text.

---

## What no MCP paper has done yet (evidence-limited)

Based **only** on the abstracts and snippets seen above — the full texts were not readable — none of the confirmed works reports:

1. **Semantic drift between a trusted and a received version of the same tool description** as a learned or measured signal. That means embedding distance used to separate benign updates from poisoned rug-pull updates.
   - ETDI, P1-15 and P1-22 detect *any* change through signatures or versions, which forces re-approval.
   - None quantifies *whether a change is malicious*. This is the strongest novelty angle (our RQ2).
2. **One gateway that combines all five layers** (integrity, signatures, semantic/ML detection with LLM judge, explicit capability policy, sandboxed runtime monitoring) **with a fused risk score (ALLOW/REVIEW/BLOCK)** and **a layer-by-layer ablation**.
   - P1-15 covers signing + LLM review + guardrails.
   - P1-11 covers rule + neural + LLM.
   - P1-19 covers static + runtime.
   - ShieldMCP covers runtime interception.
   - None was seen reporting a full ablation across integrity, semantic, policy and runtime layers.
3. **A dataset of legitimate version changes paired with poisoned version changes.** Existing datasets (MCPTox, MCP-AttackBench, the 1,440-description set, 114 malicious servers) label static descriptions or servers, not *pairs of versions*.
4. **Generalisation tests of description classifiers against adaptive, evasion-optimised poisons** (MCP-ITP-style) and implicit poisoning.
   - P1-16 reports a saturated 100% binary F1, which suggests in-distribution evaluation.
   - Cross-dataset or unseen-pattern evaluation was not seen in any abstract.
5. **A false-positive-rate vs detection trade-off and per-layer latency budget, published together for a gateway.** ShieldMCP reports median latency and ASR reduction, but no FPR on benign tool churn was seen.

**Caveat:** Points 1–5 must be re-checked against the full texts of P1-07 (ShieldMCP), P1-11 (MCP-Guard), P1-15 (Jamshidi et al.), P1-19 (Connor), P1-25 and P1-26, and against the Section E leads, before they are claimed in a paper.
