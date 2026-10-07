# Step 2 — Area P4: Software Supply-Chain Security, Integrity & Third-Party Extension/Plugin Ecosystems

Date compiled: 2026-10-07. Prepared for: "A Layered Security Framework for Detecting and Preventing Tool-Description Poisoning in MCP Environments".

## Method and important caveats (read first)

- Verification source: WebSearch result snippets (publisher pages, usenix.org, NDSS, conf.researchr.org program pages, OpenAlex, arXiv listings, university repositories, NSF-PAR) that came back for each query. **Direct page fetches (WebFetch) were blocked by the egress proxy for every domain tried** (doi.org, dl.acm.org, usenix.org, arxiv.org, ndss-symposium.org, ojs.aaai.org, scimagojr.com, semanticscholar API, conf.researchr.org). So no full texts were read; all summaries come from abstracts/snippets surfaced by search.
- **The shared web-search budget ran out partway through this task.** Sub-area (d) (LLM plugin stores, GPT Store, browser-extension malicious updates, VS Code extensions) **could not be verified at all** in this session. Those items are listed separately in Section D as *UNVERIFIED leads* with no numbers or DOIs invented. A follow-up session should verify them before citing.
- **Tier info**: SJR quartiles and CORE ranks could NOT be checked on scimagojr.com / portal.core.edu.au (blocked). All tier statements below are marked "per general knowledge — verify".
- Labels: [J] = peer-reviewed journal, [C] = peer-reviewed conference, [W] = workshop, [M] = magazine (peer-reviewed practitioner venue), [P] = arXiv-only preprint.

---

## A. Integrity, provenance and signing frameworks

### [P4-01] Survivable Key Compromise in Software Update Systems (TUF)
- Justin Samuel, Nick Mathewson, Justin Cappos, Roger Dingledine | 2010 | 17th ACM Conference on Computer and Communications Security (CCS '10), Chicago, Oct 4–8 2010 [C]
- Tier: CORE A* (per general knowledge — verify)
- DOI: not surfaced in search — UNVERIFIED (look up in ACM DL). PDF seen at https://uptane.org/assets/files/samuel_ccs_2010-2e4e7a69695e936b1ad3b0b7010c550a.pdf
- What they did: Argue that existing software-update systems have little or no defence against signing-key compromise, which had put millions of update clients at risk. They design and implement The Update Framework (TUF), which separates responsibilities into roles (root, targets, snapshot, timestamp) with threshold signatures, key revocation and freshness metadata so that compromising one key does not let an attacker push arbitrary updates. TUF is the basis of Uptane (automotive) and is used in package-repository signing designs.
- Key numbers: not seen in snippets.
- Limitations/gaps: Protects the *distribution* of artifacts whose content is assumed to be what the developer intended; says nothing about whether the artifact is semantically malicious.
- Mapping to project: Threat-model analogue for MCP "rug pulls": a server operator (or a compromised server) pushing a changed tool definition = malicious/compromised update. TUF's concepts — signed metadata, freshness/expiry, rollback and freeze-attack protection, role separation and threshold signing — map directly onto an MCP tool-manifest signing scheme (Ed25519 extension). Notably, SHA-256 pinning alone gives no rollback/freeze protection; TUF's snapshot/timestamp roles show what is missing.
- Verification source seen: uptane.org PDF listing + uptane.org publications page (search snippets).

### [P4-02] in-toto: Providing Farm-to-Table Guarantees for Bits and Bytes
- Santiago Torres-Arias, Hammad Afzali, Trishank Karthik Kuppusamy, Reza Curtmola, Justin Cappos | 2019 | 28th USENIX Security Symposium, Santa Clara [C] | pp. 1393–1410
- Tier: CORE A* (per general knowledge — verify)
- Link: https://www.usenix.org/conference/usenixsecurity19/presentation/torres-arias ; open PDF https://www.usenix.net/system/files/sec19-torres-arias.pdf
- What they did: Present in-toto, a framework that cryptographically binds every step of the supply chain (commit, build, test, package) via signed "link" metadata and a project "layout" policy, so the end user can verify the whole chain from start to deployment. Integrated with Debian apt, kubesec and the Datadog agent.
- Key numbers: Recreated 30 real-world supply-chain compromises; in-toto would have prevented at least 83% (per NYU press release seen in search).
- Limitations: Requires functionaries to adopt and sign each step; does not judge semantic maliciousness of a step that is authorised.
- Mapping: Model for *provenance* of MCP tool definitions — who authored a description, who approved it, which registry published it. A gateway "layout" could state which signer may publish which tool, analogous to the project's policy checker.
- Verification source seen: USENIX presentation page, NJIT Digital Commons, NYU news (search snippets).

### [P4-03] Sigstore: Software Signing for Everybody
- Zachary Newman, John Speed Meyers, Santiago Torres-Arias | 2022 | ACM CCS 2022, Los Angeles [C]
- Tier: CORE A* (per general knowledge — verify)
- DOI: 10.1145/3548606.3560596 (seen in OpenAlex record; open access CC-BY)
- What they did: Propose Sigstore, which ties signatures to existing OIDC identities through an ACME-like protocol, uses short-lived (ephemeral) keys to remove key-management burden, and records artifacts and identities in transparency logs (Rekor). Includes a formal attacker model, attack avenues on the ecosystem and hardening advice.
- Key numbers: Sigstore blog: ~2 M Rekor entries when the paper was drafted, ~6 M at publication (blog, not paper).
- Limitations: Transparency logs show *that* something was signed and by whom, not whether content is benign.
- Mapping: Concrete design for signing MCP tool manifests without long-lived keys; a transparency log of tool-definition versions would let clients detect silent changes (rug pulls) and audit history — a stronger alternative/complement to local SHA-256 pinning.
- Verification source seen: OpenAlex record, Sigstore blog, NSF-PAR (search snippets).

### [P4-04] Speranza: Usable, Privacy-friendly Software Signing
- Kelsey Merrill, Zachary Newman, Santiago Torres-Arias, Karen Sollins | 2023 | ACM CCS 2023, Copenhagen, Nov 26–30 [C]
- Tier: CORE A* (per general knowledge — verify)
- DOI: 10.1145/3576915.3623200 (seen in arXiv 2305.06463 listing details via search)
- What they did: Certificate-based signing that keeps the signer anonymous using zero-knowledge identity co-commitments: a signer obtains an identity-bound signature from an automated CA, and verifiers check that the signer was authorised for the package without learning who they are.
- Key numbers: Sub-millisecond signing/verification even for repositories with millions of packages; a few hundred lines of code.
- Limitations: Proof-of-concept.
- Mapping: Relevant if MCP registries want maintainer-authorisation checks without exposing maintainer identity; design input for the signature extension.
- Verification source seen: MIT DSpace, arXiv listing, The New Stack (search snippets).

### [P4-05] CHAINIAC: Proactive Software-Update Transparency via Collectively Signed Skipchains and Verified Builds
- Kirill Nikitin, Eleftherios Kokoris-Kogias, Philipp Jovanovic, Nicolas Gailly, Linus Gasser, Ismail Khoffi, Justin Cappos, Bryan Ford | 2017 | 26th USENIX Security Symposium, Vancouver [C] | pp. 1271–1287
- Tier: CORE A* (per general knowledge — verify)
- Link: https://usenix.org/conference/usenixsecurity17/technical-sessions/presentation/nikitin ; IACR ePrint 2017/648
- What they did: Decentralised update framework: independent witness servers collectively check that updates conform to release policy, build verifiers check source-to-binary correspondence, and a tamper-proof skipchain release log stores collectively signed updates so arbitrarily out-of-date clients can validate updates and key changes efficiently.
- Key numbers: ~5 min per package release and ~20 s for the aggregate timeline on reproducible Debian packages; with PyPI data, security comparable to verifying every update personally at ~1/5 of the bandwidth.
- Limitations: Needs reproducible builds and a witness cothority.
- Mapping: "Witness cosigning" maps to multiple independent scanners (e.g., several gateways/registries) co-signing that a tool-description version passed poisoning checks before clients accept it; skipchain = efficient version history for drift checking.
- Verification source seen: USENIX page, EPFL Infoscience, IACR ePrint, Morning Paper blog (snippets).

### [P4-06] Reproducible Builds: Increasing the Integrity of Software Supply Chains
- Chris Lamb, Stefano Zacchiroli | 2022 | IEEE Software [J/M] | vol. 39, no. 2, pp. 62–70
- Tier: IEEE Software — SJR Q1/Q2 in Software (per general knowledge — verify). Won IEEE Software Best Paper 2022 (Télécom Paris announcement seen).
- DOI: 10.1109/MS.2021.3073045 (seen in snippet); arXiv 2104.06020
- What they did: Present reproducible builds (bit-for-bit identical outputs from the same source) as a way for independent parties to verify binaries correspond to source, drawing on the Debian reproducibility effort, and link reproducibility to QA practice.
- Limitations: Applies to compiled artifacts; requires deterministic toolchains.
- Mapping: Conceptual basis for "independently re-derive and compare": a gateway can re-fetch a tool definition through an independent path/registry and compare hashes; also motivates *canonicalisation* of tool JSON before hashing (so benign formatting differences do not trigger false integrity alarms).
- Verification source seen: arXiv listing, IP-Paris research portal, Zacchiroli site (snippets).

### [P4-07] Signing in Four Public Software Package Registries: Quantity, Quality, and Influencing Factors
- Taylor R. Schorlemmer, Kelechi G. Kalu, Luke Chigges, Kyung Myung Ko, Eman Abu Ishgair, Saurabh Bagchi, Santiago Torres-Arias, James C. Davis | 2024 | 45th IEEE Symposium on Security and Privacy (S&P 2024) [C]
- Tier: CORE A* (per general knowledge — verify)
- Link: arXiv 2401.14635; CERIAS project page lists S&P 2024. IEEE DOI not seen — UNVERIFIED.
- What they did: Measure signing quantity and quality in Maven Central, PyPI, Docker Hub and Hugging Face, and use a quasi-experiment to estimate factors affecting signing.
- Key findings: Mandatory signing policies give near-perfect signing rates (Maven); de-emphasising signing reduces it (PyPI); dedicated tooling improves signature quality.
- Limitations: Measures presence/quality of signatures, not whether signatures stopped attacks.
- Mapping: Direct evidence for a design recommendation: optional signing of MCP tool definitions will see low adoption; registries/clients must *require* signatures and ship tooling. Supports positioning Ed25519 as a policy-enforced control, not merely optional.
- Verification source seen: arXiv listing, CERIAS page, Purdue poster (snippets).

---

## B. SoKs, taxonomies and surveys

### [P4-08] (SoK:) Taxonomy of Attacks on Open-Source Software Supply Chains
- Piergiorgio Ladisa, Henrik Plate, Matias Martinez, Olivier Barais | 2023 | IEEE Symposium on Security and Privacy (S&P 2023) [C] — **venue per general knowledge; my searches only confirmed the arXiv version (2204.04008) and one blog listing "S&P'22"; DOI 10.1109/SP46215.2023.10179304 is UNVERIFIED** — confirm on IEEE Xplore.
- Tier: CORE A* (per general knowledge — verify)
- What they did: Language- and ecosystem-independent attack tree covering all stages from code contribution to package distribution; mapped to safeguards and validated with user surveys.
- Key numbers: 107 unique attack vectors, 94 real-world incidents, 33 safeguards; surveys with 17 experts and 134 developers.
- Limitations: Focused on code/package artifacts; no vectors for natural-language metadata consumed by an AI agent.
- Mapping: Use as the template for the MCP threat taxonomy: e.g. "inject into existing package via maintainer account takeover" ↔ compromised MCP server update (rug pull); "typosquatting/name confusion" ↔ tool-name shadowing; "distribute malicious version" ↔ description change after approval.
- Verification source seen: arXiv listing, deepai, secrss.com (snippets).

### [P4-09] Journey to the Center of Software Supply Chain Attacks
- Piergiorgio Ladisa, Serena Elisa Ponta, Antonino Sabetta, Matias Martinez, Olivier Barais | 2023 | IEEE Security & Privacy (magazine) [M] | published 2023-08-21
- Tier: IEEE S&P magazine — SJR Q1/Q2 (per general knowledge — verify)
- DOI: 10.1109/MSEC.2023.3302066 (seen in snippet); arXiv 2304.05200
- What they did: Summarise the taxonomy of [P4-08], list safeguards, and introduce the "Risk Explorer for Software Supply Chains" visualisation tool.
- Mapping: Practitioner-oriented framing usable for the dashboard (attack-vector → safeguard mapping).
- Verification source seen: arXiv/deepai snippets.

### [P4-10] Backstabber's Knife Collection: A Review of Open Source Software Supply Chain Attacks
- Marc Ohm, Henrik Plate, Arnold Sykosch, Michael Meier | 2020 | DIMVA 2020 (17th Int. Conf. on Detection of Intrusions and Malware, and Vulnerability Assessment), LNCS, Springer [C]
- Tier: CORE B (per general knowledge — verify)
- DOI: 10.1007/978-3-030-52683-2_2 (seen in snippet); arXiv 2005.09535
- What they did: Manually collected and analysed real malicious packages and built two attack trees: how malicious code is injected into a dependency tree and when/under which conditions it executes (install-time, runtime, conditional triggers); characterised samples by objective, obfuscation, etc.
- Key numbers: 174 malicious packages from npm, PyPI, RubyGems, Nov 2015–Nov 2019.
- Limitations: Small, manually curated dataset; access to the dataset is by request.
- Mapping: (i) Labeled-dataset methodology template for the SAFE/POISONED tool-definition dataset (curated real incidents + characterisation dimensions); (ii) the "trigger conditions" tree is analogous to conditional poisoning (descriptions activated only for certain prompts/after N invocations).
- Verification source seen: arXiv listing, Fraunhofer publica, SAP blog (snippets).

### [P4-11] SoK: Analysis of Software Supply Chain Security by Establishing Secure Design Properties
- Chinenye Okafor, Taylor R. Schorlemmer, Santiago Torres-Arias, James C. Davis | 2022 | ACM Workshop on Software Supply Chain Offensive Research and Ecosystem Defenses (SCORED '22), co-located with CCS [W]
- Tier: workshop (no CORE rank)
- DOI: 10.1145/3560835.3564556 (seen in snippet)
- What they did: Identify four stages of a supply-chain attack and propose three secure-design properties — transparency, validity, separation — then map existing defences to them and identify gaps.
- Mapping: The three properties are a neat framing for the gateway: transparency (logging/version history of tool definitions), validity (integrity + semantic checks), separation (policy-derived capabilities, sandboxing).
- Verification source seen: SIGSAC SCORED proceedings page, Purdue e-Pubs, arXiv 2406.10109 (snippets).

### [P4-12] Research Directions in Software Supply Chain Security
- Laurie Williams, Giacomo Benedetti, Sivana Hamer, Ranindya Paramitha, Imranur Rahman, Mahzabin Tamanna, Greg Tystahl, Nusrat Zahan, Patrick Morrison, Yasemin Acar, Michel Cukier, Christian Kästner, Alexandros Kapravelos, Dominik Wermke, William Enck | 2025 | ACM Transactions on Software Engineering and Methodology (TOSEM) [J] | vol. 34 (no. 5 per one snippet), pp. 1–38
- Tier: TOSEM — SJR Q1 (per general knowledge — verify)
- DOI: 10.1145/3714464 (seen)
- What they did: Combine practitioner outreach with a literature review to describe three attack vectors — tainted dependencies/components/containers, compromised build infrastructure, and attacks on humans — and propose a research agenda (cites SolarWinds, log4j, xz utils).
- Mapping: Strongest Q1-journal anchor for the "MCP servers are supply-chain artifacts" framing in the Related Work section; also a source for "open problems" positioning.
- Verification source seen: Paderborn RIS record, NCSU library bib, NSF-PAR (snippets). Full text not read.

### [P4-13] Software supply chain: A taxonomy of attacks, mitigations and risk assessment strategies
- Betul Gokkaya, Leonardo Aniello, Basel Halak | 2026 | Journal of Information Security and Applications (Elsevier) [J] | vol. 97 (page/article no. UNVERIFIED)
- Tier: JISA — SJR Q1/Q2 (per general knowledge — verify); SCI-E and Scopus indexed per university listing seen.
- DOI: UNVERIFIED. Preprint: arXiv 2305.14157 ("Software supply chain: review of attacks, risk assessment strategies and security controls").
- What they did: Systematic literature review of 96 papers (2015–2023): 19 distinct supply-chain attacks (6 novel), 25 security controls mapped to attacks in a taxonomy, plus a risk-assessment methodology.
- Mapping: Recent journal SLR — useful for showing that existing control catalogues do not include semantic-metadata controls; its risk-assessment methodology can inform the risk engine's weighting.
- Verification source seen: Erdogan University AVESIS record, Southampton ePrints, arXiv (snippets).

---

## C. Ecosystem measurement and malicious-package detection

### [P4-14] Small World with High Risks: A Study of Security Threats in the npm Ecosystem
- Markus Zimmermann, Cristian-Alexandru Staicu, Cam Tenny, Michael Pradel | 2019 | 28th USENIX Security Symposium [C]
- Tier: CORE A* (per general knowledge — verify)
- Link: https://www.usenix.org/conference/usenixsecurity19/presentation/zimmerman ; arXiv 1902.09217
- What they did: Dependency/maintainer-network analysis of npm showing single points of failure: individual packages and a small number of maintainer accounts can affect huge parts of the ecosystem; evaluate mitigations (trusted maintainers, vetting).
- Key numbers: On average a package implicitly trusts 79 third-party packages and 39 maintainers.
- Mapping: Analogue for MCP clients that aggregate many servers: one compromised server's tool description influences the agent's behaviour across all tools (cross-tool "shadowing"); motivates per-server trust scoring.
- Verification source seen: USENIX page, arXiv, CISPA (snippets).

### [P4-15] Towards Measuring Supply Chain Attacks on Package Managers for Interpreted Languages
- Ruian Duan, Omar Alrawi, Ranjita Pai Kasturi, Ryan Elder, Brendan Saltaformaggio, Wenke Lee | 2021 | NDSS 2021 [C]
- Tier: CORE A* (per general knowledge — verify)
- DOI: 10.14722/ndss.2021.23055 (seen)
- What they did: Comparative framework of functional/security features of package managers; pipeline combining metadata, static and dynamic analysis to find registry abuse.
- Key numbers: 339 new malicious packages reported, 278 (82%) confirmed; 3 had >100,000 downloads.
- Mapping: Template for a *layered* (metadata + static + dynamic) pipeline — precisely the gateway's layering (metadata/NLP + policy + sandbox runtime). Supports RQ3 (layer combination).
- Verification source seen: NDSS paper page, arXiv 2002.01139 (snippets).

### [P4-16] LastPyMile: Identifying the Discrepancy between Sources and Packages
- Duc-Ly Vu, Fabio Massacci, Ivan Pashchenko, Henrik Plate, Antonino Sabetta | 2021 | ESEC/FSE 2021, Athens [C] | pp. 780–792
- Tier: CORE A* (per general knowledge — verify)
- Link: ESEC/FSE 2021 program page; tool github.com/assuremoss/lastpymile
- What they did: Identify file/line differences between a package's distributed artifact and its source repository, then scan only the differences with YARA rules and AST analysis; targets owner hijacking and typosquatting where code is injected only into the artifact.
- Key numbers: 2,438 popular PyPI packages (~10 M LoC). Reported discrepancy rates vary across secondary sources (e.g. 5.8% of artifacts / 2.6% of files with Python changes in a talk) — check paper.
- Limitations: Many discrepancies are benign — differences "cannot be just attributed to malicious injections".
- Mapping: **Closest classical analogue of the project's drift detection.** "Diff what changed, then analyse only the delta" ↔ compare trusted vs received tool description and run semantic analysis on the changed spans. Its finding that most diffs are benign is exactly RQ2's problem (distinguishing poisoned vs legitimate changes).
- Verification source seen: FSE 2021 program page, UniTN IRIS, GitHub README, SFSCON talk (snippets).

### [P4-17] Containing Malicious Package Updates in npm with a Lightweight Permission System
- Gabriel Ferreira, Limin Jia, Joshua Sunshine, Christian Kästner (authors per general knowledge — UNVERIFIED) | 2021 | ICSE 2021 (per general knowledge — UNVERIFIED) [C]
- Tier: CORE A* (per general knowledge — verify)
- Link: NSF-PAR record https://par.nsf.gov/biblio/10302333 (title seen in search result only; no abstract seen)
- What they did (per general knowledge — verify): Permission system for npm packages so that a malicious *update* cannot use capabilities (file system, network, etc.) the package did not previously need; dependents approve permission changes.
- Mapping: Direct analogue of the project's permission/policy checker: capabilities come from an explicit, versioned policy, and an update that requests new capabilities is flagged — the "capability drift" counterpart to description drift.
- Verification source seen: title only in NSF-PAR search result. Treat details as UNVERIFIED.

### [P4-18] Practical Automated Detection of Malicious npm Packages (Amalfi)
- Adriana Sejfia, Max Schäfer | 2022 | 44th International Conference on Software Engineering (ICSE 2022) [C] | pp. 1681–1692
- Tier: CORE A* (per general knowledge — verify)
- DOI: 10.1145/3510003.3510104 (seen in OpenAlex)
- What they did: Three-stage pipeline: ML classifiers trained on known malicious/benign packages; a reproducibility check (can the package be rebuilt from its source repo?) to filter false positives; textual clone detection to catch copies of known malware.
- Key numbers: Over 96,287 package versions published in one week, found 95 previously unknown malware samples with a "manageable" false-positive rate; a few seconds per package.
- Mapping: (i) Cheap classifier + secondary integrity check to cut FPs ↔ TF-IDF/LogReg + hash/signature layer; (ii) clone detection of known malware ↔ near-duplicate matching of known poisoned descriptions (embedding similarity to a poison corpus). Supports RQ3/RQ4 (layer combination reduces FPR).
- Verification source seen: arXiv 2202.13953, ICSE 2022 program page, OpenAlex (snippets).

### [P4-19] Killing Two Birds with One Stone: Malicious Package Detection in NPM and PyPI using a Single Model of Malicious Behavior Sequence (Cerebro)
- Junan Zhang et al. (Fudan University; full author list not seen) | TOSEM (arXiv comment "TOSEM 2024"; DOI 10.1145/3705304 → issue year 2025 likely — UNVERIFIED) [J]
- Tier: TOSEM — SJR Q1 (per general knowledge — verify)
- DOI: 10.1145/3705304 (seen in arXiv and CiteDrive)
- What they did: 16 static features abstracting malicious behaviour, organised into a behaviour *sequence*, then a fine-tuned BERT classifies; one model serves both npm and PyPI (cross-language knowledge fusion).
- Key numbers: vs. state of the art, +10.0% precision / +7.4% recall (mono-lingual), +9.9% / +8.9% (bi-lingual); 10.5 s per package; 7–8 months monitoring: 683 malicious PyPI and 799 malicious npm versions confirmed (later arXiv version; earlier versions report smaller numbers).
- Mapping: Shows that abstracting raw artifacts into a language-neutral *behaviour description* then fine-tuning a transformer generalises across ecosystems — supports the project's sentence-embedding / transformer classifier and the "unseen pattern generalisation" experiment (train on one MCP server family, test on another).
- Verification source seen: arXiv 2309.02637, CiteDrive DOI record, Zenodo (snippets).

### [P4-20] A Needle is an Outlier in a Haystack: Hunting Malicious PyPI Packages with Code Clustering (MPHunter)
- Wentao Liang, Xiang Ling, Jingzheng Wu, Tianyue Luo, Yanjun Wu | 2023 | 38th IEEE/ACM ASE 2023 [C] | pp. 307–318
- Tier: CORE A* (per general knowledge — verify)
- What they did: Unsupervised approach — cluster installation scripts; benign ones form clusters, malicious ones are outliers; rank by outlierness and distance to known malicious examples. Needs no taint sources/sinks or known patterns.
- Key numbers: 60 previously unknown malicious packages among 31,329 new uploads in two months, all confirmed by PyPI.
- Journal follow-up: "Detecting malicious packages in PyPI and npm by clustering installation scripts", IEEE TSE 2025 — **seen only as a citation in a later paper; UNVERIFIED**.
- Mapping: Outlier detection over a population of artifacts ↔ embedding-space anomaly detection over tool descriptions (and the project's Isolation Forest at runtime). Useful unsupervised baseline for unseen-pattern generalisation (RQ4/RQ5).
- Verification source seen: ASE 2023 program page, dblp.dagstuhl ASE 2023 listing (snippets).

### [P4-21] SpiderScan: Practical Detection of Malicious NPM Packages Based on Graph-Based Behavior Modeling and Matching
- Authors include Ruisi Wang (Fudan); full list not seen | 2024 | ASE 2024, Sacramento [C]
- Tier: CORE A* (per general knowledge — verify)
- What they did: Offline: build behaviour graphs (control flow + data dependencies across sensitive API calls) from known malicious packages, using an LLM to identify sensitive APIs in built-ins and third-party deps. Online: build suspicious graphs for a target and match; dynamic analysis + LLM confirm selected behaviours.
- Key numbers: 249 new malicious npm packages detected; 70 thank-you letters from npm.
- Mapping: Hybrid LLM + rule/graph matching + dynamic confirmation ↔ the gateway's NLP layer escalating to the sandbox only when needed (latency budget, RQ5).
- Verification source seen: ASE 2024 program page, researchr author profile (snippets).

### [P4-22] EA4MP — Integrating Deep Code Behaviors with Metadata Features for Malicious PyPI Package Detection
- Authors not seen | 2024 | ASE 2024 [C] (title partially truncated in the program-page snippet — exact title UNVERIFIED)
- Tier: CORE A* (per general knowledge — verify)
- What they did (snippet): Argues earlier work uses only partial metadata (name, version); combines BERT-based code-behaviour features with PKG-INFO metadata in an AdaBoost ensemble.
- Mapping: Direct precedent for fusing *text/metadata* signals with *behavioural* signals in one ensemble — the project's risk engine.
- Verification source seen: ASE 2024 program page title + secondary summary (snippets).

### [P4-23] Malicious Package Detection using Metadata Information (MeMPtec)
- Sajal Halder, Michael Bewong, et al. (Charles Sturt Univ., Data61/CSIRO, QUT, Univ. of Adelaide) | 2024 | ACM Web Conference (WWW 2024) [C] — venue per a review site and arXiv listing reference; confirm in ACM DL
- Tier: CORE A* (per general knowledge — verify)
- Link: arXiv 2402.07444
- What they did: Metadata-only detector for npm; features split into easy-to-manipulate (ETM) vs difficult-to-manipulate (DTM) by monotonicity and restricted-control properties to resist adversarial metadata edits.
- Key numbers: Reductions of up to 97.56% in false positives and up to 91.86% in false negatives vs. state of the art (one secondary source says 97.5%).
- Mapping: **Most transferable idea for adversarial robustness of tool-metadata features.** Tool names/descriptions are easy to manipulate; server provenance, signing key, version history, schema-vs-behaviour consistency are harder. The project should classify its features along ETM/DTM lines and evaluate against adaptive attackers.
- Verification source seen: arXiv HTML, CSU research output page, liner.com review (snippets).

### [P4-24] On the Feasibility of Cross-Language Detection of Malicious Packages in npm and PyPI
- Piergiorgio Ladisa, Serena Elisa Ponta, Nicola Ronzoni, Matias Martinez, Olivier Barais | 2023 | ACSAC 2023, Austin [C]
- Tier: CORE A (per general knowledge — verify)
- Link: https://acsac.org/2023/program/final/s69.html ; arXiv 2310.09571
- What they did: Language-independent features (simple lexical and package-size features) to train a single classifier that works across npm and PyPI, mitigating scarcity of labeled samples outside npm; evaluated in controlled and in-the-wild settings; released dataset and models.
- Key numbers: 10 days of new uploads, 31,292 packages scanned → 58 previously unknown malicious packages (38 npm, 20 PyPI).
- Mapping: Evidence that cheap lexical features + classic ML transfer across ecosystems — supports a TF-IDF/LogReg baseline and cross-server-family generalisation tests.
- Verification source seen: ACSAC program page and slides, arXiv (snippets).

### [P4-25] Leveraging Large Language Models to Detect npm Malicious Packages (SocketAI; earlier "Shifting the Lens")
- Nusrat Zahan, Philipp Burckhardt, Mikola Lysenko, Feross Aboukhadijeh, Laurie Williams | 2025 | ICSE 2025 (Research Track) [C]
- Tier: CORE A* (per general knowledge — verify)
- Link: arXiv 2403.12196; ICSE 2025 program page
- What they did: LLM-assisted (ChatGPT) workflow to review npm packages for malicious behaviour, with static analysis as a pre-screener; compared with CodeQL using 39 custom rules; qualitative analysis of misses.
- Key numbers: Benchmark of 5,115 npm packages (2,180 malicious). GPT-4: ~99% precision, ~97% F1; GPT-3: ~91% precision, ~94% F1; vs static analysis +16% precision, +9% F1; pre-screening cut files sent to LLM by ~78%.
- Limitations: Cost; LLM non-determinism; evaluation on one ecosystem.
- Mapping: Supports an "LLM-as-judge" layer for tool descriptions with cheap pre-screening to control latency/cost (RQ5). Also a caution: LLM judges can themselves be prompt-injected by the very description they analyse — a risk *specific* to MCP that npm code review lacks.
- Verification source seen: arXiv listing, ICSE 2025 program page, NSF-PAR (snippets).

### [P4-26] MalGuard: Towards Real-Time, Accurate, and Actionable Detection of Malicious Packages in PyPI Ecosystem
- First author Xingan Gao (from URL slug; full author list not seen) | 2025 | 34th USENIX Security Symposium [C]
- Tier: CORE A* (per general knowledge — verify)
- Link: https://www.usenix.org/conference/usenixsecurity25/presentation/gao-xingan ; arXiv 2506.14466
- What they did (snippet): Shows that traditional ML with a rich feature set can perform well for real-time PyPI detection (not LLM-based).
- Key numbers: not seen.
- Mapping: Supports the claim that a fast classical-ML layer is a defensible, low-latency baseline for a gateway.
- Verification source seen: USENIX page title in search; secondary summary only.

### [P4-27] A Machine Learning-Based Approach for Detecting Malicious PyPI Packages
- Haya Samaana, Diego Elias Costa, Emad Shihab, Ahmad Abdellatif | 2025 | 40th ACM/SIGAPP Symposium on Applied Computing (SAC 2025) [C]
- Tier: CORE B (per general knowledge — verify)
- Link: arXiv 2412.05259
- What they did: ML + static analysis over package metadata, code, files and *textual characteristics* (e.g., README length, author info, homepage, number of versions); notes not all metadata features are significant.
- Key numbers: F1 = 0.94 with a stacking ensemble on PyPI.
- Mapping: Precedent for textual/metadata features in a stacking ensemble — mirrors TF-IDF+LogReg plus meta-features; feature-ablation finding matches the planned ablation study.
- Verification source seen: arXiv listing, An-Najah staff page (snippets).

### [P4-28] An Empirical Study of Malicious Code in PyPI Ecosystem
- Wenbo Guo, Zhengzi Xu, Chengwei Liu, Cheng Huang, Yong Fang, Yang Liu | 2023 | ASE 2023 per general knowledge — **venue UNVERIFIED** (search confirmed arXiv 2309.11021 only) [C?]
- What they did: Automated collection framework; dataset of 4,669 malicious package files grouped into five behaviour categories; dataset released (pypi_malregistry on GitHub).
- Key numbers: >50% of samples show more than one malicious behaviour; ~75% reach users via source installation; >72% of reported packages remained on PyPI mirrors long after discovery.
- Mapping: Persistence on mirrors ↔ cached/stale MCP tool definitions in clients and registries; argues for revocation/expiry metadata (TUF-style, [P4-01]).
- Verification source seen: arXiv listing (snippet).

### [P4-29] MalWuKong: Towards Fast, Accurate, and Multilingual Detection of Malicious Code Poisoning in OSS Supply Chains
- Authors from Huazhong University of Science and Technology (names not seen) | 2023 | ASE 2023 **Industry Challenge track** (not FSE 2023 as the task brief suggested; seen on ASE program page) [C, industry track]
- Tier: industry track (main ASE is CORE A*, per general knowledge)
- What they did (per a 2026 empirical study's table): static tool using CodeQL information-flow tracking from sensitive calls back to sources; features = code and API calls; not publicly available.
- Mapping: Minor; shows rule/query-based detectors as a baseline class.
- Verification source seen: ASE 2023 program listing + a 2026 arXiv study table (snippets).

---

## D. Third-party extension / plugin / LLM-app ecosystems — UNVERIFIED LEADS

**The search budget was exhausted before this sub-area could be checked, and all direct fetches were blocked.** The items below come from my general knowledge only. Do not cite them until a follow-up session confirms title, authors, venue and DOI. No numbers are given on purpose.

| Lead ID | Working title (UNVERIFIED) | Claimed venue (UNVERIFIED) | Why it matters for MCP |
|---|---|---|---|
| P4-D1 | "LLM Platform Security: Applying a Systematic Evaluation Framework to OpenAI's ChatGPT Plugins" (Iqbal, Kohno, Roesner) | AAAI/ACM AIES 2024; arXiv 2309.10254 | Closest pre-MCP analogue: third-party plugins whose *natural-language manifests/descriptions* are consumed by the LLM; attack taxonomy for plugin→user/LLM/other-plugin. |
| P4-D2 | "On the (In)Security of LLM App Stores" (Hou et al.) | IEEE S&P 2025 (per general knowledge) | Measurement of malicious/abusive apps and misleading descriptions in GPT-store-like marketplaces. |
| P4-D3 | "LLM App Store Analysis: A Vision and Roadmap" (Zhao, Hou, Wang) | ACM TOSEM 2025 (per general knowledge) | Q1-journal anchor for LLM app-store analysis agenda. |
| P4-D4 | Custom-GPT/GPT-Store measurement studies (e.g., "GPTs Window Shopping", "A First Look at GPT Apps") | various 2024–2025 (UNVERIFIED) | Ecosystem-scale evidence of instruction-level abuse in third-party LLM extensions. |
| P4-D5 | "Hulk: Eliciting Malicious Behavior in Browser Extensions" (Kapravelos et al.) | USENIX Security 2014 | Dynamic analysis to trigger hidden malicious behaviour — analogue for the sandboxed runtime monitor. |
| P4-D6 | Browser-extension ownership-transfer / malicious-update studies (Chrome Web Store) | various (UNVERIFIED) | Classic "benign-then-malicious update" = rug pull. |
| P4-D7 | "UntrustIDE: Exploiting Weaknesses in VS Code Extensions" (Edirimannage et al.) | NDSS 2024 (per general knowledge) | IDE extensions run with broad privileges and auto-update — analogous to MCP servers in IDE agents. |
| P4-D8 | Trust-on-first-use / pinning studies (e.g., Perspectives, SSH/HPKP pinning) | various (UNVERIFIED) | Weaknesses of TOFU apply directly to SHA-256 pinning of tool definitions (first contact unprotected; legitimate updates cause alarm fatigue). |

## E. arXiv-only / non-archival items seen (appendix; cite with care)
- Cutting the Gordian Knot: PyGuard — arXiv 2601.16463 (2026): behavioural pattern mining + LLM reasoning for PyPI; reports 99.50% accuracy with 2 FPs; notes current PyPI detectors may flag ~1/3 of legitimate packages in some cases. [P]
- IntelGuard — arXiv 2601.16458: RAG over >8,000 threat-intel reports; deployed on PyPI, 54 previously unreported malicious packages. [P]
- LAMPS / "Many Hands Make Light Work" — arXiv 2601.12148: LLM multi-agent PyPI detection. [P]
- Ibiyo et al. — arXiv 2504.13769: RAG performed poorly vs few-shot (97% accuracy, 95% balanced accuracy) for malicious PyPI code. [P] — relevant negative result for RAG-based description classifiers.
- "How Effective Are NPM Malicious Package Detectors? A Large-Scale Empirical Study" — arXiv 2603.27549 (2026): 6,420 malicious + 7,288 benign packages, 8 tools / 13 variants; GuardDog best at 93.32% F1. [P] — template for a benchmark-style evaluation of MCP scanners.
- Poster: Using CodeQL to Detect Malware in npm — CCS 2023 poster: 125 malicious packages, no false alarms reported. [poster]

---

## Transferable ideas into MCP (with entry IDs)

1. **Rug pull = malicious update; model it with update-security theory.** Treat each tool definition version as signed metadata with role separation, threshold signing, expiry/freshness and rollback/freeze protection, not just a local hash pin. [P4-01, P4-05, P4-03]
2. **Transparency log of tool-definition versions.** Append-only, publicly auditable log (Sigstore/Rekor- or skipchain-style) lets clients detect split-view attacks (a server showing different descriptions to different clients) and audit history. [P4-03, P4-05]
3. **Keyless/identity-bound or privacy-preserving signing for MCP registries.** [P4-03, P4-04]
4. **Mandate signing, don't make it optional.** Measured adoption shows optional signing fails. [P4-07]
5. **Provenance layout.** in-toto-style policy stating which identity may publish/modify which tool, checked by the gateway's policy layer. [P4-02, P4-11]
6. **Canonicalise before hashing; re-derive independently.** Reproducible-build thinking: fetch via independent path and compare canonical JSON. [P4-06, P4-16]
7. **Delta-focused analysis.** Diff trusted vs received description and analyse only changed spans; expect most diffs to be benign → need semantic classification of the delta (RQ2). [P4-16]
8. **Capability-drift detection.** An update that implies new capabilities is flagged, mirroring per-package permissions for npm updates. [P4-17]
9. **Layered pipelines reduce FPs.** Classifier → integrity/reproducibility check → clone/near-duplicate match (Amalfi); metadata + static + dynamic (Duan). Direct support for RQ3/RQ4. [P4-18, P4-15, P4-21, P4-22]
10. **Adversarially robust feature design.** Split features into easy- vs difficult-to-manipulate; weight DTM features (provenance, signer, history, schema–behaviour consistency) more heavily in the risk engine. [P4-23]
11. **Generalisation across ecosystems.** Language-neutral behaviour abstractions and lexical features transfer across npm/PyPI → test across MCP server families/languages. [P4-19, P4-24]
12. **Unsupervised outlier baseline.** Clustering/outlier ranking over many tool descriptions finds novel poisoning without labels. [P4-20]
13. **LLM-as-reviewer with pre-screening for cost/latency.** [P4-25, P4-21]; with the MCP-specific caveat that the reviewer LLM is itself injectable.
14. **Dataset construction.** Curated, characterised real incidents + attack trees as labelling taxonomy for SAFE/POISONED. [P4-10, P4-08, P4-28]
15. **Revocation and stale copies.** Malicious packages persist on mirrors; MCP clients/registries need revocation and cache expiry. [P4-28, P4-01]
16. **Ecosystem concentration risk.** A small number of servers/maintainers can affect many agents → per-server trust scores and blast-radius limits. [P4-14]

## Gaps: what supply-chain literature does not cover for natural-language tool metadata

1. **The payload is natural language read by an LLM, not code executed by an interpreter.** All detectors in Section C analyse code (install scripts, API-call graphs, behaviour sequences, ASTs). None analyse imperative instructions hidden in descriptive text whose "execution" is the LLM's interpretation. Static/dynamic code analysis has no direct counterpart; semantic NLP detection is the gap. [contrast P4-18…P4-29]
2. **Integrity ≠ safety.** TUF/in-toto/Sigstore/CHAINIAC ([P4-01]–[P4-05]) guarantee a definition is the one the publisher signed; a malicious publisher signs poisoned descriptions happily. The literature assumes the developer is trusted or detection happens elsewhere — MCP needs both layers.
3. **Legitimate-change vs malicious-change discrimination for text.** LastPyMile [P4-16] shows most diffs are benign for code; there is no established method or dataset for *semantic* drift classification of short descriptive texts (RQ2 novelty).
4. **Server-controlled, per-session dynamic metadata.** Package artifacts are immutable per version; MCP servers can serve different tool lists per client/session and change them at runtime (tools/list_changed). Split-view and per-client targeting are only partially addressed by transparency logs and not studied for agent tools.
5. **Cross-artifact influence.** In npm, malicious code mostly affects its own process; in MCP, one tool's description can steer the LLM's use of *other* servers' tools (shadowing). No supply-chain taxonomy ([P4-08], [P4-13]) has a vector for "metadata of artifact A changes how artifact B is used".
6. **Adaptive attacks against NLP/LLM detectors.** MeMPtec [P4-23] is a rare adversarial-robustness study, and only for numeric metadata; paraphrase/obfuscation attacks against text classifiers and prompt injection against LLM reviewers ([P4-25]) are unstudied in this literature.
7. **No benchmark of poisoned tool metadata.** Supply-chain work has curated malware corpora (Backstabber's [P4-10], pypi_malregistry [P4-28]); no equivalent labelled corpus exists here (to be confirmed by the MCP-specific literature agents).
8. **Runtime semantics of "capability".** npm permission work [P4-17] uses OS-level capabilities; MCP needs capabilities defined in terms of agent actions (which tools may be invoked, with which data flows), not just syscalls.
9. **Third-party LLM plugin/app-store evidence (Section D) could not be verified in this session** — to be closed before writing Related Work.
