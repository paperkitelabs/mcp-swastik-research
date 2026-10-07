# Step 2 — Area P3: Defenses for Prompt Injection and Tool-Using LLM Agents

Compiled 2026-10-07. Scope: detection (guard models/classifiers), training/prompt-level defenses, system/architectural defenses for agents, runtime monitoring/permission systems, and journal literature.

## Read this first: what was verified and what was not

- **How things were checked.** Each entry below rests on WebSearch result snippets that this agent actually saw. The snippets came from arXiv listings, ACL Anthology, PMLR/mlanthology, icml.cc/neurips.cc, usenix.org, ndss-symposium.org, the NSF PAR repository and Penn State Pure. **WebFetch was egress-blocked for every domain tried in this session**, so no full text or table was read directly. These domains were tried: arxiv.org, aclanthology.org, usenix.org, ndss-symposium.org, proceedings.mlr.press, sciencedirect.com, huggingface.co, ceur-ws.org, api.semanticscholar.org and journal.hep.com.cn. As a result:
  - The "Key numbers" field gives only figures that appeared in the search snippets, which usually come from the abstract. Check them against the PDF before citing.
  - All page numbers and DOIs come from search snippets. Each one is marked as such.
- **Search budget.** Partway through, the shared 200-call WebSearch budget ran out. The journal-specific sweep (part e) is therefore **incomplete**. Searches for TIFS, TDSC and generic ScienceDirect returned **no confirmed Q1/Q2 journal article on prompt-injection defense**. That is a gap in coverage. It is not evidence that no such article exists. Searches for ACM CSUR, Information Fusion, ESWA, KBS, Neurocomputing, IEEE Access, JISA and FGCS were **not run**. They should be run in a follow-up session.
- **Tiers.** CORE ranks and SJR quartiles are **per general knowledge, not checked on portal.core.edu.au or scimagojr.com** (both were unreachable or not attempted) unless stated otherwise. Verify them before using them in the paper.
- **UNVERIFIED items.** A few well-known items the task named (Llama Guard, Prompt Guard, perplexity filters, BIPIA, GenTel-Safe, AgentSentinel) could not be confirmed by any search this session because the budget was gone. They are listed in Appendix B with the label **UNVERIFIED** and minimal detail.

---

## (a) Detection-based defenses (guard models, classifiers, detectors)

### [P3-01] DataSentinel: A Game-Theoretic Detection of Prompt Injection Attacks
- Yupei Liu, Yuqi Jia, Jinyuan Jia, Dawn Song, Neil Zhenqiang Gong | 2025 | IEEE Symposium on Security and Privacy (S&P 2025) (peer-reviewed conference) | pp. 2190–2208 (per the NSF PAR listing in the search snippet)
- Tier: CORE A* (per general knowledge — verify)
- Link: arXiv 2504.11358; NSF PAR record par.nsf.gov/biblio/10633541; code in the Open-Prompt-Injection GitHub repo (per snippet)
- What they did: Builds on known-answer detection, where a detection LLM is told to output a secret "known answer". If the answer is missing, the input contained an injection. They fine-tune the detection LLM so it holds up against adaptive injections designed to evade it. Training is framed as a minimax game and solved by alternating gradient-based inner-max and outer-min steps. They evaluate across several benchmark datasets and LLMs against both existing and adaptive attacks.
- Key numbers: none seen in snippets.
- Limitations: The S&P meta-review, quoted in a snippet, notes the defense may weaken as LLMs follow instructions better. An adaptive attack could get the model to return the known answer *and* follow the injection. Inputs are text data prompts, not tool metadata.
- Informs: semantic detector. **Baseline candidate** for a "detector over tool descriptions" comparison. Feed the description in as the data and run known-answer detection on it.
- Verified: search snippets (arXiv, NSF PAR, PSU Pure).

### [P3-02] Attention Tracker: Detecting Prompt Injection Attacks in LLMs
- Kuo-Han Hung, Ching-Yun Ko, Ambrish Rawat, I-Hsin Chung, Winston H. Hsu, Pin-Yu Chen | 2025 | Findings of the Association for Computational Linguistics: NAACL 2025 (peer-reviewed; Findings track) | pp. 2309–2322
- Tier: NAACL main is commonly CORE A. Findings papers are usually counted below main-track papers (per general knowledge — verify).
- DOI: 10.18653/v1/2025.findings-naacl.123; arXiv 2411.00348
- What they did: Describes a "distraction effect": some "important heads" shift attention from the original instruction to the injected one. They build a training-free detector that scores attention on the instruction region and needs no extra LLM inference.
- Key numbers: an AUROC improvement of up to 10.0% over existing methods (abstract); works on small LLMs.
- Limitations: It needs white-box access to attention, so it cannot run on closed API models. Like most work here, it is evaluated on prompts and data, not on tool metadata.
- Informs: semantic detector (white-box signal). Usable as a **baseline** only if the gateway runs an open-weights model.
- Verified: search snippets (ACL Anthology preview pages, arXiv).

### [P3-03] PIGuard: Prompt Injection Guardrail via Mitigating Overdefense for Free (preprint title: InjecGuard)
- Hao Li, Xiaogeng Liu, Chaowei Xiao (InjecGuard preprint authors; PIGuard author list on ACL Anthology not fully seen) | 2025 | Proceedings of the 63rd Annual Meeting of the ACL (Long Papers), ACL 2025 (peer-reviewed) | anthology ID 2025.acl-long.1468
- Tier: ACL is CORE A* (per general knowledge — verify)
- Link: aclanthology.org/2025.acl-long.1468; arXiv 2410.22770 (InjecGuard); code at GitHub leolee99/PIGuard; model at Hugging Face leolee99/PIGuard (DeBERTa-v3-base)
- What they did: Identifies **over-defense**: guard models flag benign inputs that contain "trigger words". They release NotInject, a benign dataset full of trigger words, to measure it. They propose MOF ("Mitigating Over-defense for Free") training to reduce trigger-word bias. The result is a lightweight DeBERTa guard trained on open data.
- Key numbers: SOTA guards fall to about 60% accuracy on NotInject, near random. PIGuard beats the best existing model by 30.4% on NotInject. The InjecGuard v2 preprint reports 30.8% over the open-source runner-up, against a different baseline set.
- Limitations: It is an input-text classifier trained on prompt-style injections, with no tool-metadata data. Over-defense, meaning false positives, is the stated core problem. This maps directly onto our RQ4 (detection vs FPR).
- Informs: semantic detector. **Strong baseline**: open model, open data, and the same encoder class as a plausible gateway ML classifier. NotInject is a template for building a "benign-but-scary tool descriptions" FPR test set.
- Verified: search snippets (ACL Anthology, papers.cool, arXiv, HF model card listing, Mozilla any-guardrail docs).

### [P3-04] Embedding-based classifiers can detect prompt injection attacks
- Md. Ahsan Ayub, Subhabrata Majumdar | 2024 | CAMLIS 2024 (Conference on Applied Machine Learning in Information Security). Published in CEUR-WS Vol-3920, paper 15. The snippets show the CEUR URL and say "presented at CAMLIS'24".
- Tier: Applied security ML conference, **not CORE-ranked as far as known**. Treat it as a peer-reviewed workshop/conference-level venue (verify).
- Link: arXiv 2410.22284; ceur-ws.org/Vol-3920/paper15.pdf
- What they did: Embeds benign and malicious prompts with three common embedding models (including OpenAI embeddings) and trains classic ML classifiers on them (RF, XGBoost and others). They compare against open-source encoder-based PI classifiers.
- Key numbers: the best is Random Forest on OpenAI embeddings, with AUC 0.764, precision 0.867 and recall 0.87. A secondary summary says the dataset has 467,057 unique prompts, of which 109,934 are malicious (secondary, verify).
- Limitations (stated): no clear linear separation in the visualizations; focused on **direct** prompt injection only; NN classifiers on embeddings left to future work.
- Informs: semantic detector. This is the **closest published analogue to the proposal's "sentence-embedding + classifier" layer**, so it is a **direct baseline**. Note that it classifies one text at a time. It does not measure *drift* between a trusted and a received description.
- Verified: search snippets (arXiv, CEUR URL, PromptLayer).

### [P3-05] PromptArmor: Simple yet Effective Prompt Injection Defenses
- Tianneng Shi + 15 co-authors (UC Berkeley, UCSB, Duke, NUS, et al.) | 2025 | **arXiv preprint** 2507.15219 (no venue seen)
- Tier: none (preprint)
- Link: arXiv 2507.15219
- What they did: Uses an off-the-shelf LLM as a pre-filter that detects injected instructions in the agent's input and **removes** them before the agent sees the input. No fine-tuning is needed. They test adaptive attacks and several prompting strategies. They propose PromptArmor as a standard baseline for future defenses.
- Key numbers: on AgentDojo, with GPT-4o, GPT-4.1 or o4-mini as the guard, FPR and FNR are both below 1%, and ASR after removal is below 1% (abstract).
- Limitations: Each input costs a frontier-LLM call, which adds latency and cost (our RQ5). Details of the adaptive-attack evaluation were not seen.
- Informs: semantic detector (LLM-as-judge). It is the **LLM-judge baseline** to set against our cheap TF-IDF and embedding detectors, and the authors explicitly ask for this comparison.
- Verified: search snippets (arXiv HTML/abs).

### [P3-06] Formalizing and Benchmarking Prompt Injection Attacks and Defenses
- Yupei Liu, Yuqi Jia, Runpeng Geng, Jinyuan Jia, Neil Zhenqiang Gong | 2024 | 33rd USENIX Security Symposium (peer-reviewed) | pp. 1831–1847
- Tier: CORE A* (per general knowledge — verify)
- Link: usenix.org/conference/usenixsecurity24/presentation/liu-yupei; arXiv 2310.12815; platform at GitHub Open-Prompt-Injection
- What they did: A formal framework for prompt injection, under which existing attacks are special cases, plus a new combined attack. They systematically evaluate **5 attacks and 10 defenses across 10 LLMs and 7 tasks**. Defenses include prevention-style and detection-style approaches, among them known-answer detection, which DataSentinel later hardened.
- Key numbers: 5 attacks × 10 defenses × 10 LLMs × 7 tasks.
- Limitations (stated): existing defenses fall short. The setting is LLM-integrated apps, not agents or tool metadata.
- Informs: evaluation methodology and the semantic detector. **The Open-Prompt-Injection toolkit gives ready-made detector baselines.**
- Verified: search snippets (usenix.org, arXiv, PSU Pure).

### [P3-07] Fine-tuned Large Language Models (LLMs): Improved Prompt Injection Attacks Detection
- Authors not captured in snippets (UNVERIFIED) | 2025 | IEEE COMPSAC 2025 (peer-reviewed IEEE conference) | DOI 10.1109/COMPSAC65507.2025.00134 (per snippet)
- Tier: COMPSAC is commonly CORE B (per general knowledge — verify)
- Link: arXiv 2410.21337; NSF PAR 10621471
- What they did: Fine-tunes a pre-trained LLM as a binary prompt-injection detector on a labeled dataset.
- Key numbers: accuracy 99.13%, precision 100%, recall 98.33%, F1 99.15% (on the authors' own dataset).
- Limitations: Near-perfect in-distribution scores suggest dataset-specific evaluation. No adaptive or out-of-distribution test was seen. The inputs are prompts.
- Informs: semantic detector. A possible fine-tuned-classifier baseline. Its in-distribution-only evaluation motivates our "unseen-pattern generalization" experiment.
- Verified: search snippets (NSF PAR, arXiv).

### [P3-08] PIShield: Detecting Prompt Injection Attacks via Intrinsic LLM Features
- Penn State and Duke authors (names not captured, UNVERIFIED) | 2025 | **arXiv preprint** 2510.14005
- Tier: none (preprint; venue not seen)
- What they did: Takes the internal representation of the final prompt token at one particular LLM layer and trains a detector on it, since that representation separates clean prompts from contaminated ones. Motivation: existing detectors have sub-optimal accuracy and/or high overhead.
- Key numbers: not seen.
- Limitations: white-box access needed.
- Informs: semantic detector (representation probe). Could be an optional baseline.
- Verified: search snippets (arXiv).

### [P3-09] Other recent detectors seen only as titles (arXiv preprints; details not verified)
- PromptSleuth: Detecting Prompt Injection via Semantic Intent Invariance (arXiv 2508.20890)
- PVDetector: Detecting Prompt Injection Attacks on Purpose-Specific LLM Agents through Policy-Violation Concept Analysis (arXiv 2607.12624)
- BASIS: Breach-Aware Selective Prompt Injection Shielding with Prefill Attention Probes (arXiv 2608.08027). The snippet says existing detectors "only detect the presence of injection and refuse … causing over-refusal".
- Prompt Attack Detection with LLM-as-a-Judge and Mixture-of-Models (arXiv 2603.25176)
- Send a SCOUT First: Pre-hoc Reasoning for Adaptive Detector Allocation in Prompt-Injection Defense (arXiv 2605.30837)
- PromptLocate (localizing injected prompts). It appeared only as a reference entry listing IEEE S&P 2026. **Venue UNVERIFIED.**
- "Attention is All You Need to Defend Against Indirect Prompt Injection Attacks in LLMs". It appeared only as a reference entry listing NDSS 2026. **Venue UNVERIFIED.**
- Use: related-work completeness only. Do not cite numbers.

---

## (b) Training-level and prompt-level defenses

### [P3-10] StruQ: Defending Against Prompt Injection with Structured Queries
- Sizhe Chen, Julien Piet, Chawin Sitawarin, David Wagner | 2025 | 34th USENIX Security Symposium (peer-reviewed)
- Tier: CORE A* (per general knowledge — verify)
- Link: usenix.org/conference/usenixsecurity25/presentation/chen-sizhe; arXiv 2402.06363; code at GitHub Sizhe-Chen/StruQ
- What they did: Separates instructions and data into distinct channels. A trusted front-end puts the prompt and data into a special delimited format. A model trained with "structured instruction tuning" ignores instructions in the data part, using training data augmented with injected instructions inside the data.
- Key numbers: not seen beyond the qualitative claim of security against a wide class of human-crafted (adaptive and non-adaptive) injections, better robustness to optimization-based attacks, and minimal utility impact.
- Limitations: Requires fine-tuning the model, which is not possible in a gateway in front of third-party clients. Optimization-based attacks are only "improved", not solved. Tool descriptions sit in the *system/instruction* channel in MCP, so the trust separation does not cover poisoned metadata out of the box.
- Informs: conceptually, the policy layer, through the principle "capabilities from trusted channel only". It is **not a gateway baseline**. Cite it as model-side prior art.
- Verified: search snippets (usenix.org, arXiv).

### [P3-11] SecAlign: Defending Against Prompt Injection with Preference Optimization
- Sizhe Chen, Arman Zharmagambetov, Saeed Mahloujifar, Kamalika Chaudhuri, David Wagner, Chuan Guo | 2025 | ACM SIGSAC Conference on Computer and Communications Security (CCS '25), Taipei (peer-reviewed)
- Tier: CORE A* (per general knowledge — verify)
- DOI: 10.1145/3719027.3744836; arXiv 2410.05451
- What they did: Builds a preference dataset of injected inputs paired with a secure response (follows the legitimate instruction) and an insecure one (follows the injection), then preference-optimizes the LLM.
- Key numbers: the arXiv v3 abstract reports ASR below 10% (8% on the strongest tested attack) with utility largely preserved. v2 claimed about 0%. Cite the published version.
- Limitations: a secondary summary notes weakness against architecture-aware and RL-based adversaries. Model-side only.
- Informs: model-level prior art, not a gateway baseline.
- Verified: search snippets (arXiv, aihub.org).

### [P3-12] Meta SecAlign: A Secure Foundation LLM Against Prompt Injection Attacks
- Sizhe Chen, Arman Zharmagambetov, David Wagner, Chuan Guo (Meta FAIR, UC Berkeley) | 2025 | **arXiv preprint** 2507.02735 (v1–v3; no venue seen)
- What they did: Releases open-weight Meta-SecAlign-8B and -70B models trained with an improved SecAlign recipe, with the full recipe published.
- Key numbers: a secondary (machine-generated) summary mentions 9 utility and 7 security benchmarks, including tool-invocation and web-agent tasks. Not verified.
- Limitations: FAIR non-commercial license. Model-side.
- Informs: an **optional end-to-end baseline**. Run an MCP client on Meta-SecAlign and measure whether poisoned descriptions still succeed. This shows whether a robust model alone is enough without a gateway.
- Verified: search snippets (arXiv).

### [P3-13] The Instruction Hierarchy: Training LLMs to Prioritize Privileged Instructions
- Eric Wallace, Kai Xiao, Reimar Leike, Lilian Weng, Johannes Heidecke, Alex Beutel (OpenAI) | 2024 | **arXiv preprint** 2404.13208 (industry; no venue seen)
- What they did: Defines a privilege hierarchy (system > user > tool outputs/third-party). Trains GPT-3.5 with synthetic data to ignore lower-privilege instructions that conflict with higher-privilege ones, rather than refusing all embedded instructions.
- Key numbers: qualitative only ("drastically increases robustness … minimal degradations").
- Limitations: In MCP, tool *descriptions* are typically injected at system or developer privilege by the client. Poisoned metadata may therefore inherit **high** privilege, which is the core reason a hierarchy alone does not solve tool poisoning. This is our own analysis, not a claim from the paper.
- Informs: motivation for the policy layer (descriptions must not grant capabilities). Not a baseline.
- Verified: search snippets (arXiv, Simon Willison blog).

### [P3-14] Defending Against Indirect Prompt Injection Attacks With Spotlighting
- Keegan Hines, Gary Lopez, Matthew Hall, Federico Zarfati, Yonatan Zunger, Emre Kıcıman (Microsoft) | 2024 | arXiv 2403.14720. A version is in CEUR-WS Vol-3920 (paper03), the same volume as P3-04, which suggests CAMLIS 2024. **Venue link to CAMLIS UNVERIFIED.**
- What they did: Prompt-engineering transformations of untrusted input (delimiting, datamarking, encoding) so the model can track provenance.
- Key numbers: ASR fell from over 50% to under 2% on GPT-family models with little task-performance impact (MSR page snippet).
- Limitations: a secondary review says encoding works only with high-capacity models. Google DeepMind's "Lessons from Defending Gemini" (arXiv 2505.14534) re-implements it with control tokens. It does not address metadata that the client places in trusted context.
- Informs: a cheap **prompt-level baseline**. The gateway could "spotlight" tool descriptions before forwarding them, which gives an ablation arm.
- Verified: search snippets (arXiv, MSR, CEUR URL).

### [P3-15] Defense Against Prompt Injection Attack by Leveraging Attack Techniques
- Yulin Chen, Haoran Li, Zihao Zheng, Dekai Wu, Yangqiu Song, Bryan Hooi | 2025 | ACL 2025 Long Papers (peer-reviewed) | anthology ID 2025.acl-long.897
- Tier: CORE A* (per general knowledge — verify)
- What they did: Repurposes attack techniques, the structure of injection prompts, as defensive prompt templates around the legitimate instruction.
- Key numbers: "significantly reduces ASR, sometimes to near zero, while maintaining accuracy" (qualitative, from snippet).
- Limitations: a prompt-level defense, likely brittle to adaptive attacks (see P3-16).
- Informs: prompt-level baseline family. Not central to us.
- Verified: search snippet (ACL Anthology preview).

### [P3-16] Adaptive Attacks Break Defenses Against Indirect Prompt Injection Attacks on LLM Agents
- Authors not captured (UNVERIFIED) | 2025 | Findings of NAACL 2025 (peer-reviewed) | anthology ID 2025.findings-naacl.395
- What they did: Shows that existing IPI defenses for agents were not tested against adaptive attacks and can be broken by them.
- Key numbers: not seen.
- Limitations and gap: a **core methodological warning**. Any detector we propose must be evaluated against adaptive or paraphrased poisoning (our "unseen-pattern" RQ).
- Informs: evaluation design for all layers.
- Verified: search snippet (ACL Anthology PDF listing).

### [P3-17] Other training- and inference-time defenses seen only as titles (arXiv)
- Defending Against Prompt Injection With a Few DefensiveTokens (arXiv 2507.07974)
- SecInfer: Preventing Prompt Injection via Inference-time Scaling (arXiv 2509.24967)
- Defending Against Prompt Injection with DataFilter (arXiv 2510.19207)
- SecOPD: Mitigating Adaptive Prompt Injections by On-Policy Distillation (arXiv 2608.21500)
- Prompt Control-Flow Integrity: A Priority-Aware Runtime Defense Against Prompt Injection in LLM Systems (arXiv 2603.18433)
- Beyond Over-Refusal: Defending Indirect Prompt Injection via Latent Instruction Manifolds (arXiv 2608.22248)
- arXiv 2504.20472 (attention- and instruction-awareness analysis: models "are aware of which specific instructions they are executing")
- Details not verified. Cite only after reading.

---

## (c) System-level and architectural defenses for agents

### [P3-18] CaMeL — Defeating Prompt Injections by Design
- Edoardo Debenedetti et al. (Google, Google DeepMind, ETH Zurich) | 2025 | **arXiv preprint** 2503.18813 (v1 March 2025; later revisions). **No peer-reviewed venue seen.** It is used as a reading in MIT 6.858 (2026).
- What they did: A protective system layer around an *unmodified* LLM. A privileged LLM turns the trusted user query into a program (control and data flow). A quarantined LLM parses untrusted data without tool access. A custom Python interpreter tracks provenance with **capabilities** and enforces security policies at tool-call time, which blocks exfiltration over unauthorized flows.
- Key numbers: on AgentDojo, it solves 77% of tasks with provable security versus 84% undefended (v2). v1 said 67%.
- Limitations (stated): some utility loss. Policies are hand-written. It defends the *data* channel. **Tool metadata is assumed trusted**, since the P-LLM sees tool descriptions when planning. A poisoned description therefore reaches the privileged planner, which is our own reading and should be verified in the paper.
- Informs: policy checker (capabilities from explicit policy) and runtime monitor (tool-call-time enforcement). **Architectural baseline and comparison point**, with code at GitHub google-research/camel-prompt-injection.
- Verified: search snippets (arXiv-derived summaries, MIT course PDF URL).

### [P3-19] IsolateGPT: An Execution Isolation Architecture for LLM-Based Agentic Systems
- Yuhao Wu, Franziska Roesner, Tadayoshi Kohno, Ning Zhang, Umar Iqbal | 2025 | Network and Distributed System Security Symposium (NDSS 2025) (peer-reviewed) | DOI 10.14722/ndss.2025.241131
- Tier: CORE A* (per general knowledge — verify)
- Link: ndss-symposium.org paper page; arXiv 2403.04960 (earlier title SecGPT)
- What they did: Hub-and-spoke architecture. Each third-party app gets its own LLM instance in an isolated "spoke", and mutually untrusting apps communicate only through a hub-mediated inter-spoke protocol with well-defined requests.
- Key numbers: overhead under 30% for three-quarters of tested queries, and "no loss of functionality" (abstract).
- Limitations: **ACE (P3-20) later showed attacks on IsolateGPT, including "Planner Manipulation via malicious app descriptions"**, which is exactly tool-description poisoning.
- Informs: runtime isolation and the policy layer. It is an architectural reference. As a baseline it is heavy, but code is available, including a LlamaIndex Llama Pack.
- Verified: search snippets (NDSS page, arXiv, WashU news).

### [P3-20] ACE: A Security Architecture for LLM-Integrated App Systems
- Authors not captured (Northeastern University "Security of LLM Agents" project page appears; UNVERIFIED author list) | 2026 | NDSS Symposium 2026 (peer-reviewed). Search results show an ndss-symposium.org paper page and the PDF "2026-s352-paper.pdf"; the year is inferred from that file name.
- Tier: CORE A* (per general knowledge — verify)
- Link: arXiv 2504.20984
- What they did: First shows new attacks on IsolateGPT: Execution Flow Disruption and Execution Manager Hijack through malicious app outputs, and **Planner Manipulation through malicious app descriptions**. It then proposes Abstract-Concrete-Execute. (1) An abstract plan is generated from the trusted query alone, using abstract apps that have a name, description and type signature but no implementation. (2) That plan is instantiated with concrete apps. (3) Execution is isolated, with data and capability barriers. Static analysis checks plans against user-specified secure information-flow constraints.
- Key numbers: secure against InjecAgent and Agent Security Bench IPI attacks and its own new attacks; utility measured on the LangChain Tool Usage suite (no numbers seen).
- Limitations: The concrete-instantiation step still has to read third-party app descriptions. How ACE handles poisoned descriptions at that stage needs a full-text check.
- Informs: **the most directly relevant peer-reviewed system paper for tool-description poisoning**. It shows that malicious descriptions are a recognized attack vector in A*-venue work. Relevant to the policy layer and the risk engine.
- Verified: search snippets (arXiv, NDSS page URL, Moonlight summary).

### [P3-21] System-Level Defense against Indirect Prompt Injection Attacks: An Information Flow Control Perspective (f-secure LLM system)
- Fangzhou Wu, Ethan Cecchetti, Chaowei Xiao | 2024 | **arXiv preprint** 2409.19091. An OpenReview PDF appears in the results, but no acceptance was seen.
- What they did: Uses IFC to formalize an "f-secure" LLM system in which the planner only sees trusted information and an executor handles untrusted data (per a secondary summary).
- Limitations: details were not verified, because only references and a secondary summary were seen.
- Informs: the policy layer's theoretical framing.
- Verified: search snippets (arXiv, PromptLayer summary).

### [P3-22] Securing AI Agents with Information-Flow Control (FIDES)
- Manuel Costa, Boris Köpf + 7 co-authors (Microsoft) | 2025 | **arXiv preprint** 2505.23643 (v1 May 2025, v2 Sep 2025); MSR publication page
- What they did: A formal model of agent planners that characterizes what dynamic taint-tracking can enforce. FIDES is a variable-passing planner that attaches confidentiality and integrity labels to data and enforces policies deterministically, with selective hide and reveal primitives. Includes a task taxonomy for security/utility trade-offs.
- Key numbers: AgentDojo evaluation (no numbers seen).
- Limitations: Microsoft Research commentary in another paper says such deterministic IFC defenses "currently appear costly", with lower task completion and more tokens.
- Informs: policy checker and risk engine (labels as risk features). Code at GitHub microsoft/fides (MIT).
- Verified: search snippets (arXiv, MSR page, ecosyste.ms).

### [P3-23] RTBAS: Defending LLM Agents Against Prompt Injection and Privacy Leakage
- CMU and Two Sigma authors (names not captured; UNVERIFIED) | 2025 | **arXiv preprint** 2502.08966 (CMU PDL hosts the PDF)
- What they did: Fine-grained dynamic IFC for tool-using agents. Two "dependency screeners" decide which data influences each step: an LLM-as-judge screener and an attention-score screener. Labels propagate only through relevant data, and irrelevant data is redacted. The goal is to avoid asking the user to confirm every tool call.
- Key numbers: prevents all targeted attacks on AgentDojo with a 2% utility loss under attack; near-oracle privacy-leak detection (abstract).
- Limitations: depends on how accurate the screeners are, so there is no hard guarantee.
- Informs: risk engine (selective confirmation instead of blanket confirmation corresponds to our REVIEW tier) and runtime monitor.
- Verified: search snippets (arXiv, CMU PDL).

### [P3-24] Progent: Programmable Privilege Control for LLM Agents
- Tianneng Shi et al. incl. Wenbo Guo, Dawn Song (UC Berkeley, UCSB, NUS) — **full author list UNVERIFIED** | 2025 | **arXiv preprint** 2504.11703 (v1 Apr, v2 Aug 2025); **no venue confirmed**
- What they did: Presents itself as the first privilege-control framework for LLM agents. A DSL expresses fine-grained tool-call policies (allow/deny on tools and arguments), enforced deterministically at runtime. Policies can be written by hand or generated by an LLM.
- Key numbers: not seen in snippets.
- Limitations: not verified from full text.
- Informs: **the policy checker directly** ("capabilities come from explicit policy, not descriptions"). It is a **strong baseline candidate for the policy layer** if code is available (not confirmed).
- Verified: search snippets (arXiv, HF papers).

### [P3-25] DRIFT: Dynamic Rule-Based Defense with Injection Isolation for Securing LLM Agents
- Hao Li, Xiaogeng Liu, Hung-Chun Chiu, Dianqi Li, Ning Zhang, Chaowei Xiao | 2025 | NeurIPS 2025 (peer-reviewed; poster)
- Tier: CORE A* (per general knowledge — verify)
- Link: neurips.cc/virtual/2025/poster/116028; arXiv 2506.12104; code at GitHub SaFoLab-WISC/DRIFT
- What they did: A Secure Planner builds a minimal function trajectory and a JSON parameter checklist from the query. A Dynamic Validator checks deviations against privilege limits and user intent. An Injection Isolator masks conflicting instructions held in memory.
- Key numbers: evaluated on AgentDojo and ASB with "strong security and high utility" (no numbers seen).
- Limitations (stated motivation): static policies cannot be updated dynamically, and memory streams are not isolated. Tool metadata trust was not discussed in snippets.
- Informs: policy checker (dynamic rules) and runtime monitor (deviation detection). **Baseline with code.**
- Verified: search snippets (NeurIPS page, mlanthology, arXiv).

### [P3-26] MELON: Provable Defense Against Indirect Prompt Injection Attacks in AI Agents
- Kaijie Zhu, Xianjun Yang, Jindong Wang, Wenbo Guo, William Yang Wang | 2025 | ICML 2025, PMLR 267:80310–80329 (peer-reviewed)
- Tier: CORE A* (per general knowledge — verify)
- Link: proceedings.mlr.press/v267/zhu25z.html; arXiv 2502.05174; code at GitHub kaijiezhu11/MELON
- What they did: A training-free detector. It re-executes the agent trajectory with a **masked user prompt** and flags an attack when the tool calls from the original and masked runs are similar, since under attack the agent's actions no longer depend on the user task. Three design choices reduce FP and FN. MELON-Aug adds prompt augmentation.
- Key numbers: a secondary (alphaXiv) summary reports 0.32% ASR on GPT-4o (not verified against tables).
- Limitations: re-execution roughly doubles inference cost (latency, our RQ5). The "provable" claim was not checked.
- Informs: runtime monitor (behavioral, tool-call-level detection). **Baseline with code** on AgentDojo.
- Verified: search snippets (PMLR, ICML virtual, mlanthology, arXiv).

### [P3-27] The Task Shield: Enforcing Task Alignment to Defend Against Indirect Prompt Injection in LLM Agents
- Feiran Jia, Tong Wu, Xin Qin, Anna Squicciarini | 2025 | ACL 2025 Long Papers, pp. 29680–29697 (peer-reviewed)
- DOI: 10.18653/v1/2025.acl-long.1435; arXiv 2412.16682
- Tier: CORE A* (per general knowledge — verify)
- What they did: A test-time defense that checks whether each instruction and tool call contributes to the user's goals, reframing security as task alignment.
- Key numbers: on AgentDojo with GPT-4o, ASR is 2.07% and utility 69.79% (abstract).
- Limitations: an LLM-based checker, which adds cost and can be attacked adaptively. It needs an explicit user task.
- Informs: runtime monitor and policy checker. A tool whose *description* tries to induce calls unrelated to the task would be flagged at runtime. **Baseline candidate.**
- Verified: search snippets (ACL Anthology, arXiv).

### [P3-28] GuardAgent: Safeguard LLM Agents via Knowledge-Enabled Reasoning
- Zhen Xiang, Linzhi Zheng, + 10 co-authors | 2025 | ICML 2025, PMLR vol. 267 (peer-reviewed)
- Tier: CORE A* (per general knowledge — verify)
- Link: icml.cc/virtual/2025/poster/46569; arXiv 2406.09187; guardagent.github.io
- What they did: A guard agent turns natural-language safety requests into a task plan and then into **guardrail code** that is executed to deterministically check the target agent's actions. An LLM with memory-retrieved demonstrations does the reasoning.
- Key numbers: guardrail accuracy above 98% on EICU-AC (healthcare access control) and above 83% on Mind2Web-SC (web agent safety).
- Limitations: an LLM generates the code, so code correctness is a risk. The benchmarks target access control and safety, not prompt injection or metadata.
- Informs: policy checker (policy turned into executable checks).
- Verified: search snippets (ICML, mlanthology, arXiv).

### [P3-29] ShieldAgent: Shielding Agents via Verifiable Safety Policy Reasoning
- Zhaorun Chen, Mintong Kang, Bo Li | 2025 | ICML 2025, PMLR 267: 8313–8344 (peer-reviewed)
- Tier: CORE A* (per general knowledge — verify)
- Link: icml.cc/virtual/2025/poster/45989; arXiv 2503.22738
- What they did: A guardrail agent extracts verifiable safety rules from regulations and policy documents, groups them by action, and checks each action of the protected agent with logical reasoning and verification tools. It releases ShieldAgent-Bench: 3K instruction-trajectory pairs, 6 web environments, 7 risk categories.
- Key numbers: +11.3% over prior methods on average, recall 90.1%, 64.7% fewer API queries and 58.2% less inference time (arXiv version).
- Limitations: built for web-agent safety-policy compliance, not metadata poisoning.
- Informs: policy checker and risk engine.
- Verified: search snippets (ICML, mlanthology, arXiv).

### [P3-30] AgentSpec: Customizable Runtime Enforcement for Safe and Reliable LLM Agents
- Haoyu Wang, Christopher M. Poskitt, Jun Sun (SMU) | 2026 | ICSE 2026 (IEEE/ACM International Conference on Software Engineering), Rio de Janeiro (peer-reviewed; per SMU news and InK repository)
- Tier: CORE A* (per general knowledge — verify)
- Link: arXiv 2503.18666; ink.library.smu.edu.sg/sis_research/10278
- What they did: A lightweight DSL for runtime rules made of a *trigger event*, a *predicate* and an *enforcement action* (block, ask the user, LLM self-reflection), applied to code agents, embodied agents and autonomous vehicles. Rules can be LLM-generated.
- Key numbers: o1-generated rules reached 95.56% precision and 70.96% recall for embodied agents; 87.26% of risky code flagged; violations prevented in 5 of 8 AV scenarios.
- Limitations: rules need domain authoring. Recall for LLM-generated rules is moderate.
- Informs: **policy checker and runtime monitor (trigger-predicate-action matches the gateway's ALLOW/REVIEW/BLOCK)**. A strong conceptual baseline.
- Verified: search snippets (arXiv, SMU).

### [P3-31] Contextual Agent Security: A Policy for Every Purpose (Conseca)
- Lillian Tsai, Eugene Bagdasarian (Google) | 2025 | HotOS 2025 (ACM Workshop on Hot Topics in Operating Systems; **peer-reviewed workshop**) | DOI 10.1145/3713082.3730378
- Tier: workshop (highly selective, but not a full conference; not CORE-ranked as a conference). Verify.
- Link: arXiv 2501.17070 (earlier title "Context is Key for Agent Security")
- What they did: Argues that static hand-written policies and user-confirmation prompts do not scale. Proposes generating **just-in-time, contextual, human-verifiable policies** with a trusted LLM given only trusted context, then enforcing them deterministically.
- Key numbers: a secondary summary mentions a 20-task case study (not verified).
- Limitations (stated future work): policies over action *sequences*; caching policies to reduce runtime overhead.
- Informs: policy checker (where policies come from).
- Verified: search snippets (arXiv, research.google, HotOS slides).

### [P3-32] Design Patterns for Securing LLM Agents against Prompt Injections
- Luca Beurer-Kellner + 13 co-authors (Invariant Labs, IBM, EPFL, ETH Zurich, Google, Microsoft, et al.) | 2025 | **arXiv preprint** 2506.08837 (v1–v3, June 2025)
- What they did: Describes six architectural patterns, including action-selector, plan-then-execute, map-reduce, dual LLM, code-then-execute and context-minimization (pattern names per general knowledge; only "plan-then-execute" and "six patterns" were seen in snippets). Applies them to ten case studies, from OS assistants to SWE agents.
- Limitations: a critic (Armosec blog, Aug 2026) argues that the patterns stop injected text from choosing actions but still let it influence the *arguments and contents* of permitted actions.
- Informs: overall gateway design rationale (policy plus least privilege). Not a baseline. Notably, the first author's organization, Invariant Labs, is the one that publicized MCP tool poisoning, so this paper is a natural bridge citation.
- Verified: search snippets (arXiv, Simon Willison).

### [P3-33] AgentArmor: Enforcing Program Analysis on Agent Runtime Trace to Defend Against Prompt Injection
- Authors UNVERIFIED | 2025 | **arXiv preprint** 2508.01249
- What they did (from snippet): Applies program analysis to agent runtime traces. It critiques prior IFC systems for operating "over ad-hoc data structures rather than structured representations".
- Informs: runtime monitor (trace analysis). Optional.
- Verified: search snippet only.

### [P3-34] Lessons from Defending Gemini Against Indirect Prompt Injections
- Google DeepMind | 2025 | **arXiv/industry report** 2505.14534
- What they did (from snippet): Describes production defenses, including a spotlighting variant with control tokens, and evaluation against adaptive attacks.
- Informs: industrial evidence that layered defenses are needed. Not a baseline.
- Verified: search snippet only.

---

## (d) Runtime monitoring, sandboxing and permission systems

Peer-reviewed work found this session that sits closest to "runtime monitor / permission system for LLM apps and plugins": IsolateGPT (P3-19, per-app isolation), ACE (P3-20, capability barriers), MELON (P3-26, behavioral tool-call comparison), Task Shield (P3-27), AgentSpec (P3-30, runtime enforcement DSL), Progent (P3-24, privilege control), GuardAgent and ShieldAgent (P3-28/29), and RTBAS (P3-23, selective confirmation). **No paper found this session evaluates OS-level sandboxing of the tool *server process*, with file and network monitoring plus anomaly detection such as Isolation Forest, for MCP or plugin servers.** This looks like a genuine gap for our layer 4. The budget cut off a targeted search, so state it as "not found in our search", not "does not exist".

---

## (e) Journal papers (Q1/Q2) — status

### [P3-35] Prompt Injection Attacks on Large Language Models: A Survey of Attack Methods, Root Causes, and Defense Strategies
- Tongcheng Geng, Zhiyuan Xu, Yubin Qu, W. Eric Wong | 2025/2026 | **Journal**. DOI 10.32604/cmc.2025.074081 points to *Computers, Materials & Continua* (Tech Science Press), hosted via ScienceDirect (pii S1546221826001384).
- Tier: CMC's SJR quartile is **not verified**. Per general knowledge it has been around Q2–Q3 in some categories; check scimagojr.com. The journal has also faced past indexing scrutiny, so check its current Scopus/WoS status before relying on it.
- What they did: Synthesizes 128 peer-reviewed studies (2022–2025) on attacks, root causes and defenses.
- Key numbers: input-preprocessing defenses reach 60–80% detection rates, with significant gaps against novel attack vectors. Standardized evaluation frameworks are limited.
- Informs: related-work framing and the gap statement.
- Verified: search snippet (ScienceDirect listing).

### [P3-36] Prompt Injection Detection in LLM Integrated Applications
- Authors UNVERIFIED | 2025 | *International Journal of Network Dynamics and Intelligence* (IJNDI), vol. 4, issue 2 | DOI 10.53941/ijndi.2025.100013
- Tier: **SJR quartile unknown, likely not Q1** (verify). A new journal.
- What they did: A banned-terms list, similarity search and a BERT classifier, combined for real-time injection neutralization.
- Informs: semantic detector. A **rules + similarity + BERT stack, structurally close to our layer 2**, so it is useful as a related-work comparator.
- Verified: search snippet only.

### [P3-37] Prompt Injection Attacks in LLMs and AI Agent Systems: A Comprehensive Review of Vulnerabilities, Attack Vectors, and Defense Mechanisms
- Authors UNVERIFIED | 2025 preprint (Preprints.org 202511.0088). The snippet says it was later in *Information* (MDPI) 2026. **Journal publication UNVERIFIED.**
- Tier: MDPI *Information* is commonly Q2–Q3 (per general knowledge — verify).
- Key claims: covers more than 120 papers from 2023–2025 and concludes that defense-in-depth is required.
- Informs: supports the layered-gateway motivation (RQ3).
- Verified: search snippet only.

**Journal sweep status:** searches of IEEE TIFS and TDSC returned no confirmed 2024–2026 prompt-injection *defense* article. A TIFS snippet mentioned only a VLM jailbreak (attack) paper. ACM CSUR, Information Fusion, ESWA, KBS, Neurocomputing, IEEE Access, JISA, FGCS, Computers & Security and ACM TOPS were **not searched** because the budget ran out. **Action item for the next session:** run venue-filtered searches (e.g., `site:sciencedirect.com "prompt injection" "Computers & Security"`, IEEE Xplore with a TIFS/TDSC filter, `dl.acm.org/journal/csur "prompt injection"`). Observation, to be checked: this literature is overwhelmingly published at A*/A conferences and on arXiv, with few Q1 journal papers so far. That is itself a useful positioning argument for a Q1 journal submission.

---

## Appendix A — arXiv/industry items cited above (non-peer-reviewed at time of search)
CaMeL (2503.18813), PromptArmor (2507.15219), Meta SecAlign (2507.02735), Instruction Hierarchy (2404.13208), Spotlighting (2403.14720; CEUR version), f-secure IFC (2409.19091), FIDES (2505.23643), RTBAS (2502.08966), Progent (2504.11703), Design Patterns (2506.08837), PIShield (2510.14005), AgentArmor (2508.01249), Gemini lessons (2505.14534), plus the title-only lists in P3-09 and P3-17.

## Appendix B — UNVERIFIED items named in the task (no search confirmation this session; budget exhausted)
- **Llama Guard** (Meta, 2023; arXiv 2312.06674): an LLM-based input/output safety classifier. **UNVERIFIED this session.** It targets content-safety taxonomies, not injection specifically.
- **Prompt Guard / Llama Prompt Guard (86M, mDeBERTa-based; Meta 2024; later Prompt Guard 2)**: a lightweight jailbreak/injection classifier. **UNVERIFIED this session** (HF fetch blocked). Very likely a usable off-the-shelf baseline for layer 2.
- **Perplexity filters**: Alon & Kamfonas, "Detecting Language Model Attacks with Perplexity" (arXiv 2308.14132), and Jain et al., "Baseline Defenses for Adversarial Attacks Against Aligned Language Models" (arXiv 2309.00614). **UNVERIFIED this session.** These mainly target gibberish adversarial suffixes, so they are weak against fluent natural-language poisoning in descriptions.
- **BIPIA** (Yi et al., benchmark and defenses for indirect prompt injection; reportedly KDD 2025): **UNVERIFIED**.
- **GenTel-Safe** (unified benchmark and shielding framework, 2024): **UNVERIFIED**.
- **AgentSentinel**: no information found; **UNVERIFIED**, do not cite until located.

---

## Defense categories vs our gateway layers (table)

| Defense category | Representative works (IDs) | Integrity checker (hash/sign) | Semantic poisoning detector | Policy/permission checker | Runtime behavior monitor | Risk engine |
|---|---|---|---|---|---|---|
| Fine-tuned classifier guards | PIGuard/InjecGuard (03), COMPSAC FT-LLM (07), Prompt Guard (App. B) | – | **Direct** (baseline) | – | – | score input |
| Embedding + classic ML | Ayub & Majumdar (04), IJNDI (36) | – | **Direct** (closest analogue) | – | – | score input |
| Known-answer / game-theoretic detection | Open-Prompt-Injection (06), DataSentinel (01) | – | Direct | – | – | score input |
| White-box internal-signal detectors | Attention Tracker (02), PIShield (08) | – | Direct (needs open model) | – | – | score input |
| LLM-as-judge filter | PromptArmor (05), Task Shield (27), RTBAS screener (23) | – | Direct (costly) | partial | Task Shield at runtime | score input |
| Model-level training | StruQ (10), SecAlign (11), Meta SecAlign (12), Instr. Hierarchy (13) | – | – (model-side) | conceptual | – | – |
| Prompt-level transforms | Spotlighting (14), attack-technique defense (15) | – | ablation arm | – | – | – |
| Isolation architectures | IsolateGPT (19), ACE (20) | – | – | **Direct** | **Direct** (isolation) | – |
| Plan/execute separation and capabilities | CaMeL (18), f-secure (21), Design Patterns (32), DRIFT (25) | – | – | **Direct** | deviation checks | – |
| IFC / taint labels | FIDES (22), RTBAS (23), CaMeL (18) | – | – | **Direct** | label tracking | labels as features |
| Privilege / policy DSLs | Progent (24), AgentSpec (30), Conseca (31) | – | – | **Direct** (baseline) | enforcement | action → ALLOW/REVIEW/BLOCK |
| Guard agents | GuardAgent (28), ShieldAgent (29) | – | partial | **Direct** | **Direct** | verdicts |
| Behavioral re-execution | MELON (26) | – | – | – | **Direct** (baseline) | score |
| **Metadata integrity / rug-pull pinning** | *None found in P3 literature* | **Gap: ours** | – | – | – | – |
| **Description drift (trusted vs received)** | *None found* | – | **Gap: ours** | – | – | – |
| **Tool-server process sandbox + anomaly detection** | *None found* | – | – | – | **Gap: ours** | – |

---

## Candidate baselines for experiments (with code/model availability, where a snippet showed it)

| Baseline | Layer compared | Availability seen | Notes on fit |
|---|---|---|---|
| PIGuard / InjecGuard (P3-03) | Semantic detector | Code at GitHub leolee99/PIGuard; model at HF leolee99/PIGuard (DeBERTa-v3-base) | Best open classifier baseline. Its NotInject methodology fits an FPR study. |
| Embedding + RF/XGBoost (P3-04) | Semantic detector | Method described; code not confirmed | Re-implement easily with our sentence encoders. Closest analogue. |
| Known-answer detection / DataSentinel (P3-01, P3-06) | Semantic detector | Open-Prompt-Injection GitHub (per snippet) | Treat the tool description as "data". |
| PromptArmor-style LLM judge (P3-05) | Semantic detector | Method is prompting an off-the-shelf LLM; code not confirmed | Upper-bound accuracy vs latency and cost (RQ5). |
| Attention Tracker (P3-02) | Semantic detector (white-box) | Code availability not confirmed | Only with an open-weights client model. |
| Prompt Guard (App. B) | Semantic detector | UNVERIFIED this session | Common industry baseline; verify the model card. |
| MELON (P3-26) | Runtime monitor | Code at GitHub kaijiezhu11/MELON | Tool-call-level behavioral baseline on AgentDojo. |
| DRIFT (P3-25) | Policy + runtime | Code at GitHub SaFoLab-WISC/DRIFT | Dynamic policy baseline. |
| CaMeL (P3-18) | Policy + capabilities | Code at GitHub google-research/camel-prompt-injection | Architectural comparison. Check whether it trusts tool descriptions. |
| FIDES (P3-22) | Policy / IFC | Code at GitHub microsoft/fides (MIT) | IFC comparison. |
| Task Shield (P3-27) | Runtime alignment | Code not confirmed | AgentDojo numbers available for comparison. |
| Spotlighting (P3-14) | Prompt-level ablation | Simple to re-implement | A "gateway spotlights descriptions" arm. |
| Meta SecAlign-8B (P3-12) | End-to-end (robust model, no gateway) | Weights released (FAIR non-commercial) | Tests whether a robust model alone suffices. |
| IsolateGPT (P3-19) | Isolation architecture | Open-sourced; LlamaIndex pack | Heavy. Mainly a qualitative comparison. |

Benchmarks used across this literature (useful for a cross-check, not for metadata): AgentDojo (CaMeL, MELON, Task Shield, PromptArmor, FIDES, RTBAS, DRIFT), ASB / Agent Security Bench (DRIFT, ACE), InjecAgent (ACE), NotInject (PIGuard), ShieldAgent-Bench, EICU-AC / Mind2Web-SC (GuardAgent).

---

## Gaps stated across this literature (and gaps implied for our proposal)

1. **Detectors are trained and evaluated on prompts and data, not on tool metadata.** Every detector seen (P3-01–08) classifies user prompts or retrieved data. None reports evaluation on tool names, descriptions or input schemas. Our labeled SAFE/POISONED tool-definition dataset fills that gap. (Observation from all abstracts seen; confirm in full texts.)
2. **Over-defense / false positives.** PIGuard (P3-03) shows SOTA guards drop to about 60% accuracy on benign inputs containing trigger words. Tool descriptions legitimately contain imperative words ("must", "always", "ignore"), so FPR is a central risk, which supports RQ4.
3. **Adaptive attacks.** The NAACL Findings 2025 paper (P3-16) shows that IPI defenses for agents break under adaptive attacks. The DataSentinel meta-review raises the same concern, and SecAlign is weak against RL and architecture-aware adversaries. Our "unseen-pattern generalization" experiment should include adaptive or paraphrased poisoning.
4. **Utility and cost trade-offs.** CaMeL drops from 84% to 77% task success. Deterministic IFC is "costly" (FIDES commentary). MELON doubles execution. PromptArmor and Task Shield need LLM calls per step. This supports measuring latency (RQ5) and favoring cheap layers first.
5. **Tool metadata is implicitly trusted by system-level defenses.** CaMeL, f-secure and plan-then-execute patterns plan from the trusted query *plus tool descriptions*. ACE (P3-20, NDSS 2026) explicitly demonstrates **Planner Manipulation via malicious app descriptions** against IsolateGPT. This is the strongest peer-reviewed evidence that description poisoning defeats architectural defenses, and it motivates our integrity and semantic layers *in front of* the planner.
6. **No temporal integrity (rug-pull) handling.** No defense found pins or signs tool definitions or detects post-approval changes (our RQ1/RQ2). This needs confirming against the P1/P2 MCP-specific literature from other agents.
7. **Static vs dynamic policies.** DRIFT and Conseca say static policies don't adapt. Conseca lists sequence-level policies and policy caching as open problems. Our policy layer should state how it handles this.
8. **White-box dependence.** Attention Tracker, PIShield and RTBAS's attention screener need model internals, which a gateway in front of closed clients usually lacks. This argues for black-box text and embedding detectors at the gateway.
9. **Weak journal presence.** Venue-filtered searches found no Q1 journal paper on prompt-injection or agent-tool defense. The only journal items were a CMC survey and an IJNDI detector, both of uncertain quartile. The search was incomplete because of the budget, so this is an opportunity to verify, not a finding.
10. **Process-level runtime sandboxing of tool servers** (file and network syscall monitoring, anomaly detection) was not found in the P3 defense literature. Agent "runtime monitors" here operate on LLM actions and tool calls, not on server-process behavior.
