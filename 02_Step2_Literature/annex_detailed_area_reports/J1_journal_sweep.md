# Step 2 / J1: Journal-only sweep (MCP security, prompt injection, LLM-agent/tool security, LLM supply chain, guardrails)

Sweep date: 2026-10-07. Method: about 75 WebSearch queries, some limited to publisher domains (sciencedirect.com, ieeexplore.ieee.org, dl.acm.org, link.springer.com, mdpi.com, cybersecurity.springeropen.com). WebFetch was blocked for sciencedirect.com, api.semanticscholar.org and api.openalex.org, and scimagojr.com was not reached. Every bibliographic detail below comes from a search-result snippet or from a search summary of a publisher, repository or arXiv page. **No SJR quartile was verified on scimagojr.com in this sweep.** All quartiles are therefore labeled "per general knowledge — verify".

Legend for "Verification seen": **PUB** = publisher or indexing page seen (ACM DL, ScienceDirect, MDPI, SpringerOpen, Springer, IEEE Xplore, hep.com.cn, Crossref, DOAJ). **REF** = only cited in another paper's reference list. **REPO** = institutional repository or NSF PAR. **ARX** = arXiv version.

---

## Bottom line (read first)

1. **Peer-reviewed journal papers specifically on MCP tool-description poisoning are very rare.** Only three were confirmed:
   - **(a)** Hou et al., *TOSEM* (DOI 10.1145/3796519): an MCP landscape and threat taxonomy.
   - **(b)** Huang et al., *Journal of Cybersecurity and Privacy* (MDPI) 6(3):84, 2026 (DOI 10.3390/jcp6030084): MCP threat modeling plus client-side tool-poisoning experiments.
   - **(c)** Ferrag et al., *ICT Express* 2025 (ScienceDirect PII S2405959525001997): a threat taxonomy that includes MCP protocol exploits.

   Almost every other MCP-security work (MCPTox, MindGuard, ETDI, MCPSecBench, MCP-Guard, SMCP, Jamshidi et al., Gaire et al. SoK, Hasan et al.) is an arXiv preprint or a conference paper. MCPTox is in the AAAI 2026 proceedings. **This gap supports the proposal: a Q1/Q2 journal paper with an empirical gateway evaluation would be among the first.**
2. Journal coverage of prompt injection, jailbreaks and agent security is mostly **surveys** (ACM CSUR ×4, Information Fusion, Neural Networks, JISA, AI Review ×2, Cybersecurity, High-Confidence Computing, MDPI Information, CMC). There are few journal papers on detectors: JailGuard (TOSEM), two IJIS 2026 papers, and the Neurocomputing taxonomy.
3. Supply-chain framing has strong Q1 anchors in TOSEM: Williams et al. 2025, Wang et al. "LLM Supply Chain: A Research Agenda", and Zhao et al. "LLM App Store Analysis".

---

## TIER Q1 (per general knowledge — verify on scimagojr.com)

### 1. Model Context Protocol (MCP): Landscape, Security Threats, and Future Research Directions
- **Authors:** Xinyi Hou, Yanjie Zhao, Shenao Wang, Haoyu Wang (HUST)
- **Journal:** ACM Transactions on Software Engineering and Methodology (TOSEM)
- **Year / Vol:** Accepted Feb 2026. Shown on the TOSEM page in the issue-in-progress for **Vol. 35, Issue 10 (Oct 2026)**. Article number UNVERIFIED.
- **DOI:** 10.1145/3796519. Link: https://dl.acm.org/doi/10.1145/3796519. arXiv: 2503.23278. Also listed in the FSE 2026 journal-first track (conf.researchr.org).
- **Summary:** Surveys MCP architecture and the MCP server lifecycle in four phases (creation, deployment, operation, maintenance) with 16 activities. Builds a threat taxonomy around four attacker types (malicious developers, external attackers, malicious users, security flaws), giving 16 threat scenarios. Validates risks with real-world case studies and proposes safeguards per lifecycle phase. Also surveys industry adoption, integration patterns and tooling.
- **Stated limitations / gaps:** A position and landscape paper with no detector or gateway implementation and no quantitative detection evaluation. It calls for future work on server vetting, versioning and integrity, and on runtime controls. Exact gap wording UNVERIFIED; only the abstract was seen.
- **Relevance:** **Very high.** It is the canonical journal taxonomy for MCP threats, and its malicious-developer scenarios include tool poisoning, rug pull and name collision. Use it to frame the attack taxonomy and lifecycle-stage placement of the gateway: integrity at install and update, the detector at registration, and the runtime monitor at operation.
- **Quartile:** TOSEM is Q1 (Software) per general knowledge — verify.
- **Verification seen:** PUB (ACM DL page and TOSEM issue listing via search), ARX, REF.

### 2. The Emerged Security and Privacy of LLM Agent: A Survey with Case Studies
- **Authors:** Feng He, Tianqing Zhu, Dayong Ye, Bo Liu, Wanlei Zhou, Philip S. Yu
- **Journal:** ACM Computing Surveys. **Vol. 58, Issue 6, Article 162**, published 9 Dec 2025.
- **DOI:** 10.1145/3773080. Link: https://dl.acm.org/doi/10.1145/3773080. arXiv: 2407.19354.
- **Summary:** Surveys privacy and security threats to LLM agents. It splits them into threats inherited from LLMs and agent-specific threats, including tool manipulation that compromises privacy or executes malicious code. It reviews defenses and future trends, uses a "virtual town" running case study, and draws on a review of 800+ papers per the arXiv text.
- **Stated limitations / gaps:** A conceptual survey with no MCP-specific treatment seen in the snippets. Notes that defenses lag behind agent capabilities. Detailed gap text UNVERIFIED.
- **Relevance:** High for background and threat taxonomy, since it covers tool misuse by agents. Low for MCP-specific mechanisms.
- **Quartile:** CSUR is Q1 per general knowledge — verify.
- **Verification seen:** PUB (ACM DL via search), ARX.

### 3. AI Agents Under Threat: A Survey of Key Security Challenges and Future Pathways
- **Authors:** Zehang Deng, Yongjian Guo, et al. (full list UNVERIFIED)
- **Journal:** ACM Computing Surveys **57(7), Article 182**, July 2025, pp. 1–36.
- **DOI:** 10.1145/3716628. Crossref record seen in search results. arXiv: 2406.02630.
- **Summary:** Organizes agent security threats into four knowledge gaps: unpredictable multi-step user inputs, complex internal execution, variable operating environments, and **interactions with untrusted external entities**. A third-party summary says it reviewed 100+ papers from Jan 2022 to Apr 2024.
- **Stated limitations / gaps:** Its coverage ends in April 2024, before MCP. It frames untrusted external entities, which include tools, as an open gap.
- **Relevance:** High. The "untrusted external entities" gap maps directly onto untrusted MCP servers and tool metadata.
- **Quartile:** Q1 per general knowledge — verify.
- **Verification seen:** Crossref (via search), ARX, REF.

### 4. Unique Security and Privacy Threats of Large Language Models: A Comprehensive Survey
- **Authors:** Shang Wang, Tianqing Zhu, et al. (full list UNVERIFIED)
- **Journal:** ACM Computing Surveys **58(4), Article 83**, published 6 Oct 2025.
- **DOI:** 10.1145/3764113. Link: https://dl.acm.org/doi/10.1145/3764113.
- **Summary:** Builds a threat-model taxonomy across four scenarios: pre-training, fine-tuning, deployment, and LLM-based agents. Argues that earlier surveys lacked such a scenario-based taxonomy.
- **Limitations / gaps:** Broad scope, so agent and tool coverage is one section. Details UNVERIFIED.
- **Relevance:** Medium. Useful for positioning tool poisoning as a deployment-time and agent-scenario threat.
- **Quartile:** Q1 per general knowledge — verify.
- **Verification seen:** PUB (ACM DL via search).

### 5. Security and Privacy Challenges of Large Language Models: A Survey
- **Authors:** Badhan Chandra Das, M. Hadi Amini, Yanzhao Wu
- **Journal:** ACM Computing Surveys **57(6)**, 2025. Article number and DOI UNVERIFIED. arXiv: 2402.00888.
- **Summary:** A general survey of LLM security and privacy: jailbreaks, prompt injection, data poisoning, privacy leakage, and defenses.
- **Relevance:** Low to medium. Background only.
- **Quartile:** Q1 per general knowledge — verify.
- **Verification seen:** Search summary of the ACM DL listing; ARX. DOI not seen.

### 6. A Comparative Survey of Security Risks in AI Systems: From LLMs to AI Agents and Embodied Agents
- **Authors:** Baiqi Wu, Qingming Li, Chunyi Zhou, Ting Wang, Shouling Ji
- **Journal:** ACM Computing Surveys **58(15), Article 392**, 2026.
- **DOI:** Likely 10.1145/3837083, inferred from the dl.acm.org PDF URL seen. Mark UNVERIFIED as the DOI.
- **Summary:** Compares security risks across LLMs, AI agents and embodied agents.
- **Relevance:** Medium. Useful for positioning agents' tool-use attack surface.
- **Quartile:** Q1 per general knowledge — verify.
- **Verification seen:** Search summary of the ACM DL listing (PDF link 10.1145/3837083).

### 7. JailGuard: A Universal Detection Framework for Prompt-based Attacks on LLM Systems
- **Authors:** Xiaoyu Zhang et al., from Xi'an Jiaotong Univ. and NTU (full list UNVERIFIED)
- **Journal:** ACM TOSEM, 2025. The XJTU portal shows a journal article dated Dec 2025. Vol/issue UNVERIFIED.
- **DOI:** 10.1145/3724393. Link: https://dl.acm.org/doi/full/10.1145/3724393. arXiv: 2312.10766.
- **Summary:** Detects jailbreaking and hijacking (prompt-injection) attacks by mutating untrusted inputs with 18 text and image mutators plus a combination policy. It measures how far the target model's responses diverge across variants, on the premise that attacks are less robust than benign inputs. The authors built a dataset of 11,000 samples covering 15 attack types. Reported detection accuracy is 86.14% on text and 82.90% on images, beating the state of the art by 11.81–25.73% and 12.20–21.40%.
- **Stated limitations:** Hyperparameters are model-specific and must be tuned per target LLM system. It may fail on some unseen attacks. Multiple model queries per input add cost.
- **Relevance:** High for the **detector baseline and evaluation design**. It is a journal-published, model-agnostic injection detector. Its divergence idea is analogous to semantic drift between a trusted and a received description, but it targets prompts, not tool metadata. Its unseen-attack weakness motivates the proposal's RQ on unseen-pattern generalization.
- **Quartile:** TOSEM is Q1 per general knowledge — verify.
- **Verification seen:** PUB (ACM DL full-text page via search), ARX, REPO (XJTU).

### 8. Large Language Model Supply Chain: A Research Agenda
- **Authors:** Shenao Wang, Yanjie Zhao, Xinyi Hou, Haoyu Wang
- **Journal:** ACM TOSEM, 2025 (2030 Roadmap for SE special issue; listed with Vol. 34 No. 5 content). Exact vol/issue/article UNVERIFIED.
- **DOI:** 10.1145/3708531. Link: https://dl.acm.org/doi/10.1145/3708531. arXiv: 2404.12736.
- **Summary:** Defines the LLM supply chain in three layers: infrastructure (compute, datasets, toolchains), the foundation-model lifecycle, and the **downstream application ecosystem**. Sets out a research agenda from software-engineering and security & privacy perspectives.
- **Stated limitations / gaps:** A vision paper. A later paper (arXiv 2504.20763) criticizes it for not clearly defining the scope of supply-chain elements.
- **Relevance:** High for the supply-chain framing. MCP servers and tools are downstream ecosystem components, and pinning and signatures are supply-chain integrity controls.
- **Quartile:** Q1 per general knowledge — verify.
- **Verification seen:** PUB (ACM DL via search), ARX.

### 9. LLM App Store Analysis: A Vision and Roadmap
- **Authors:** Yanjie Zhao, Xinyi Hou, Shenao Wang, Haoyu Wang
- **Journal:** ACM TOSEM **34(5), Article 125, pp. 1–25**, published 24 May 2025.
- **DOI:** 10.1145/3708530. Link: https://dl.acm.org/doi/10.1145/3708530. arXiv: 2404.12737.
- **Summary:** A vision for analyzing LLM app stores (GPT Store and similar) covering data mining, **security risk identification**, development assistance and market dynamics. Argues for governance frameworks.
- **Limitations:** Self-described as visionary, with no concrete framework or evaluation.
- **Relevance:** Medium. A third-party tool and app ecosystem is analogous to MCP registries and marketplaces, which supports the supply-chain and vetting motivation.
- **Quartile:** Q1 per general knowledge — verify.
- **Verification seen:** PUB (ACM DL via search), ARX.

### 10. Research Directions in Software Supply Chain Security
- **Authors:** Laurie Williams, Giacomo Benedetti, Sivana Hamer, Ranindya Paramitha, Imranur Rahman, Mahzabin Tamanna, Greg Tystahl, Nusrat Zahan, Patrick Morrison, Yasemin Acar, Michel Cukier, Christian Kästner, Alexandros Kapravelos, Dominik Wermke, William Enck
- **Journal:** ACM TOSEM **34(5)**, 2025, pp. 1–38 (per NCSU record; Jan 2025 date)
- **DOI:** 10.1145/3714464. This DOI was seen only on the NCSU library record, so verify it at doi.org.
- **Summary:** Uses SolarWinds, log4j and xz-utils as motivating attacks. Draws on practitioner outreach to set a research agenda for closing software supply-chain attack vectors, including artifact integrity, provenance, signing and dependency trust.
- **Relevance:** Medium to high. It is the journal anchor for treating MCP servers and tool definitions as supply-chain artifacts, and for SHA-256 pinning and Ed25519 signatures as provenance and integrity controls.
- **Quartile:** Q1 per general knowledge — verify.
- **Verification seen:** REPO (NCSU, Paderborn, NSF PAR).

### 11. Security of LLM-based agents regarding attacks, defenses, and applications: A comprehensive survey
- **Authors:** Yaxin Tang, Yijia Liu, Jiahe Lan, Zheng Yan, Erol Gelenbe. Authors were taken from citing papers' reference lists, not seen on ScienceDirect, so verify.
- **Journal:** Information Fusion, 2025 (article no. **103941**). Volume UNVERIFIED.
- **DOI:** 10.1016/j.inffus.2025.103941. Link: https://www.sciencedirect.com/science/article/abs/pii/S1566253525010036
- **Summary:** Gives a systematic taxonomy of attacks on LLM-based agents (prompt injection, jailbreaks, unsafe tool use, memory poisoning, reasoning failures) and of defenses. Also reviews agents as cyber-offense and cyber-defense applications.
- **Limitations:** Not seen.
- **Relevance:** High for the related-work taxonomy, since it covers unsafe tool use. MCP-specific content is unknown.
- **Quartile:** Information Fusion is Q1 per general knowledge — verify.
- **Verification seen:** PUB (ScienceDirect listing via search), REF.

### 12. Attack and defense techniques in large language models: A survey and new perspectives
- **Authors:** Zhiyu Liao, Kang Chen, Yuanguo Lin, Kangkang Li, Yunxuan Liu, Hefeng Chen, Xingwang Huang, Yuanhui Yu (from arXiv)
- **Journal:** **Neural Networks.** Inferred from the ScienceDirect PII S0893608025012699, whose ISSN 0893-6080 belongs to Neural Networks, and the exact title match. Year 2025 per the PII. Vol/article/DOI UNVERIFIED.
- **Link:** https://www.sciencedirect.com/science/article/abs/pii/S0893608025012699. arXiv: 2505.00976.
- **Summary:** Classifies attacks into adversarial prompting, optimized attacks, model theft, and attacks on LLM applications. Classifies defenses as prevention-based or detection-based.
- **Stated gaps:** Calls for adaptive and scalable defenses, explainable security techniques, and standardized evaluation frameworks.
- **Relevance:** Medium. The prevention-versus-detection split helps position the gateway, which does both.
- **Quartile:** Neural Networks is Q1 per general knowledge — verify.
- **Verification seen:** PUB listing seen in results (title + PII); ARX.

### 13. Security concerns for Large Language Models: A survey
- **Authors:** Miles Q. Li, Benjamin C. M. Fung
- **Journal:** Journal of Information Security and Applications (JISA) **Vol. 95 (2025), Article 104284**
- **DOI:** UNVERIFIED (likely 10.1016/j.jisa.2025.104284, not seen). Link: https://www.sciencedirect.com/science/article/abs/pii/S2214212625003217. arXiv: 2505.18889.
- **Summary:** Covers prompt injection and jailbreaking as inference-time manipulation, training-time poisoning and backdoors, misuse, and risks from autonomous agents (misalignment, deception, scheming). Reviews defenses and their limitations for studies from 2022–2025.
- **Stated gaps:** Argues that existing taxonomies are "conceptually muddled", for example by treating prompt injection (a technique) and jailbreak (an objective) as parallel categories.
- **Relevance:** Medium. Useful for precise terminology: tool poisoning is a technique, an indirect injection via metadata.
- **Quartile:** JISA is Q1/Q2 per general knowledge — verify.
- **Verification seen:** PUB (ScienceDirect listing), REF (vol 95, 104284 in a citing paper), ARX.

### 14. From prompt injections to protocol exploits: Threats in LLM-powered AI agents workflows
- **Authors:** Mohamed Amine Ferrag, Norbert Tihanyi, Djallel Hamouda, Leandros Maglaras, Abderrahmane Lakas, Merouane Debbah. Lakas appears on the UAEU record but not in some citations, so check the final author list.
- **Journal:** **ICT Express** (Elsevier / KICS), 2025. The UAEU research portal showed "Accepted/In press – 2025". Volume/issue/pages UNVERIFIED.
- **DOI:** UNVERIFIED (10.1016/j.icte.2025.xx not seen). Link: https://www.sciencedirect.com/science/article/pii/S2405959525001997. arXiv: 2506.23260 (v2, Dec 2025).
- **Summary:** Builds an end-to-end threat model for LLM-agent ecosystems that covers host-to-tool and agent-to-agent communication. Catalogs 30+ attack techniques in four domains: Input Manipulation, Model Compromise, System & Privacy Attacks, and **Protocol Vulnerabilities (MCP, ACP, ANP, A2A)**. Assesses real-world feasibility and existing defenses. Examples include Prompt-to-SQL injection and the "Toxic Agent Flow" exploit against GitHub's MCP server. Claims to be the first integrated taxonomy bridging input-level and protocol-layer exploits.
- **Stated gaps:** Argues that plugins, connectors and inter-agent protocols have outpaced security practice. Calls for protocol-level defenses (details UNVERIFIED).
- **Relevance:** **Very high.** It is a journal source that explicitly covers MCP tool-poisoning-class threats in a protocol taxonomy.
- **Quartile:** ICT Express is Q1 per general knowledge — verify. This is uncertain; it may be Q1/Q2 depending on category.
- **Verification seen:** PUB (ScienceDirect PII page title in results), REPO (UAEU portal), ARX.

### 15. Safeguarding large language models: a survey
- **Authors:** Yi Dong, Ronghui Mu, et al. (Univ. of Liverpool; full list UNVERIFIED)
- **Journal:** Artificial Intelligence Review **58(12), Article 382**, Dec 2025.
- **DOI:** UNVERIFIED (Springer s10462-… not seen). Open access: PMC12532640; Liverpool repository 3195295. arXiv: 2406.02622.
- **Summary:** A systematic review of guardrail mechanisms used by LLM providers and open source (Llama Guard, NeMo Guardrails, Guardrails AI, etc.). Covers hallucination, fairness and privacy properties, attacks that circumvent guardrails, and defenses. Proposes a vision for comprehensive guardrails using multidisciplinary, neural-symbolic and SDLC-based design.
- **Stated limitations:** Several challenges cannot easily be handled by current methods. Guardrails are complex because they mediate human–LLM interaction.
- **Relevance:** Medium to high for the guardrail/classifier layer and the risk-engine design. It is input/output-centric, not tool-metadata-centric, which is a gap the proposal fills.
- **Quartile:** AI Review is Q1 per general knowledge — verify.
- **Verification seen:** REPO (PMC, Liverpool), ARX.

### 16. LLM agents security duality: a comprehensive survey of self-security and empowered cybersecurity
- **Authors:** Yiwei Xu, Yong Zhuang, Xuanming Liu, Tian Zhang, Bowen Xiao, Xiaoyang Xu, Delong Jiang, Juan Wang, Hongxin Hu (taken from the arXiv listing of the same title)
- **Journal:** Artificial Intelligence Review **(2026) 59:174**. Received 19 Oct 2025, accepted 7 Apr 2026, online 9 May 2026.
- **DOI:** 10.1007/s10462-026-11563-0. Link: https://link.springer.com/article/10.1007/s10462-026-11563-0
- **Summary:** Part 1 covers threats to LLM agents (internal and external attack surfaces, a taxonomy by threat source), their mitigations and evaluation frameworks. Part 2 covers agents that support the cyber offense–defense lifecycle. Notes that tool use widens the attack surface.
- **Relevance:** Medium to high. It is a recent Q1 survey to cite for external, tool-related attack surfaces.
- **Quartile:** Q1 per general knowledge — verify.
- **Verification seen:** PUB (Springer page and PDF via search), ARX (2606.28450).

### 17. A domain-based taxonomy of jailbreak vulnerabilities in large language models
- **Authors:** Carlos Peláez-González, Andrés Herrera-Poyatos, Cristina Zuheros, David Herrera-Poyatos, Virilo Tejedor, Francisco Herrera (Univ. of Granada)
- **Journal:** Neurocomputing **Vol. 683, Article 133534**, 2026 (repository date 2026-04-13)
- **DOI:** 10.1016/j.neucom.2026.133534. Repository: https://digibug.ugr.es/handle/10481/112788. arXiv: 2504.04976.
- **Summary:** Classifies jailbreaks by the alignment weakness they exploit rather than by how the prompt is built. Its four categories are mismatched generalization, competing objectives, adversarial robustness, and mixed attacks. Sub-classifies by modality, model access, noise, stealthiness and generation method.
- **Relevance:** Low to medium. A methodological model for a taxonomy of poisoning patterns organized by exploited weakness, such as instruction-following, authority impersonation or hidden-channel.
- **Quartile:** Neurocomputing is Q1 per general knowledge — verify.
- **Verification seen:** REPO (UGR digibug with DOI), ARX.

### 18. When LLMs meet cybersecurity: a systematic literature review
- **Authors:** Jie Zhang, Haoyu Bu, Hui Wen, Yongji Liu, Haiqiang Fei, Rongrong Xi, Lun Li, Yun Yang, Hongsong Zhu, Dan Meng (IIE, CAS)
- **Journal:** Cybersecurity (SpringerOpen) **Vol. 8, No. 1, pp. 1–41** (DOAJ; Feb 2025)
- **DOI:** 10.1186/s42400-025-00361-w. Link: https://cybersecurity.springeropen.com/articles/10.1186/s42400-025-00361-w
- **Summary:** An SLR of 300+ works on LLMs for cybersecurity. Its section on LLM security covers jailbreaks (Shen et al.'s 6,387 prompts), HOUYI black-box prompt injection, Virtual Prompt Injection, and dataset-based robustness fine-tuning.
- **Relevance:** Low to medium. Background on injection attacks; not tool-focused.
- **Quartile:** Cybersecurity (SpringerOpen) is Q1 per general knowledge — verify.
- **Verification seen:** PUB (SpringerOpen), DOAJ, ARX.

### 19. Bridging AI and software security: A comparative vulnerability assessment of LLM agent deployment paradigms
- **Authors:** Tarek Gasmi, Ramzi Guesmi, Ines Belhadj, Jihene Bennaceur (from arXiv 2507.06323)
- **Journal:** **Information Sciences.** Inferred from the ScienceDirect PII S0020025526001623, whose ISSN 0020-0255 belongs to Information Sciences, plus the exact title on ScienceDirect and a citing reference. Year 2026. Vol/DOI UNVERIFIED.
- **Link:** https://www.sciencedirect.com/science/article/abs/pii/S0020025526001623
- **Summary:** Compares **Function Calling vs. MCP** deployment paradigms using 3,250 attack scenarios across seven LLMs. Attacks include prompt injection, JSON injection, DoS, and function-name and function-parameter attacks. Function Calling had higher overall attack success (73.5% vs. 62.59% for MCP), while MCP showed more LLM-centric exposure. Chained attacks reached 91–96%. Advanced reasoning models were easier to exploit even though they detected threats better.
- **Limitations:** Not seen.
- **Relevance:** **High.** It is a Q1-journal empirical study of MCP's attack surface and a direct baseline for the claim that MCP needs a dedicated gateway.
- **Quartile:** Information Sciences is Q1 per general knowledge — verify.
- **Verification seen:** PUB (ScienceDirect listing title + PII), REF, ARX.

### 20. A survey on large language model (LLM) security and privacy: The Good, The Bad, and The Ugly
- **Authors:** Yifan Yao, Jinhao Duan, Kaidi Xu, Yuanfang Cai, Zhibo Sun, Yue Zhang (Drexel)
- **Journal:** High-Confidence Computing **4(2), Article 100211**, 2024 (online 1 Mar 2024)
- **DOI:** 10.1016/j.hcc.2024.100211. Link: https://journal.hep.com.cn/hcc/EN/1182986108045800119
- **Summary:** Groups the literature into beneficial uses, offensive uses, and vulnerabilities with defenses. Finds that LLMs help vulnerability detection while their reasoning also aids user-level attacks.
- **Stated gaps:** Little work on model and parameter extraction and on safe instruction tuning.
- **Relevance:** Low to medium; background. Highly cited.
- **Quartile:** High-Confidence Computing is a newer Elsevier/SDU journal. Its quartile is uncertain to me (possibly Q1 in recent SJR), so verify.
- **Verification seen:** PUB (journal.hep.com.cn), REPO (NSF PAR), ARX.

### 21. [IEEE Access 2026 SLR — title UNVERIFIED] Prompt injection across trust boundaries in LLM-integrated systems
- **Authors:** Woesle and Buettner (first names UNVERIFIED)
- **Journal:** IEEE Access, 2026, per a search summary. IEEE Xplore document **11551573** (https://ieeexplore.ieee.org/document/11551573). Exact title and DOI UNVERIFIED.
- **Summary (from snippets):** A systematic literature review of prompt injection in LLM-integrated systems that codes **81 papers** along three axes. Defines a "Tool/Connector Boundary" where attackers induce unintended tool, plugin or API calls, including tool-choice hijacking and parameter manipulation. Reports that **83.9% of papers target the prompt interface while tool boundaries have zero papers**.
- **Relevance:** **Very high as gap evidence.** If confirmed, it shows quantitatively that tool and connector boundaries are under-researched. **Confirm the title, authors and the figures before citing.**
- **Quartile:** IEEE Access is Q1 (some categories Q2) per general knowledge — verify.
- **Verification seen:** IEEE Xplore document URL and snippet text only. Title not seen. Treat as PARTIALLY VERIFIED.

---

## TIER Q2 / Q2–Q3

### 22. Model Context Protocol Threat Modeling and Analysis of Vulnerabilities to Prompt Injection with Tool Poisoning
- **Authors:** Charoes Huang, Xin Huang, Ngoc Phu Tran, Amin Milani Fard (New York Institute of Technology, Vancouver). Authors taken from arXiv 2603.22489; the MDPI author list was not seen directly but the title matches.
- **Journal:** Journal of Cybersecurity and Privacy (MDPI) **Vol. 6, Issue 3, Article 84**, published 5 May 2026.
- **DOI:** 10.3390/jcp6030084. Link: https://www.mdpi.com/2624-800X/6/3/84
- **Summary:** Applies STRIDE and DREAD to identify **57 threats across six MCP components**: host, client, LLM, server, external data stores, and authorization server. Empirically tests **seven MCP clients against four types of tool-poisoning attack**. Attack success ranged from 0% (Claude Desktop) to 100% (Cursor). Proposes layered defenses: static metadata analysis, model decision-path tracking, behavioral anomaly detection, and user transparency.
- **Stated gaps:** Prior MCP security work focused on server-side flaws, leaving **client-side** weaknesses under-studied.
- **Relevance:** **Very high and closest to the proposal.** It has the same attack class, layered defense recommendations and anomaly detection. It does not appear to implement or evaluate an integrity-pinning, drift-detection and policy gateway with P/R/F1 on a labeled dataset. That is the proposal's differentiator; verify by reading the full text.
- **Quartile:** JCP is a newer MDPI journal; quartile UNVERIFIED (possibly Q2), so verify.
- **Verification seen:** PUB (MDPI page via search, with vol/issue/article/date and DOI), ResearchGate listing, ARX.

### 23. Prompt Injection Attacks in Large Language Models and AI Agent Systems: A Comprehensive Review of Vulnerabilities, Attack Vectors, and Defense Mechanisms
- **Authors:** Saidakhror Gulyamov + 6 co-authors (full list UNVERIFIED)
- **Journal:** Information (MDPI) **17(1), Article 54**, Jan 2026
- **DOI:** 10.3390/info17010054. Preprint: Preprints.org 202511.0088.
- **Summary:** Reviews 2023–2025 research on direct jailbreaks and indirect injection. Covers **MCP-expanded attack surfaces including tool poisoning and credential theft**, CVE-2025-53773 (GitHub Copilot RCE, CVSS 9.6), and RAG poisoning (five crafted documents manipulate responses about 90% of the time). Bases mitigations on the OWASP LLM Top-10 2025 and argues for defense-in-depth.
- **Limitations:** Narrative review. The source count is inconsistent (120+ papers vs. 45 key sources), so check the final version.
- **Relevance:** Medium to high. It is a journal citation that explicitly names MCP tool poisoning.
- **Quartile:** Information (MDPI) is Q2 (some categories Q3) per general knowledge — verify.
- **Verification seen:** Mirror PDF (kiut.uz), preprint pages, REF. The MDPI page itself was not seen.

### 24. Enhancing security in LLM applications: a performance evaluation of early detection systems
- **Authors:** Valerii Gakh, Hayretdin Bahsi (TalTech; NAU). Authors taken from arXiv 2506.19109 with the same title.
- **Journal:** International Journal of Information Security (Springer), 2026
- **DOI:** 10.1007/s10207-026-01338-7. Link: https://link.springer.com/article/10.1007/s10207-026-01338-7
- **Summary:** Benchmarks open-source prompt-injection detectors (**LLM Guard, Vigil, Rebuff**) against prompt-leak attacks built from context-ignoring and context-manipulation techniques.
- **Relevance:** High for the **evaluation baseline**. Existing detectors are run as black boxes, and the proposal could compare its tool-metadata detector against LLM Guard or Vigil.
- **Quartile:** IJIS is Q2 (possibly Q1 in some categories) per general knowledge — verify.
- **Verification seen:** PUB (Springer page via search), ARX.

### 25. Comparative evaluation of machine learning methods for protecting LLMs from prompt injection attacks
- **Authors:** Dzhaliuk, Sabodashko, Khoma, et al. (first names UNVERIFIED)
- **Journal:** International Journal of Information Security **25, 109 (2026)**
- **DOI:** 10.1007/s10207-026-01264-8. Link: https://link.springer.com/article/10.1007/s10207-026-01264-8
- **Summary:** Compares classical ML methods for prompt-injection classification (details UNVERIFIED; only the title and citation were seen).
- **Relevance:** High for the **TF-IDF+LogReg / ML classifier baseline** in the proposal. Read the full text for its feature sets and results.
- **Quartile:** As for item 24, verify.
- **Verification seen:** PUB (Springer URL in results), with the citation string in the search summary.

### 26. Prompt Injection Attacks on Large Language Models: A Survey of Attack Methods, Root Causes, and Defense Strategies
- **Authors:** Tongcheng Geng, Zhiyuan Xu, Yubin Qu, W. Eric Wong
- **Journal:** Computers, Materials & Continua (Tech Science Press) **87(1):4, 2026**
- **DOI:** 10.32604/cmc.2025.074081. Link: https://www.sciopen.com/article/10.32604/cmc.2025.074081 (also on ScienceDirect/org)
- **Summary:** A Kitchenham-style SLR of 128 peer-reviewed studies (2022–2025). Traces a shift from direct to multimodal injection, with success rates above 90% on unprotected systems. Input preprocessing achieves 60–80% detection, and architectural defenses reach up to 95% on known patterns.
- **Stated gaps:** Significant gaps remain against **novel attack vectors**, which supports the proposal's RQ on unseen patterns.
- **Relevance:** Medium.
- **Quartile:** CMC is Q2/Q3 per general knowledge — verify. Treat it as a weaker venue.
- **Verification seen:** PUB (SciOpen; note its AI-generated summary disclaimer), ScienceDirect/org listing.

---

## Q3 / unknown / tangential (listed for completeness)

- **LLM-Based Agents for Tool Learning: A Survey.** Data Science and Engineering (Springer), 2025. DOI 10.1007/s41019-025-00296-9. Authors UNVERIFIED. Notes that unsafe queries can bypass checks via long text or tool-invocation requests. Relevance: low to medium. Quartile unknown, so verify.
- **From AI-Generated Content to Agentic Action: Security and Safety Threats in Generative AI.** Zelin Zhang, Qi Li, Jie Cao, Lingshuang Liu, Jianbing Ni (Queen's/Waterloo). The ScienceDirect PII S2949715926000405 was listed under *Journal of Information and Intelligence* (2026), but the journal name was confirmed only via a search summary (UNVERIFIED). arXiv 2605.16471. An analytical review rather than a systematic survey. Quartile unknown; it is a new journal.
- **Agentic AI Security: Threats, Defenses, Evaluation, and Open Challenges.** Shrestha Datta, Shahriar Kabir Nahin, Anshuman Chhabra, Prasant Mohapatra. A reference list cites it as *IEEE Access* 2026, but **no IEEE Access record was seen**, so the venue is UNVERIFIED. arXiv 2510.23883.

---

## Items checked and NOT journal (do not cite as journal)

| Work | Status seen |
|---|---|
| MCPTox (Wang et al.) | AAAI 2026 proceedings (vol. 40 no. 42, pp. 35811–35819 per a reference list) — conference |
| A Systematic Security Analysis of MCP (IEEE doc 11395848) | IEEE ICAIC 2026 conference (DOI 10.1109/ICAIC67076.2026.11395848); the "IEEE Access" header seen in results is misleading |
| Enterprise-Grade Security for MCP (Narajala & Habler) | IEEE Xplore 11395723 — conference (venue UNVERIFIED); arXiv 2504.08623 |
| MCPXKIT / "Systematic Analysis of MCP Security" (Guo et al.) | IEEE Xplore 11531012 (venue UNVERIFIED); arXiv 2508.12538 |
| MCP-Secure runtime access-control layer | IEEE Xplore 11394790 (venue UNVERIFIED, likely conference) |
| "We Urgently Need Privilege Management in MCP" | IEEE Xplore 11206219 (venue UNVERIFIED) |
| ETDI (Bhatt et al.) | IEEE CARS symposium per a reference list; arXiv 2506.01333 |
| Secure MCP with Dual Signatures | ACM DL 10.1145/3737897.3767287 — workshop/conference proceedings |
| MCP-SecLint | ACM DL 10.1145/3806007.3810961 — proceedings |
| Securing the MCP (Jamshidi et al.) | arXiv 2512.06556 only (ACM JACM template ≠ acceptance) |
| Invisible Threats from MCP (arXiv 2603.24203) | TDSC template header only — not confirmed accepted |
| Gaire et al. SoK MCP; Hasan et al. MCP servers; MindGuard; MCPSecBench; MCP-DPT; MCP-38; SMCP | arXiv preprints |
| A Survey on Trustworthy LLM Agents (Yu et al.) | KDD '25 conference |
| Exploring ChatGPT App Ecosystem (Yan et al.) | ASE 2024 conference |
| LLM Platform Security / ChatGPT plugins (Iqbal, Kohno, Roesner) | AAAI/ACM AIES 2024 conference |
| Prompt-to-SQL injections (Pedro et al.) | ICSE 2025 conference |
| DataSentinel | IEEE S&P 2025 conference |
| CaMeL "Defeating Prompt Injections by Design" | IEEE SaTML 2026 conference |
| A Survey on Autonomy-Induced Security Risks in Large Model-Based Agents (Su et al.) | IEEE Xplore 11498611; arXiv header says "submitted to TPAMI" — venue UNVERIFIED |
| Polymorphic Prompt Assembling (Wang et al.) | IEEE Xplore 11068353 — venue UNVERIFIED (likely conference) |
| MalPID dataset | IEEE ComNet 2024 conference |
| Fine-tuned LLMs prompt-injection detection (XLM-RoBERTa) | IEEE Xplore 11126597 — venue UNVERIFIED |
| Lifting the Veil on LLM Supply Chain; Unveiling LLM Supply Chain | arXiv only |
| Jailbreaking ChatGPT via Prompt Engineering (Liu et al.) | arXiv only in results |

---

## Searched with no confirmed hit (worth a manual database query)
- Computers & Security (Elsevier): no confirmed 2023–2026 article on prompt injection, jailbreaks or MCP found via web search. **Search ScienceDirect directly** with the journal filter.
- IEEE TIFS, TDSC, TSE, TNNLS, TKDE, TAI, COMST, IoT-J, and IEEE S&P magazine: no confirmed journal article on prompt injection or MCP in the snippets. Web search does not index these well, so use IEEE Xplore with a publication-title filter.
- ESWA, KBS, EAAI, FGCS, Computer Networks, Computer Science Review, JSS, IST, Array: none confirmed.
- ACM TOPS, TIST, CACM: none confirmed.
- Empirical Software Engineering, Automated Software Engineering: none confirmed on LLM tool or plugin security.
- MDPI Future Internet, Electronics, Applied Sciences: none confirmed on MCP.

## Implications for the proposal
- **Novelty claim:** There is little journal work on MCP tool poisoning. The confirmed papers are Hou (TOSEM, a taxonomy), Huang (JCP, threat modeling plus client tests), Ferrag (ICT Express, a taxonomy) and Gasmi (Information Sciences, an FC-vs-MCP attack comparison). **None evaluates a multi-layer gateway with integrity pinning, semantic drift and policy against a labeled SAFE/POISONED corpus.** This matches what was visible in the snippets; confirm it in the full texts.
- **Baselines to cite and compare:** JailGuard (TOSEM) for a divergence-based detector; LLM Guard, Vigil and Rebuff (IJIS 2026) for off-the-shelf detectors; the ML-classifier comparison (IJIS 2026, 25:109) for the TF-IDF/LR baseline.
- **Supply-chain framing:** Williams et al. (TOSEM 2025), Wang et al. (TOSEM, LLM supply chain) and Zhao et al. (TOSEM, LLM app stores).
- **Gap evidence:** The IEEE Access SLR reports that 83.9% of papers target the prompt interface and none the tool boundary. Confirm the title and figures before citing. CMC 2026 reports that defenses fail on novel vectors.
