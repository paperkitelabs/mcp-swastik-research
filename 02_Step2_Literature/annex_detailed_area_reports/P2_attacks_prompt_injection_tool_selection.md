# Step 2 — Area P2: Attacks on LLM-integrated applications and tool-using agents

Compiled 2026-10-07 for the MCP tool-description-poisoning project.

## Method and honesty notes (read first)
- Every bibliographic detail below comes from search-result snippets seen in this session: publisher, proceedings, ACL Anthology, NDSS, USENIX, NeurIPS/ICLR proceedings, ojs.aaai.org, and university repositories. Details I could not confirm are marked **UNVERIFIED**.
- **Tooling limits I hit:** the shared web-search budget (200 calls per turn) ran out partway through. WebFetch was then blocked by egress policy for arxiv.org, dl.acm.org, aclanthology.org, proceedings.iclr.cc, sciencedirect.com and scimagojr.com.
  - As a result, **no SJR quartile and no CORE rank in this file was checked on scimagojr.com or portal.core.edu.au.** All tiers are marked "per general knowledge — verify".
  - The ACM DOI for Greshake et al. is also not confirmed.
- **Gap in the journal search:** targeted searches in Q1/Q2 security journals (Computers & Security, IEEE TIFS, IEEE TDSC, ESWA, KBS, Information Fusion, IEEE COMST) turned up **no verifiable** journal paper on prompt-injection or tool-selection attacks. The search tool cannot filter by journal, so such papers may exist. They need a direct check on ScienceDirect or IEEE Xplore (see the "To verify" list in Section F).
- One citation found inside another paper's reference list could not be confirmed and is **excluded**: "Ferrag 2025, *Taxonomy and challenges of prompt injection in LLMs*, Computers & Security 145, 103241". It may be a mis-citation, so do not use it.
- Ordering follows the brief: Q1 journals → Q2/other journals → A* conferences → A conferences → others (workshops, unranked venues) → appendix of preprints.

---

## A. Journals (quartile per general knowledge — verify all on scimagojr.com)

### [P2-01] The Emerged Security and Privacy of LLM Agent: A Survey with Case Studies
- Feng He, Tianqing Zhu, Dayong Ye, Bo Liu, Wanlei Zhou, Philip S. Yu | 2025 (online AM 27 Oct 2025; published 9 Dec 2025; issue dated April 2026) | ACM Computing Surveys (journal) | Vol. 58, Issue 6
- Tier: Q1 (ACM CSUR, quartile per general knowledge — verify)
- DOI: 10.1145/3773080. Open-access copy: https://opus.lib.uts.edu.au/handle/10453/192579. arXiv 2407.19354.
- What they did: a full survey of privacy and security issues that are new to LLM agents. It covers LLM-agent fundamentals, a categorisation of threats, and the impact of those threats on humans, the environment and other agents. It then reviews defensive strategies and future trends, with case studies to make the material accessible.
- Key numbers: none seen.
- Stated limitations/gaps: points to future trends. I did not see the specific gap statements because the full text could not be fetched.
- Relevance: the main **journal-grade survey to cite** for agent threat taxonomy in the Introduction and Related Work. Use it to place tool or metadata poisoning inside the agent threat landscape.
- Verification seen: UTS repository listing (journal, volume, issue, DOI, dates, authors); arXiv record noting acceptance to CSUR.

### [P2-02] From prompt injections to protocol exploits: Threats in LLM-powered AI agents workflows
- Authors: **UNVERIFIED**. A UAEU research-portal listing appeared in results; arXiv 2506.23260 has the same title. | 2025 | Elsevier journal, ScienceDirect PII S2405959525001997 (journal) | vol/pages **UNVERIFIED**
- Tier: the PII prefix S2405-9595 matches the ISSN of **ICT Express** (my inference — verify). ICT Express quartile per general knowledge Q1/Q2 — verify.
- Link: https://www.sciencedirect.com/science/article/pii/S2405959525001997
- What they did (from the search snippet): a survey focused on indirect prompt injection (IPI) against LLM agents that use external tools. It proposes a unified end-to-end threat model for LLM-agent ecosystems that covers both host-to-tool and agent-to-agent communication. The title signals coverage of protocol-level exploits, i.e. MCP-style host↔tool protocols.
- Key numbers: none seen.
- Stated limitations/gaps: not seen.
- Relevance: **very high.** This is the closest journal survey to the MCP threat model, since it explicitly frames host-to-tool protocol communication as an attack surface. Cite it in the threat model and Related Work once the venue is confirmed.
- Verification seen: ScienceDirect URL in search results (fetch blocked); UAEU portal title; arXiv HTML 2506.23260 title.

### [P2-03] A Lifecycle-Oriented Survey of Emerging Threats and Vulnerabilities in Large Language Models
- Authors: **UNVERIFIED** (IMT Lucca repository) | 2025 | IEEE Access (journal) | vol/pages **UNVERIFIED**
- Tier: IEEE Access is generally Q1 in "Computer Science (miscellaneous)" in recent SJR years (per general knowledge — verify; some reviewers treat it as a lower-prestige megajournal).
- Link: https://iris.imtlucca.it/handle/20.500.11771/39658
- What they did: a survey that sets out to identify and examine under-explored vulnerabilities affecting LLMs, organised by LLM lifecycle stage.
- Key numbers: none seen.
- Relevance: medium. A general LLM threat survey for background; not agent- or tool-specific.
- Verification seen: search snippet stating IEEE Access 2025; IMT Lucca repository PDF link.

### [P2-04] Prompt Injection Attacks on Large Language Models: A Survey of Attack Methods, Root Causes, and Defense Strategies
- Geng T., Xu Z., Qu Y., et al. | 2025 | Computers, Materials & Continua (journal, Tech Science Press) — journal name inferred from the DOI prefix "cmc" (verify) | vol/pages **UNVERIFIED**
- Tier: CMC quartile per general knowledge Q2/Q3 — verify. Note that some institutions treat Tech Science Press journals cautiously.
- DOI: 10.32604/cmc.2025.074081. Link: https://www.sciopen.com/article/10.32604/cmc.2025.074081
- What they did: a systematic review following Kitchenham's guidelines that synthesises 128 peer-reviewed studies from 2022–2025. It traces attacks from simple direct injections to sophisticated multimodal attacks, with a table of attack methods that includes indirect injection and tool-invocation attacks.
- Key numbers: 128 studies; 2022–2025 window.
- Relevance: medium-high. A recent SLR-style taxonomy of prompt-injection attacks.
- Verification seen: SciOpen listing (authors, DOI, review type, abstract snippet).

### [P2-05] Prompt injection attacks in LLMs and AI agent systems (review) — exact title UNVERIFIED
- Authors **UNVERIFIED** | 2026 | MDPI *Information* (journal) | 2026, 17(1), 54
- Tier: MDPI Information quartile per general knowledge Q2/Q3 — verify.
- Link: preprint https://www.preprints.org/manuscript/202511.0088 (which states the peer-reviewed version appeared in Information 2026, 17(1), 54)
- What they did: a review of prompt-injection attacks on LLMs and AI agent systems. It covers research from 2023–2025 and analyses more than 120 peer-reviewed papers.
- Relevance: medium. A recent review; check the exact title before citing.
- Verification seen: Preprints.org listing snippet.

### [P2-06] Prompt Injection Detection in LLM Integrated Applications
- Lan, Kaul, Jones (first names **UNVERIFIED**) | 2025 | International Journal of Network Dynamics and Intelligence (journal) | DOI 10.53941/ijndi.2025.100013
- Tier: **unknown.** IJNDI is a young journal and its Scopus/SJR status is not verified.
- Link: https://journal.hep.com.cn/ijndi/EN/10.53941/ijndi.2025.100013
- What they did: studies the detection of prompt injections in LLM-integrated applications.
- Relevance: low-medium. A journal-format detection baseline; its ranking may be too low for the target audience.
- Verification seen: journal page in search results.

---

## B. A* conferences (CORE rank per general knowledge — verify on portal.core.edu.au)

### [P2-07] Formalizing and Benchmarking Prompt Injection Attacks and Defenses
- Yupei Liu, Yuqi Jia, Runpeng Geng, Jinyuan Jia, Neil Zhenqiang Gong | 2024 | 33rd USENIX Security Symposium (conference) | pp. 1831–1847
- Tier: CORE A* (per general knowledge — verify)
- Link: https://www.usenix.org/conference/usenixsecurity24/presentation/liu-yupei. arXiv 2310.12815. Code: Open-Prompt-Injection on GitHub.
- What they did: a formal framework for prompt-injection attacks in which existing attacks are special cases. Combining existing attacks inside the framework yields a new combined attack. They then systematically evaluate 5 attacks and 10 defenses across 10 LLMs and 7 tasks, and release the result as a common benchmark.
- Key numbers: 5 attacks × 10 defenses × 10 LLMs × 7 tasks.
- Stated limitations/gaps: attacks are effective across LLMs and tasks, and existing defenses are insufficient. Prior work was mostly case studies.
- Relevance: the **canonical formal definition** of prompt injection to adapt. Tool-description poisoning can be formalised as an injected task placed in the *tool-metadata channel* instead of the data channel. The benchmark platform also supplies detection-baseline implementations (e.g. known-answer detection).
- Verification seen: USENIX presentation page and arXiv listing in results.

### [P2-08] Prompt Injection Attack to Tool Selection in LLM Agents (ToolHijacker)
- Jiawen Shi, Zenghui Yuan, Guiyao Tie, Pan Zhou, Neil Zhenqiang Gong, Lichao Sun | 2026 | Network and Distributed System Security Symposium (NDSS 2026, 23–27 Feb 2026, San Diego) (conference)
- Tier: CORE A* (per general knowledge — verify)
- Link: https://www.ndss-symposium.org/ndss-paper/prompt-injection-attack-to-tool-selection-in-llm-agents. arXiv 2504.19793.
- What they did: an attack in a no-box setting, where the attacker does not know the target LLM or the retriever. A crafted malicious *tool document* is inserted into the tool library so that the agent's retrieval-plus-selection pipeline picks the attacker's tool for a target task. Crafting the document is posed as an optimisation problem and solved with a two-phase strategy, with gradient-free and gradient-based variants. Evaluation covers 8 LLMs and 4 retrievers on 2 benchmark datasets, including MetaTool.
- Key numbers: 96.43% attack success rate (gradient-free; Llama-3.3-70B shadow model → GPT-4o target) on MetaTool; 100% retrieval hit rate on MetaTool.
- Stated limitations/gaps: tested defenses were insufficient, and the authors call for new defenses. Prevention defenses tested: StruQ, SecAlign. Detection defenses tested: known-answer detection, DataSentinel, perplexity and windowed perplexity.
- Relevance: **core.** This is the top-venue paper closest to tool-description poisoning, because the attack payload *is* tool metadata. It shows that existing prompt-injection detectors fail on poisoned tool documents, which motivates a dedicated description-level detector plus integrity pinning. Reuse its threat model and its baseline-defense list.
- Verification seen: NDSS paper page and arXiv in search results.

### [P2-09] AgentDojo: A Dynamic Environment to Evaluate Prompt Injection Attacks and Defenses for LLM Agents
- Edoardo Debenedetti, Jie Zhang, Mislav Balunović, Luca Beurer-Kellner, Marc Fischer, Florian Tramèr | 2024 | Advances in Neural Information Processing Systems 37, NeurIPS 2024 Datasets and Benchmarks Track (conference)
- Tier: NeurIPS CORE A* (per general knowledge — verify; the D&B track is part of the main proceedings)
- DOI: 10.52202/079017-2636. Link: https://proceedings.neurips.cc/paper_files/paper/2024/hash/97091a5177d8dc64b1da8bf3e1f6fb54-Abstract.html. Project: agentdojo.spylab.ai
- What they did: an extensible environment, rather than a static test set, with 97 realistic tasks (email client, e-banking, travel booking) and 629 security test cases. It supports multi-step agent runs in which the agent chooses which tools to call, and it implements attack and defense paradigms from the literature. Unlike InjecAgent, it evaluates the agent's planning rather than a single adversarial tool output.
- Key numbers: 97 tasks; 629 security test cases.
- Stated limitations/gaps: state-of-the-art LLMs fail many tasks even without attacks. Existing attacks break some security properties but not all. The benchmark is meant to evolve with new attacks and defenses.
- Relevance: a **benchmark to reuse or extend.** Poisoned tool descriptions can be injected into AgentDojo's tool suites to measure the end-to-end impact of the gateway (utility vs. attack success), addressing RQ4 and RQ5. Because injections there arrive via tool *outputs*, it can also serve as a contrast condition.
- Verification seen: NeurIPS proceedings page, poster page and arXiv in results.

### [P2-10] Agent Security Bench (ASB): Formalizing and Benchmarking Attacks and Defenses in LLM-based Agents
- Hanrong Zhang, Jingyuan Huang, Kai Mei, Yifei Yao, Zhenting Wang, Chenlu Zhan, Hongwei Wang, Yongfeng Zhang | 2025 | International Conference on Learning Representations (ICLR 2025) (conference)
- Tier: CORE A* (per general knowledge — verify)
- Link: https://proceedings.iclr.cc/paper_files/paper/2025/hash/5750f91d8fb9d5c02bd8ad2c3b44456b-Abstract-Conference.html. Code: github.com/agiresearch/ASB
- What they did: a framework and benchmark covering 10 scenarios (e.g. e-commerce, autonomous driving, finance), 10 agents, more than 400 tools, and 27 attack/defense methods. The attacks include 10 prompt-injection attacks, a memory-poisoning attack, a novel Plan-of-Thought backdoor and 4 mixed attacks; 11 defenses are evaluated. Testing spans 13 LLM backbones with 7 metrics, including a new utility–security balance metric.
- Key numbers: highest average attack success rate 84.30%. Defenses showed limited effectiveness. (arXiv v1 reported slightly different counts; cite the ICLR version.)
- Stated limitations/gaps: vulnerabilities occur at every stage (system prompt, user prompt, tool usage, memory retrieval), and current defenses are limited.
- Relevance: an attack taxonomy across agent stages and a large tool pool. Its tool-usage-stage attacks and its utility–security metric are worth reusing for RQ4.
- Verification seen: ICLR proceedings page and poster page in results.

### [P2-11] ToolSword: Unveiling Safety Issues of Large Language Models in Tool Learning Across Three Stages
- Junjie Ye, Sixian Li, Guanyu Li, et al. (10 authors) | 2024 | Proceedings of the 62nd Annual Meeting of the ACL (Volume 1: Long Papers) (conference) | pp. 2181–2211
- Tier: ACL CORE A* (per general knowledge — verify)
- Link: https://aclanthology.org/2024.acl-long.119. arXiv 2402.10753. Data: github.com/Junjie-Ye/ToolSword
- What they did: splits tool learning into input, execution and output stages and defines six safety scenarios, two per stage:
  - input: malicious queries, jailbreak attacks;
  - execution: noisy misdirection, risky cues;
  - output: harmful feedback, error conflicts.

  They evaluate 11 open- and closed-source LLMs.
- Key numbers: 11 LLMs. Persistent problems were found even in GPT-4.
- Stated limitations/gaps: tool use can weaken safety alignment, and noise can steer tool selection.
- Relevance: a stage-based taxonomy. Tool-description poisoning sits at the input/selection stage ("noisy misdirection"), which helps position the work.
- Verification seen: ACL Anthology entry in results.

### [P2-12] BadAgent: Inserting and Activating Backdoor Attacks in LLM Agents
- Yifei Wang, Dizhan Xue, Shengjie Zhang, Shengsheng Qian | 2024 | ACL 2024 (Volume 1: Long Papers) (conference) | pp. 9811–9827
- Tier: CORE A* (per general knowledge — verify)
- DOI: 10.18653/v1/2024.acl-long.530. Code: github.com/DPamK/BadAgent
- What they did: backdoors are planted through poisoned fine-tuning data on agent tasks. An **active** attack is triggered by a concealed trigger in the input; a **passive** attack is triggered by specific environment conditions. Once triggered, the agent performs harmful tool operations.
- Key numbers: high attack success rates were reported while clean-input behaviour stayed normal (exact numbers not seen).
- Stated limitations/gaps: the backdoors survive fine-tuning on trustworthy data and data-centric defenses. Building agents on untrusted LLMs or data is risky.
- Relevance: an out-of-scope threat (model-level supply chain) to *exclude explicitly* in the threat model. The gateway assumes a benign model but untrusted tool servers.
- Verification seen: ACL Anthology entry in results.

### [P2-13] Watch Out for Your Agents! Investigating Backdoor Threats to LLM-Based Agents
- Wenkai Yang, Xiaohan Bi, Yankai Lin, Sishuo Chen, Jie Zhou, Xu Sun | 2024 | NeurIPS 2024 (main track) (conference)
- Tier: CORE A* (per general knowledge — verify)
- DOI: 10.52202/079017-3201. Link: https://neurips.cc/virtual/2024/poster/95425. Code: github.com/lancopku/agent-backdoor-attacks
- What they did: formulates a general framework of agent backdoor attacks and analyses its forms, illustrated with web-shopping scenarios. Experiments show severe backdoor vulnerability.
- Stated limitations/gaps: current textual backdoor defenses cannot easily mitigate these backdoors, so agent-specific defenses are needed.
- Relevance: the same as P2-12. Cite it to scope out model backdoors and to support the "agent-specific defenses needed" motivation.
- Verification seen: NeurIPS poster page, MLAnthology and arXiv in results.

### [P2-14] WASP: Benchmarking Web Agent Security Against Prompt Injection Attacks
- Ivan Evtimov, Arman Zharmagambetov, Aaron Grattafiori, Chuan Guo, Kamalika Chaudhuri | 2025 | NeurIPS 2025 Datasets and Benchmarks Track (conference)
- Tier: CORE A* (per general knowledge — verify)
- Link: https://papers.nips.cc/paper_files/paper/2025/hash/1c9818387f5dd0a0bc151214660f059d-Abstract-Datasets_and_Benchmarks_Track.html. Code: github.com/facebookresearch/wasp
- What they did: an end-to-end web-agent prompt-injection benchmark in a sandbox built on VisualWebArena, with realistic hijacking objectives and an attacker with limited power. It critiques earlier benchmarks for unrealistic scenarios, overly powerful attackers, or single-step evaluation.
- Key numbers: agents began executing the adversarial instruction 16–86% of the time but achieved the attacker's goal only 0–17% of the time.
- Stated limitations/gaps: a gap between being hijacked and completing the attack. Stronger attacks under realistic constraints are needed.
- Relevance: methodological lesson for evaluation. Report both "agent follows injected instruction" and "harmful action completed" when measuring tool-poisoning impact.
- Verification seen: NeurIPS proceedings and poster pages in results.

### [P2-15] DataSentinel: A Game-Theoretic Detection of Prompt Injection Attacks
- Liu et al. (full author list **UNVERIFIED**) | 2025 | IEEE Symposium on Security and Privacy (S&P 2025) (conference) | pp. 2190–2208
- Tier: CORE A* (per general knowledge — verify)
- What they did: a detection defense against prompt injection based on a game-theoretic formulation (detail from the title and citing references only).
- Relevance: a **detection baseline.** ToolHijacker (P2-08) shows DataSentinel fails against poisoned tool documents, a useful negative baseline for the semantic detector (RQ3).
- Verification seen: reference entry quoted in search results (S&P 2025, pp. 2190–2208). The S&P page itself was not seen.

### [P2-16] Prompt-to-SQL Injections in LLM-Integrated Web Applications: Risks and Defenses
- Authors **UNVERIFIED** | 2025 | IEEE/ACM 47th International Conference on Software Engineering (ICSE 2025) (conference)
- Tier: CORE A* (per general knowledge — verify)
- DOI: 10.1109/ICSE55347.2025.00007. arXiv 2308.01990.
- What they did: studies how user prompts become SQL through LangChain-style middleware. They find P2SQL vulnerabilities in five real-world applications and propose four defenses as LangChain extensions.
- Relevance: shows injection reaching backend actions through middleware; an analogy for the gateway-placement argument (defense at the middleware layer).
- Verification seen: ACM DL DOI link and arXiv in results.

---

## C. A-ranked conferences and ACL/NAACL "Findings" (Findings has no separate CORE rank; it is the parent conference's companion volume)

### [P2-17] InjecAgent: Benchmarking Indirect Prompt Injections in Tool-Integrated Large Language Model Agents
- Qiusi Zhan, Zhixiang Liang, Zifan Ying, Daniel Kang | 2024 | Findings of the Association for Computational Linguistics: ACL 2024 (conference companion) | pp. 10471–10506
- Tier: Findings of ACL; parent ACL is CORE A* (per general knowledge — verify). Findings is often rated below main-track.
- DOI: 10.18653/v1/2024.findings-acl.624. Code: uiuc-kang-lab on GitHub.
- What they did: a benchmark of 1,054 test cases across domains (finance, smart home, email). Attacks fall into two categories: direct harm to users and exfiltration of private data. They evaluate 30 LLM agents, then reinforce attacks with a "hacking prompt".
- Key numbers: ReAct-prompted GPT-4 attacked successfully 24% of the time; the hacking prompt nearly doubled the success rate.
- Stated limitations/gaps: questions broad agent deployment. AgentDojo (P2-09) criticises it as single-turn and simulated.
- Relevance: the **data-exfiltration and direct-harm attack categories** map directly onto MCP tool-poisoning goals (e.g. "read ~/.ssh and pass it as a parameter"). Use them as payload templates for the POISONED class in the labelled dataset.
- Verification seen: ACL Anthology preview page and Illinois Experts in results.

### [P2-18] Adaptive Attacks Break Defenses Against Indirect Prompt Injection Attacks on LLM Agents
- Qiusi Zhan, Richard Fang, Henil Shalin Panchal, Daniel Kang | 2025 | Findings of the ACL: NAACL 2025 (conference companion) | pp. 7101–7117
- Tier: Findings of NAACL; NAACL is CORE A (per general knowledge — verify)
- Anthology ID 2025.findings-naacl.395. Code: github.com/uiuc-kang-lab/AdaptiveAttackAgent
- What they did: evaluates eight published IPI defenses and breaks all of them with adaptive attacks.
- Key numbers: attack success rate above 50% against every defense.
- Stated limitations/gaps: defenses must be evaluated against adaptive attacks, not only static ones.
- Relevance: **critical for the evaluation design.** The semantic or ML detector must be tested against adaptive or paraphrased poisoned descriptions (the "unseen-pattern generalization" RQ), or reviewers will cite this paper against it. It also argues for non-ML layers (hash pinning, policy) that adaptive text attacks cannot bypass.
- Verification seen: ACL Anthology preview, arXiv and author blog in results.

### [P2-19] Attention Tracker: Detecting Prompt Injection Attacks in LLMs
- IBM Research and National Taiwan University authors (names **UNVERIFIED**) | 2025 | Findings of NAACL 2025 (conference companion)
- Tier: as P2-18.
- Link: https://aclanthology.org/2025.findings-naacl.123.pdf
- What they did: a training-free detector that monitors attention patterns on the instruction to flag injections, without extra model inference.
- Key numbers: AUROC up to 10.0% better than existing methods; works on small LLMs.
- Relevance: a detection baseline. It requires white-box model access, unlike a gateway that sees only text, which is a useful contrast for the design rationale.
- Verification seen: ACL Anthology PDF link and snippet in results.

### [P2-20] The Threat of PROMPTS in Large Language Models: A System and User Prompt Perspective
- Authors **UNVERIFIED** | 2025 | Findings of ACL 2025 (conference companion)
- Link: https://preview.aclanthology.org/watermark/2025.findings-acl.675
- What they did: reviews prompt-threat attack methods, focusing on prompt leakage and prompt jailbreak attacks.
- Relevance: low-medium background (system-prompt leakage is one exfiltration goal of poisoned descriptions).
- Verification seen: ACL Anthology preview in results.

---

## D. Other peer-reviewed venues (workshops, AIES, smaller proceedings)

### [P2-21] Not what you've signed up for: Compromising Real-World LLM-Integrated Applications with Indirect Prompt Injection
- Kai Greshake, Sahar Abdelnabi, Shailesh Mishra, Christoph Endres, Thorsten Holz, Mario Fritz | 2023 | Proceedings of the 16th ACM Workshop on Artificial Intelligence and Security (AISec 2023, co-located with ACM CCS) (workshop) | pp. 79–90
- Tier: workshop (no CORE rank; the parent CCS is A*). Highly cited and seminal.
- DOI: the ACM DOI 10.1145/3605764.3623985 is **UNVERIFIED** (not shown in any result). arXiv DOI 10.48550/arXiv.2302.12173.
- What they did: introduces *indirect prompt injection*, where malicious instructions are planted in content the LLM later retrieves (web pages, emails). It gives a security taxonomy of impacts — data theft, worming, information-ecosystem contamination, remote control — and demonstrates the attacks on real LLM-integrated applications.
- Relevance: **seminal motivation citation.** Tool-description poisoning is a form of indirect prompt injection in which the carrier is tool metadata rather than retrieved content. Its taxonomy of impacts frames the harms considered.
- Verification seen: arXiv record and citing-paper reference list (venue, pages) in results.

### [P2-22] LLM Platform Security: Applying a Systematic Evaluation Framework to OpenAI's ChatGPT Plugins
- Umar Iqbal, Tadayoshi Kohno, Franziska Roesner | 2024 | Proceedings of the AAAI/ACM Conference on AI, Ethics, and Society (AIES 2024) (conference) | Vol. 7, No. 1, pp. 611–623
- Tier: CORE rank **unknown/UNVERIFIED** (AAAI/ACM co-sponsored)
- DOI: 10.1609/aies.v7i1.31664. Link: https://ojs.aaai.org/index.php/AIES/article/view/31664
- What they did: builds an attack taxonomy by exploring how platform stakeholders (platform, users, third-party plugins) could attack one another. It argues that third-party plugin code cannot be trusted by default and that natural-language interfaces are imprecise. They apply the framework to OpenAI's plugin ecosystem and find real plugins exhibiting the risks.
- Relevance: **direct predecessor of MCP's threat model.** Third-party plugin or tool providers are untrusted and communicate via NL descriptions. Cite it for the "capabilities must come from explicit policy, not descriptions" principle.
- Verification seen: ojs.aaai.org article page and arXiv in results.

### [P2-23] Ignore Previous Prompt: Attack Techniques For Language Models
- Fábio Perez, Ian Ribeiro | 2022 | NeurIPS 2022 ML Safety Workshop (workshop); one listing reports a Best Paper Award (**UNVERIFIED**)
- Tier: workshop
- Link: https://neurips.cc/virtual/2022/65627. arXiv 2211.09527. Code: agencyenterprise/PromptInject
- What they did: PromptInject, a mask-based iterative framework for composing adversarial prompts against GPT-3. It studies goal hijacking and prompt leaking.
- Key numbers: 58.6% goal hijacking and 23.6% prompt leaking across 35 application prompts (from a secondary ae.studio summary; confirm in the paper).
- Relevance: seminal origin of direct prompt injection ("ignore previous instructions"). Lexical patterns like this belong in the rule-based layer.
- Verification seen: NeurIPS virtual page, MLAnthology and arXiv in results.

### [P2-24] How Not to Detect Prompt Injections with an LLM
- Authors **UNVERIFIED** | 2025 | ACM proceedings, DOI 10.1145/3733799.3762980 (venue likely AISec 2025 — **UNVERIFIED**)
- Link: https://dl.acm.org/doi/10.1145/3733799.3762980
- What they did: formally characterises known-answer detection (KAD), which had reported near-perfect results, and identifies a structural vulnerability that undermines its security premise.
- Relevance: argues against relying solely on LLM-based detectors, which supports a layered gateway with non-LLM integrity and policy layers.
- Verification seen: ACM DL link and snippet in results.

### [P2-25] Prompt Injection Attacks on Large Language Models: Multi-Model Security Analysis (title truncated — **UNVERIFIED**)
- Authors **UNVERIFIED** | 2025 | KDIR 2025 (SciTePress proceedings) (conference)
- Tier: low (CORE B/C or unranked — verify)
- Link: https://www.scitepress.org/Papers/2025/138384/138384.pdf
- What they did: injection tests across several LLM architectures, comparing detection performance by attack type. Indirect phrasing, metaphor, multi-step scenarios, and especially jailbreak- or roleplay-based attacks reduced filter effectiveness.
- Relevance: low. Evidence that filter-style detectors degrade under obfuscated phrasing.
- Verification seen: SciTePress PDF snippet.

---

## E. Appendix — arXiv-only preprints (seminal or directly on tool-metadata attacks; no peer-reviewed venue confirmed)

### [P2-26] ToolTweak: An Attack on Tool Selection in LLM-based Agents — arXiv 2510.02554 (Oct 2025)
- Jonathan Sneh et al. (Univ. of Oxford & Microsoft; full author list **UNVERIFIED**).
- Threat model: the attacker is a legitimate marketplace tool provider who can edit the tool's name and description but not its parameter schema, with black-box access to the model.
- Method: iteratively rewrites the name and description using LLM feedback to maximise selection.
- Key numbers: selection rate rose from about 20% to as high as 81%, with transfer between open and closed models.
- Defenses evaluated: paraphrasing and perplexity filtering, which reduced the bias.
- **Highly relevant.** It is the purest "description manipulation" attack and directly motivates description-drift and semantic checks. Note that its manipulation is commercial bias rather than malicious instructions, a distinct POISONED sub-class to consider.

### [P2-27] Attractive Metadata Attack (Mo et al.) — arXiv 2508.02110
- Manipulates tool metadata (names, descriptions, parameter schemas) to influence agent behaviour without prompt injection or model access.
- Venue **UNVERIFIED**; it may have appeared at a 2025 conference, so check before citing.
- Highly relevant: schema-level poisoning, so the integrity hash must cover the whole tool definition, not just the description.

### [P2-28] "Select Me! When You Need a Tool: A Black-box Text Attack on Tool Selection" — arXiv 2504.04809
- Black-box text attack on the tool-selection step. Venue **UNVERIFIED**.

### [P2-29] ToolFlood (Jawad & Brunel) — arXiv 2603.13950
- Attacks the retrieval stage by flooding it with a few attacker-controlled tools.
- Relevant to multi-server MCP setups where a malicious server registers many tools.

### [P2-30] Imprompter: Tricking LLM Agents into Improper Tool Use — arXiv 2410.14923 (Oct 2024)
- Xiaohan Fu, Shuheng Li, Zihan Wang, Yihao Liu, Rajesh K. Gupta, Taylor Berg-Kirkpatrick, Earlence Fernandes (UCSD, NTU).
- Automatically optimised, *obfuscated* prompts make agents misuse tools, e.g. exfiltrating PII via a markdown image URL in Mistral LeChat.
- Key numbers: nearly 80% end-to-end success.
- **No peer-reviewed venue found** in this session (the brief's guess of a venue is UNVERIFIED).
- Relevance: obfuscated payloads defeat visual inspection and keyword rules, which argues for embedding-, ML- and behaviour-based layers.

### [P2-31] MalTool: Malicious Tool Attacks on LLM Agents — arXiv 2602.12194 (2026)
- Malicious-tool attacks on LLM agents; only the title was seen. Highly relevant topic; read before citing.

### [P2-32] ContextLeak: Exfiltrating LLM Agent Context via Malicious Tools — arXiv 2608.27800 (2026)
- Only the title was seen. Directly relevant: malicious tools exfiltrating context.

### [P2-33] TRUSTDESC: Preventing Tool Poisoning in LLM Applications via Trusted Description Generation — arXiv 2604.07536 (2026)
- A defense, listed here because it is the **closest competing approach**: it regenerates trusted descriptions instead of detecting poisoned ones.
- Must be compared in Related Work.

### [P2-34] Shorter supporting preprints
- **The Landscape of Prompt Injection Threats in LLM Agents: From Taxonomy to Analysis** — arXiv 2602.10453 (2026).
- **Systematic literature review of prompt-injection mitigation** (88 studies, extends the NIST taxonomy) — arXiv 2601.22240.
- **Navigating the Risks: A Survey of Security, Privacy, and Ethics Threats in LLM-Based Agents** — arXiv 2411.09523. Venue UNVERIFIED.
- **AI Agents Under Threat: A Survey of Key Security Challenges and Future Pathways** — arXiv 2406.02630; reviews 100+ papers. A journal version (possibly ACM CSUR) is UNVERIFIED; check, since if confirmed it is a Q1 citation.
- **A Survey on Trustworthy LLM Agents: Threats and Countermeasures** (Yu et al., 2025). Venue UNVERIFIED. Taxonomy: intrinsic components (LLM core, memory, tools) and extrinsic interactions (agent-to-agent, agent-to-environment, agent-to-user).
- **Indirect Prompt Injections: Are Firewalls All You Need, or Stronger Benchmarks?** — arXiv 2510.05244.
- **Towards Action Hijacking of LLM-based Agent** — arXiv 2412.10807.
- **TopicAttack** — arXiv 2507.13686.
- **IterInject** — arXiv 2605.24659.
- **A Survey on the Safety and Security Threats of Computer-Using Agents** — arXiv 2505.10924.
- **Prompt Injection Attack against LLM-integrated Applications** (Liu et al., HouYi) — arXiv 2306.05499. Seminal; venue not confirmed.

---

## F. To verify next (not confirmed in this session — **do not cite until checked**)
The search budget ran out before these could be checked. All are well-known to me, but their venue and details are **UNVERIFIED**:
- AgentPoison (memory/RAG poisoning of agents), likely NeurIPS 2024.
- EIA, Environmental Injection Attack on generalist web agents, likely ICLR 2025.
- PoisonedRAG, likely USENIX Security 2025.
- ToolEmu ("Identifying the Risks of LM Agents with an LM-Emulated Sandbox"), likely ICLR 2024.
- AgentHarm, likely ICLR 2025.
- BIPIA ("Benchmarking and Defending Against Indirect Prompt Injection Attacks on LLMs"), possibly KDD 2025.
- Neural Exec, possibly AISec 2024.
- HackAPrompt, possibly EMNLP 2023.
- Tensor Trust, possibly ICLR 2024.
- R-Judge, possibly Findings of EMNLP 2024.
- Sleeper Agents (Anthropic), arXiv 2024.
- MCP-specific attack benchmarks:
  - **MCPTox** (tool poisoning on real MCP servers), possibly AAAI 2026;
  - **MCP Security Bench (MSB)**;
  - "MCP Safety Audit";
  - Hou et al., "MCP: Landscape, Security Threats and Future Research Directions".
- Journal sweep still needed: search ScienceDirect for "prompt injection" in Computers & Security, JISA, ESWA, KBS, Information Fusion and EAAI (2024–2026), and IEEE Xplore for TIFS, TDSC and IEEE Access. **None was verifiable in this session.**
- Quartile and rank checks: scimagojr.com for ACM CSUR, ICT Express, IEEE Access, CMC, MDPI Information and IJNDI; portal.core.edu.au for AIES, NAACL and NDSS.

---

## Gaps stated across this literature (synthesis)
1. **Existing prompt-injection defenses do not transfer to tool-metadata attacks.**
   - ToolHijacker [P2-08] shows StruQ, SecAlign, known-answer detection, DataSentinel [P2-15] and perplexity detectors are all insufficient against poisoned tool documents.
   - ToolTweak [P2-26] finds that only paraphrasing and perplexity filtering partly mitigate it.
   - → Dedicated, description-level detection is an open need, which is the project's core claim.
2. **Defenses are evaluated against static, not adaptive, attacks.** Adaptive attacks broke 8 of 8 IPI defenses at over 50% ASR [P2-18]. Static detectors and LLM-based detectors are structurally fragile [P2-24, P2-25, P2-30]. → Evaluate against adaptive or paraphrased poisoned descriptions, and favour layers that text attacks cannot bypass (hashing, signatures, policy).
3. **Benchmarks focus on injection via tool *outputs* or retrieved data, not tool *definitions*.** InjecAgent [P2-17], AgentDojo [P2-09], WASP [P2-14] and Greshake [P2-21] carry payloads in data returned at runtime. Tool-selection works [P2-08, P2-26–P2-29] target *which* tool is chosen. **No verified top-venue benchmark** in this set offers a labelled SAFE/POISONED corpus of tool definitions with *rug-pull (post-approval change)* scenarios. → The planned dataset fills that gap.
4. **Realism gap between hijacking and attack completion.** WASP reports 16–86% hijack but only 0–17% goal completion [P2-14]. AgentDojo notes that utility failures confound security results [P2-09]. → Report both behavioural compliance and harmful-action completion, plus utility (benign-task success) with the gateway on [P2-10's utility–security metric].
5. **Untrusted third-party extensions and natural-language ambiguity are unresolved platform-design problems** [P2-22]. Surveys call for agent-specific, multi-layer defenses [P2-01, P2-02, P2-13]. → Supports a layered gateway with capability policies separated from NL descriptions.
6. **Defenses keep lagging new attacks.** ASB finds high ASR (84.30%) at every agent stage, with limited defense effectiveness [P2-10]. ToolSword shows tool use erodes safety alignment [P2-11]. Backdoor works show model-level threats current defenses cannot remove [P2-12, P2-13]. → The threat model should state explicitly that model backdoors are out of scope.
7. **Journal-literature gap.** The verified journal literature on these attacks is so far mostly *surveys* [P2-01–P2-05]. No Q1/Q2 journal paper presenting an empirical *tool-description poisoning detector* was found. → This is an opening for a Q1/Q2 submission, but an exhaustive journal sweep (Section F) is still needed before claiming novelty.
