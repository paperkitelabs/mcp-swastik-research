# Step 3: Gap Analysis and Refined Problem Statement

**Project:** MCP Tool-Description Poisoning: Detection and Prevention
**Compiled:** 7 October 2026
**Inputs:**
- Step 1 (`01_Step1_Problem_Landscape/`): practitioner needs, incidents, spec status, product matrix.
- Step 2 (`02_Step2_Literature/`): 52 journal papers, 75 top-conference papers, 13 workshop papers, 30 novelty-threat preprints. IDs such as J-04, C-06 and A-01 refer to that catalogue.

**Ground rule for this document:** every gap claim cites the evidence behind it and states its **confidence**. Confidence is limited by the fact that, in this stage, papers were assessed from **abstracts and indexed summaries, not full texts**. Each gap therefore has a "verify in Step 4" item (§8).

---

## 1. What the existing work already covers

### 1.1 Coverage matrix: closest works × proposed layers

Legend:
- ✔ = covered (per abstract or documentation); ~ = proposed or partial, without evaluation; blank = not seen; ? = not determinable from the abstract.
- **INT** = hash/version pinning, **SIG** = signatures, **SEM** = rule/ML/LLM detection on metadata, **DRIFT** = analysing *what changed* between a trusted and a received version, **POL** = explicit capability policy, **RT** = runtime monitoring, **RISK** = fused/calibrated scoring, **DATA** = labelled dataset or benchmark, **ABL** = per-layer ablation, **FPR@base** = false-positive rate at realistic prevalence, **ADV** = adaptive/paraphrase robustness, **LAT** = latency.

| Work | Status | INT | SIG | SEM | DRIFT | POL | RT | RISK | DATA | ABL | FPR@base | ADV | LAT |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Hou et al. (J-01) | TOSEM | | | | | | | | | | | | |
| Huang et al. (J-04) | JCP (MDPI) 2026 | | | ~ | | | ~ | | ~ (client tests) | | | | |
| Gasmi et al. (J-02) | Information Sciences | | | | | | | | ✔ (3,250 attacks) | | | | |
| MCPTox (C-01) | AAAI'26 | | | | | | | | ✔ | | | | |
| MSB (C-04) | ICLR'26 | | | | | | | | ✔ | | | | |
| MCIP (C-05) | EMNLP'25 | | | ✔ (guard) | | | ~ | | ✔ | | | | |
| ShieldMCP (C-06) | ACL'26 Industry | ? | ? | ✔ | | ? | ✔ | ? | | | | | ✔ (<120 ms) |
| Jamshidi et al. (A-01) | arXiv | ✔ (rug pull) | ✔ | ✔ (LLM review) | | | ✔ | | ? | ? | | | ~ |
| MCP-Guard (A-02) | arXiv | | | ✔ (rule→E5→LLM) | | | | | ✔ (70k) | ? | | | ? |
| ETDI (A-03) | arXiv | ✔ | ✔ | | | ✔ | | | | | | | |
| ML detection (A-04) | arXiv | | | ✔ | | | | | ✔ (1,440) | | | | |
| Connor (A-05) | arXiv | | | ✔ (static) | | | ✔ (intent vs behaviour) | | ✔ (114 servers) | | | | |
| TRUSTDESC (A-08) | arXiv | | | (regenerates descriptions) | | | | | | | | | |
| Enterprise-Grade (A-13) | arXiv | ~ | ~ | ~ | | ~ | ~ | ~ | | | | | |
| Attested Admission (A-14) | arXiv | ✔ | ✔ | | | ✔ | | | | | | | |
| mcp-scan v0.3 / Snyk Agent Scan | product | ✔ (exact hash, v0.3 only) | | ✔ | | ~ | ~ | ✔ (0–1000) | | | | | |
| Cisco mcp-scanner, Lasso, Docker, ToolHive | products | | ✔ (images) | ✔ (some) | | ✔ (some) | ✔ (some) | ~ | | | | | |
| **Original proposal (uploaded docx)** | – | ✔ | ~ | ✔ | ~ (whole-text cosine) | ✔ | ✔ | ~ (fixed bands) | synthetic | ✔ planned | – | ~ ("unseen patterns") | ✔ planned |

Sources: Step 2 §3.1 and Appendix A; Step 1 §5; detailed P1 coverage matrix in `02_Step2_Literature/annex_detailed_area_reports/P1_MCP_specific_literature.md`.

### 1.2 What this means

| Component | Status | Evidence |
|---|---|---|
| Hash pinning (INT), signing (SIG) | Done; **not novel** | ETDI (A-03), Jamshidi (A-01), Attested Admission (A-14), mcp-scan v0.3, Microsoft registry plan. Plus classical theory: TUF (C-41), Sigstore (C-43), in-toto (C-42). |
| Static description classifiers (SEM) | Done, including multi-stage rule→neural→LLM | A-02, A-04, MCIP (C-05), ShieldMCP (C-06) |
| Runtime "declared intent vs observed behaviour" (RT) | Done in a preprint | Connor (A-05) |
| A *conceptual* layered MCP gateway | Proposed several times | A-13, J-04, A-01 |

**Consequence:** the original proposal's novelty claim, "a layered framework combining integrity, NLP, policy and runtime monitoring", would be **rejected as not novel** by an informed reviewer. The novelty has to come from somewhere more specific.

---

## 2. Gap analysis

Each gap is listed with its evidence, the closest existing work, and a confidence rating.

### G1. Nobody distinguishes *legitimate* tool-definition updates from *poisoned* ones

**Main opening.**

- **Academic evidence:**
  - Every MCP integrity mechanism found treats *any* change as suspicious: hash or signature mismatch, then re-approval (A-01, A-03, A-14). It does not judge *whether the change is malicious*.
  - Every MCP detector found classifies a **single snapshot** of a description (A-02, A-04, C-05, C-06). None takes the *(trusted version, received version)* pair as input.
  - No MCP paper in the P1 coverage matrix has a DRIFT column entry.
- **Industry evidence:** no product documents semantic drift analysis (Step 1 §5). mcp-scan's exact-hash pinning has since disappeared from its documentation.
- **Practitioner evidence:**
  - Rug-pull detection is the #1 unmet need (16/41 sources).
  - Telling cosmetic from capability-widening change is need #10.
  - Exact-pin alarm rates are reported as high: hash pinning stable on only 4/10 servers (Discussion #2457); artifact pin fires on 74.6% of releases vs 13.0% for capability-expansion alerts (agent-scan#482).
- **Real-world grounding:**
  - **8–10.9% of ~13,000 public endpoints changed their tool inventory or descriptions within days** (Discussion #3303).
  - postmark-mcp was a benign-then-malicious version update.
  - MCPoison (CVE-2025-54136) is "approve once, trust forever".
- **Closest analogues outside MCP:**
  - LastPyMile (C-50) analyses only the delta between source and package and finds most deltas benign. That is for **code**.
  - CADE (C-64) learns drift distances for security samples.
  - npm permission-drift (C-51) flags updates that request new capabilities.
  - None of these handles natural-language instructions consumed by an LLM.
- **Confidence: Medium–High.** The basis is abstracts, product docs and practitioner threads. The full texts of A-01, A-02, C-06 and J-04 must be checked for any version-pair analysis.

### G2. No labelled corpus of version *pairs* (benign update vs poisoned update) drawn from real version histories

- **What existing datasets label:**
  - **static** descriptions: MCPTox 1,497 cases (C-01); MCP-AttackBench 70,448 (A-02); 1,440 descriptions (A-04);
  - **servers**: 114 malicious servers (A-05);
  - **attack scenarios**: MSB 2,000 (C-04); 3,250 (J-02).
- **Missing:** none pairs a trusted version with a benign or poisoned successor, and none uses the **real distribution of legitimate changes**.
- **Practitioner demand:** a community "shared tool-definition drift (rug-pull) test corpus" PR to the MCP spec repo was closed for process reasons (PR #2924).
- **Methodological need:** TESSERACT (C-61) and Arp et al. (C-60/J-31) show that realistic class ratios and time-ordered splits are required for credible security-ML results. Synthetic-only, balanced datasets inflate scores.
- **Confidence: High** for "no public version-pair corpus" (none found in academia, industry or the spec repo).

### G3. Detectors are evaluated in ways that reviewers of top venues reject

- **Saturation signals an easy, in-distribution test:**
  - binary F1 = **100%** on 1,440 descriptions (A-04);
  - 96.01% accuracy (A-02);
  - 99%+ for a fine-tuned prompt-injection detector (W-11).
  - Chakraborty et al. (J-33) and PrimeVul show such scores collapse under de-duplication and realistic splits.
- **False positives dominate in practice but are not measured at realistic prevalence:**
  - a scanner self-reports **~65% detection at 95% FPR** (Discussion #3301);
  - a third-party audit found **~78% of Cisco YARA flags false** (n=33 servers; Step 1 §5);
  - PIGuard (C-28) shows guard models fall to **~60% accuracy** on benign text containing trigger words. Tool descriptions legitimately contain "must", "always" and "before using".
  - Axelsson (J-32): at low base rates, FPR determines usefulness.
- **No adaptive evaluation:**
  - adaptive attacks broke **8/8** IPI defenses (C-13);
  - MCP-ITP (A-07) optimises poisons that suppress detection to 0.3% (secondary figure);
  - ToolHijacker (C-08) defeats DataSentinel, known-answer and perplexity detection.
- **Confidence: High** for the methodological gap (directly visible in the reported numbers).

### G4. The "what should be pinned" question is open and contested

- **The options in use or proposed:**
  - description string only (mcp-scan, per agent-scan#482);
  - full canonical definition (ETDI);
  - capability fingerprint: name + parameter names/types (Discussion #2457);
  - artifact or package (agent-scan#482).
- **Contradictory practitioner numbers:** 4/10 servers stable; 74.6% of releases alarm; only 0.38% of description changes cosmetic.
- **Missing pieces:**
  - **No peer-reviewed study** measures the alarm burden of each granularity on real data.
  - Canonicalisation issues (RFC 8785, cross-language float encoding) were raised in SEP reviews (S10, S41 in Step 1).
- **Confidence: High** that no study exists. This is a cheap but valuable measurement contribution.

### G5. Attack surface beyond the top-level description is under-covered

- **Practitioner evidence:**
  - "100% of the prompt-injection payloads landed through *nested* schema fields" (Discussion #2457; 10 production servers).
  - The server `instructions` field is an open injection issue (spec #3213).
  - SDKs accept zero-width and RTL-override characters in tool names (typescript-sdk#2777).
- **Academic evidence:** the Attractive Metadata Attack (A-10) manipulates schemas. MSB (C-04) includes out-of-scope parameters.
- **What is missing:** detectors in A-02 and A-04 operate on descriptions; whole-schema coverage was not visible in abstracts.
- **Confidence: Medium.** Full texts may show partial schema coverage.

### G6. No calibrated fusion and no per-layer ablation for MCP defenses

- **Proposed but not evaluated:** layered designs in A-13 and J-04 have no quantitative evaluation.
- **Evaluated without per-layer contribution:** A-01, A-02 and C-06 report end results, but per-layer contribution and calibrated thresholds were not visible.
- **The original proposal's 0–30 / 31–70 / 71–100 bands** are the "biased parameter selection" pitfall (J-31). A weighted sum of uncalibrated, heterogeneous scores is not meaningful (C-72).
- **Principled alternatives exist in the literature:**
  - cost-derived thresholds (C-73);
  - classification-with-rejection for the REVIEW band (C-62, C-63);
  - easy- vs hard-to-manipulate feature weighting (C-56).
- **Confidence: Medium.** Check A-01, A-02 and C-06 full texts.

### G7. Journal gap: almost no empirical MCP defense work in Q1/Q2 journals

- Only **four** MCP-specific journal papers were found (J-01 to J-04). They are:
  - a landscape survey (TOSEM);
  - an attack comparison (Information Sciences);
  - a taxonomy (ICT Express);
  - a threat model plus client tests with *proposed* defenses (JCP).
- No Q1/Q2 journal paper was found presenting an **implemented and evaluated** MCP tool-poisoning defense.
- No Q1/Q2 journal paper on prompt-injection detection in **tool metadata** was found either. The journal detection papers found (J-20 to J-23) are about prompts.
- **Confidence: Medium.** Web search indexes journals poorly. Run the direct database queries in Step 2 §5 before stating this in the paper.

### G8. Runtime behaviour verification exists but is not integrated with change analysis

- Connor (A-05) checks behaviour against declared intent per server.
- Practitioners ask to diff *observed behaviour per version* (Discussion #3211; agent-scan#482: "alert on capability expansion — a newly reachable host, a newly read secret").
- **No work links a definition change to a behaviour change across versions.**
- Classical warnings apply:
  - "anomalous ≠ malicious" (C-65);
  - flat features lack causal context (C-74, J-39);
  - plain Docker is a weak isolation boundary for hostile code (P5 annex, unverified sandbox studies).
- **Confidence: Medium.** Treat this as a **secondary** contribution, not the headline.

### G9. LLM-as-judge detectors can be attacked by the very text they judge

- **Evidence:**
  - SocketAI (C-58) uses LLM review for packages. For MCP, the reviewed text is itself an instruction to an LLM.
  - "How Not to Detect Prompt Injections with an LLM" (W-06) shows a structural weakness in known-answer detection.
- **Implication:** any LLM-judge layer must be evaluated against poisons that target the judge.
- **Confidence: Medium.** This is an evaluation requirement rather than a standalone contribution.

---

## 3. Critical assessment of the original proposal

### 3.1 What is strong and should be kept
- A clear and **honest threat model**: the attacker must already control a server or its update path; experiments are simulated. This matches how the threat is documented (Step 1 §2.4).
- A layered design with **explicit policy so that descriptions never grant permissions**. This is supported by ACE (C-32), CaMeL (C-40), Iqbal et al. (W-03) and OWASP LLM06.
- The planned ablation, FPR/FNR and latency metrics, and group-aware split ("without leaking near-duplicate variants"). This is exactly what J-31, C-61 and W-13 recommend.
- The "Scope and Limitations" section already anticipates the novelty risk ("should not claim that the proposed combination is completely new").

### 3.2 What a Q1/A\* reviewer would attack (with the evidence)

| # | Issue in the original proposal | Why it is a problem | Evidence |
|---|---|---|---|
| 1 | Novelty rests on the **combination** of layers | The combination is already proposed or implemented (A-01, A-02, A-13, C-06, J-04) | §1 |
| 2 | **RQ1 is answered by construction.** A SHA-256 hash detects 100% of byte changes. | The real question is the **false-alarm burden** of legitimate changes and *what* to pin | G4; Step 1 §4.1-3 |
| 3 | Semantic drift = **whole-description cosine similarity** | A short appended exfiltration clause barely moves the cosine of a long description, while a benign rewrite can move it a lot | C-67 caution; P5 annex pitfall 6 |
| 4 | **Synthetic, roughly balanced SAFE/POISONED dataset** | Spatial bias and artefact learning; saturated scores (cf. A-04 at 100% F1) | C-61, J-31, J-33 |
| 5 | **Fixed risk bands (0–30/31–70/71–100) and hand-set weights** | Uncalibrated fusion; data snooping if tuned on test data | C-72, C-73, C-62, J-31 |
| 6 | TF-IDF+LR and embedding baselines only | Reviewers will expect comparison with **PIGuard (C-28), LLM Guard/Vigil (J-21), an LLM judge (A-27), mcp-scan / Cisco scanner**, and ideally MCP-Guard (A-02) | Step 2 §3.3 |
| 7 | Runtime layer = Docker + Isolation Forest | Overlaps Connor (A-05). Anomaly ≠ malicious. Docker is not a strong boundary. | C-65, J-39, A-05 |
| 8 | "Unseen patterns" mentioned but no **adaptive attacker** | Adaptive attacks break detectors (C-13, A-07, C-08) | G3 |
| 9 | Evaluation is detector-level only | Top venues also expect **end-to-end** impact on attack success and utility (MCPTox, MSB, AgentDojo), reporting hijack vs completion separately (C-14) | C-01, C-04, C-09, C-14 |

---

## 4. Refined problem statement (recommended)

### 4.1 Narrowed focus

> **From "detect poisoned tool descriptions" to "decide whether a *change* to a trusted MCP tool definition is a legitimate update or a poisoning (rug pull)", with honest, base-rate-aware evaluation on real version histories.**

This keeps your whole architecture (integrity → semantic → policy → runtime → risk). The layers stay, but the **headline contribution** moves to the place where Steps 1 and 2 found the clearest gap (G1, G2, G4), with G3 and G6 as methodological contributions.

### 4.2 Title options

1. **"Rug Pull or Routine Update? Change-Aware Detection of Tool-Definition Poisoning in Model Context Protocol Ecosystems"** (recommended)
2. "Beyond Hash Pinning: Semantic Change Analysis for Trustworthy Tool Definitions in MCP-Based AI Agents"
3. "Drift-Aware Trust for LLM Agent Tools: Measuring and Detecting Malicious Tool-Definition Updates in MCP"

### 4.3 Research problem (one paragraph)

MCP clients place server-supplied tool definitions directly into the model's context, and the protocol neither requires clients to pin those definitions nor tells them what changed when a server updates them. Exact-hash pinning, the only widely proposed control, flags every change. Yet real definitions change frequently for benign reasons (8–10.9% of ~13,000 public endpoints within days), producing alarm fatigue, while a poisoned update can be a single appended sentence or a nested schema field. Existing academic detectors classify single snapshots, report saturated in-distribution scores, and are not evaluated at realistic base rates or against adaptive attackers. **The problem is to decide, at the moment a trusted tool definition changes, whether the change is benign or malicious, with a false-alarm rate low enough for deployment and robustness to adaptive poisoning.**

### 4.4 Research objective

Design, implement and evaluate a **change-aware MCP security gateway** that:
- pins canonical tool definitions;
- analyses the semantic and capability delta of every change across the *entire* definition (name, description, schema, enums, server instructions);
- enforces description-independent capability policy;
- optionally verifies behaviour change in a sandbox;
- fuses these signals into a **calibrated** ALLOW / REVIEW / BLOCK decision.

The gateway is evaluated on a new corpus of real benign version histories and controlled poisoned updates.

### 4.5 Revised research questions

| RQ | Question | Replaces | Gap |
|---|---|---|---|
| **RQ1 (measurement)** | How often, and in what ways, do real MCP tool definitions change legitimately? What alarm burden does each pinning granularity impose (description hash, canonical full-definition hash, capability fingerprint)? | Old RQ1 (trivial) | G4, G2 |
| **RQ2 (detection)** | Can **delta-level** semantic analysis (span/field diff + embeddings + classifier + capability-expansion features) separate poisoned updates from legitimate ones better than (a) whole-text cosine drift, (b) single-snapshot classifiers (TF-IDF+LR, PIGuard, LLM Guard), and (c) an LLM judge? Measured as precision at fixed recall and at 1:100 and 1:1000 prevalence. | Old RQ2 | G1, G3 |
| **RQ3 (fusion)** | Does **calibrated** fusion of integrity, delta-semantic, capability/policy and (optional) behavioural signals improve over the best single layer? What does each layer contribute in a full ablation? | Old RQ3 | G6 |
| **RQ4 (robustness)** | How do detectors degrade on (i) unseen payload families, (ii) unseen server families (group-aware split), (iii) chronologically later versions, and (iv) adaptive attackers (paraphrase via TextAttack; LLM-optimised poisons in the style of MCP-ITP and ToolTweak; poisons targeting the LLM judge)? | Old RQ4 (partly) | G3, G9 |
| **RQ5 (end-to-end cost)** | With the gateway deployed, how much do attack success and task utility change on MCPTox / MSB / AgentDojo extended with poisoned updates? What is the per-layer latency, compared with ShieldMCP's reported <120 ms median? | Old RQ5 | G6 |

### 4.6 Hypotheses (state them so they can be falsified)

- **H1:** Exact hashing of the description string or full definition produces an alarm rate on benign updates too high for practical use. Capability fingerprints reduce it but miss description-only poisoning. *(Tests the contested practitioner numbers.)*
- **H2:** Delta-level features outperform whole-description cosine drift, because poisoned updates are typically small insertions.
- **H3:** Single-snapshot detectors trained on synthetic data lose substantial precision under group-aware and chronological splits (cf. J-33, C-61).
- **H4:** Hard-to-manipulate signals (pinning history, capability expansion, policy violations) contribute most to robustness under adaptive attack (cf. C-56, C-13).

### 4.7 Claimable contributions (if results hold)

1. **MCP-Drift corpus** (working name): real benign version histories of MCP tool definitions, paired with controlled poisoned updates.
   - Payload taxonomy: imperative injection, exfiltration, persuasive/preference (MPMA), implicit (MCP-ITP), schema-level, Unicode.
   - Released with a datasheet, a labelling protocol and inter-annotator agreement.
   - *Fills G2.*
2. **The first measurement** of legitimate tool-definition churn and the alarm burden of pinning granularities. *Fills G4; answers a contested practitioner question with data.*
3. **A change-aware detector** that analyses the delta across the whole definition. *Fills G1/G5.*
4. **A calibrated layered gateway** with cost-derived thresholds and a full ablation. *Fills G6.*
5. **A base-rate-aware, adaptive evaluation protocol** for MCP poisoning detectors, comparing against PIGuard, LLM Guard/Vigil, an LLM judge, mcp-scan and (if available) MCP-Guard. *Fills G3/G9.*

**Do not claim** novelty for hashing, signing, explicit policy, sandboxing, or the existence of a layered gateway. Cite ETDI, TUF/Sigstore, Jamshidi, MCP-Guard, ShieldMCP and Huang (JCP) for those.

### 4.8 Updated threat model (additions to the original)

- **In scope:**
  - a malicious or compromised server that serves benign definitions first and later updates them (rug pull);
  - a malicious-from-day-one server (handled by single-snapshot detection plus policy, reported separately);
  - poisoning in any metadata field;
  - per-session / per-client variation of definitions (split view);
  - an adaptive attacker who knows the detector (grey-box).
- **Out of scope:**
  - model backdoors (C-15, C-16);
  - injection through tool *outputs* (covered by AgentDojo-style defenses; cite C-09, C-34, C-35);
  - compromise of the gateway itself.
- **Trust anchor:** trust-on-first-use pinning, with optional registry-anchored signatures. State the weakness of first contact explicitly; TOFU is unprotected at first contact.

---

## 5. Positioning against the closest works (for the paper's Related Work table)

| Work | What it does | What the refined proposal adds |
|---|---|---|
| ShieldMCP (C-06, ACL'26 Ind.) | Runtime interception; attack success 74%→<9%; <120 ms | Version-pair change analysis; benign-update FPR at realistic base rates; per-layer ablation; public corpus |
| Jamshidi et al. (A-01) | Signed manifests + LLM review + guardrails; rug pull defined | Distinguishing benign vs malicious change (not only *that* something changed); calibrated fusion; adaptive evaluation |
| MCP-Guard (A-02) | Rule→E5→LLM single-snapshot detection; 70k samples | Delta analysis; real benign churn; group-aware/chronological splits; base-rate metrics |
| ETDI (A-03), Attested Admission (A-14) | Signing, versioning, policy, re-approval on change | Measured alarm burden of re-approval; semantic triage of changes, so signing becomes usable |
| ML-Based Detection (A-04) | Classifiers on 1,440 descriptions; 100% F1 | Harder, realistic evaluation showing where single-snapshot classifiers fail |
| Connor (A-05) | Behaviour vs declared intent | Links *definition* change to *behaviour* change across versions (optional layer) |
| Huang et al. (J-04, JCP'26) | STRIDE/DREAD; 7 clients × 4 attacks; proposed layered defenses | An implementation and quantitative evaluation of a gateway |
| TRUSTDESC (A-08) | Regenerates trusted descriptions | Detection and triage instead of replacement; can be combined (discuss) |
| mcp-scan / Snyk, Cisco, Lasso (products) | Hash (v0.3), API/YARA/LLM scanning; no metrics | Published metrics; semantic drift |
| LastPyMile (C-50), npm permissions (C-51), CADE (C-64) | Delta analysis / capability drift / learned drift for **code** and malware | Transfer to **natural-language instructions consumed by an LLM** |

---

## 6. Optional broadening and narrowing

- **Broaden (if you want wider impact):** generalise from MCP to "agent tool ecosystems" (MCP, OpenAI Apps/GPT actions, agent *skills*, A2A agent cards).
  - Evidence that the same problem exists elsewhere:
    - GPTracker (C-23): builders "hiding intention in descriptions";
    - ChatGPT plugins (W-03);
    - Snyk ToxicSkills: 13.4% of 3,984 agent skills had at least one critical issue (Step 1 annex, [2nd-hand]).
  - Cost: more data engineering. **Recommendation:** keep MCP as the main subject and discuss the generalisation.
- **Narrow further (if time or resources are tight):** drop the runtime monitor (G8) and focus on RQ1–RQ4 (measurement + change-aware detection + calibration + robustness). That is still a complete journal paper. The runtime layer can become future work, citing Connor (A-05).

---

## 7. Target venues (with reasoning, not predictions)

| Venue | Type | Quality | Why it fits | What it will expect |
|---|---|---|---|---|
| **Computers & Security** (Elsevier) | Journal | Q1 (SJR 2025 1.598) | Applied security systems with empirical evaluation | Dataset, baselines, ablation, limitations |
| **IEEE TDSC** | Journal | Q1 (1.758) | Dependable/secure system design with rigorous evaluation | Strong threat model; adaptive attacks |
| **IEEE TIFS** | Journal | Q1 (2.193) | More selective; detection/forensics angle | Strong novelty and theory |
| **ACM TOPS** | Journal | Q1 | Security systems | Rigor |
| **JISA** (Elsevier) | Journal | Q1 (0.905) | Applied security; faster | Solid evaluation |
| **ACM TOSEM** | Journal | Q1 (1.590) | If the RQ1 mining/measurement study is strong (SE-ecosystem angle; Hou et al. is there) | Mining methodology |
| USENIX Security / CCS / NDSS / IEEE S&P | Conference | A\* | If results are strong, especially adaptive robustness and the measurement study | Very high bar on novelty and adaptive evaluation |
| ACSAC / RAID / ESORICS / AsiaCCS / EuroS&P | Conference | A | Good fit for a gateway system paper | Systems plus evaluation |
| MSR (Mining Software Repositories) | Conference | A | The RQ1 churn measurement alone could be a short or full paper | Reproducible mining |

**Note:** the journal gap (G7) makes a Q1 journal a natural first target. Confirm the absence of competing journal papers with direct database searches first (Step 2 §5, item 8).

---

## 8. What must be verified in Step 4 (deep reading of downloaded papers)

**Read these in full and tick each check:**

- [ ] **ShieldMCP (C-06):** Does it compare trusted vs received definitions? Does it report FPR on benign updates? Does it give per-layer ablation? Is a dataset released?
- [ ] **Jamshidi et al. (A-01):** How is a rug pull detected (signature mismatch only, or semantic review of the delta)? What are the metrics and dataset?
- [ ] **MCP-Guard (A-02):** Does MCP-AttackBench contain version pairs or benign updates? Is there a split methodology? Is there an ablation?
- [ ] **Huang et al. (J-04):** Are any of the proposed defenses implemented and evaluated?
- [ ] **ML-Based Detection (A-04):** How was the dataset built? Was there template leakage?
- [ ] **Connor (A-05):** Does it consider version changes?
- [ ] **TRUSTDESC (A-08):** Mechanism, and whether it handles updates.
- [ ] **MCP-DPT (A-19):** Does its defense-placement coverage analysis already state G1/G6?
- [ ] **MCPTox (C-01) and MSB (C-04):** Licences and reusability of their poisoned descriptions as poisoned "successor versions".
- [ ] **IEEE Access SLR (Woesle & Buettner; IEEE Xplore 11551573):** Confirm the "83.9% prompt interface / zero tool boundary" figure. If true, it is quotable gap evidence.
- [ ] **Direct journal-database search** (ScienceDirect / IEEE Xplore / Springer) for 2025–2026 MCP and tool-poisoning articles, to confirm G7.
- [ ] **Feasibility of RQ1 data:** availability of version histories for MCP servers. Candidate sources:
  - GitHub repositories of servers listed in the official registry;
  - the 67,057-server registry corpus of Li & Gao (A-15);
  - whether the practitioner dataset in Discussion #3303 is public.

If any of the first three checks shows that a competitor already does version-pair semantic change analysis, fall back as follows:
- headline = **RQ1 measurement + RQ4 robustness/evaluation protocol** (G2, G3, G4 remain open on current evidence);
- change-aware detection becomes a component.

---

## 9. One-page summary for your supervisor or faculty review

- **The threat is real and recognised.**
  - OWASP MCP03, MITRE ATLAS AML.T0110/T0109 and an NSA CSI cover it.
  - There are PoCs (Invariant Labs), a rug-pull CVE (MCPoison) and a version rug pull in the wild (postmark-mcp).
  - No confirmed in-the-wild *description*-poisoning breach yet, so frame it as demonstrated, not widespread.
- **The broad idea is crowded.**
  - Layered MCP defenses already exist: ShieldMCP (ACL'26), MCP-Guard, Jamshidi et al., ETDI, Huang et al. (JCP'26).
  - Hashing, signing, policy and sandboxing are not novel.
- **The clear gap is change-awareness.**
  - Nobody (academia or products) decides whether a *change* to a trusted tool definition is benign or malicious.
  - No real version-pair dataset exists.
  - The cost of exact pinning (false alarms) is contested and unmeasured.
  - Detector evaluations are saturated, balanced and non-adaptive.
- **Refined project:**
  - mine real MCP version histories (RQ1);
  - build a change-aware, calibrated, layered gateway (RQ2/RQ3);
  - evaluate it rigorously against adaptive attacks and real baselines (RQ4);
  - measure end-to-end impact and latency (RQ5).
- **Target:** a Q1 journal first (Computers & Security, TDSC, JISA, TOPS). Only four MCP journal papers exist and none evaluates an implemented defense.
