# Step 2 / J2: Venue quartiles and ranks, closest text-detection analogues, and lead verification

Date: 2026-10-07. Searches used: about 80 WebSearch calls. WebFetch to scimagojr.com, resurchify.com and portal.core.edu.au is **blocked by the egress proxy**. Every value below therefore comes from **WebSearch result snippets of those sites** (mainly `allowed_domains` searches on scimagojr.com and portal.core.edu.au). I did not view any page directly.

Legend for "verified?":
- **Y**: the value appeared in a scimagojr.com or portal.core.edu.au snippet for that exact title.
- **P** (partial): seen only on a third-party aggregator, or the snippet was ambiguous.
- **N**: not found. The value given is general knowledge or is left blank.

Important context on CORE: the CORE portal now publishes **ICORE2026** as the current edition, and most snippets returned that edition. Where a snippet also showed CORE2023, I give both.

---

## 1. Quartile and rank table

### 1a. Journals named in step2_*.md files

The venues were found by grepping step2_P1 to P5. SJR values are the **2025 SJR** (the latest year visible on SCImago), unless noted otherwise.

| Venue | Type | Best SJR quartile (SJR value) | Ranking year | Evidence (snippet source) | Verified? |
|---|---|---|---|---|---|
| Computers & Security (Elsevier) | Journal | Q1 (SJR 1.598; H-index 148) | SJR 2025 | https://www.scimagojr.com/journalsearch.php?q=28898&tip=sid&clean=0 (also: SJR 2024 = 1.445). JCR: an aggregator (journalmetrics.org) shows a 2024 JIF of 5.4 and JCR Q1; Peeref showed JCR 2023 Q2 (CS, Information Systems). | Y (SJR); P (JCR) |
| Expert Systems with Applications (ESWA) | Journal | Q1 (1.939; H 315) | 2025 | https://www.scimagojr.com/journalsearch.php?q=24201&tip=sid&clean=0 | Y |
| Knowledge-Based Systems (KBS) | Journal | Q1 (1.753); Q1 in Artificial Intelligence 2011–2025 | 2025 | https://www.scimagojr.com/journalsearch.php?tip=sid&q=24772 | Y |
| IEEE Access | Journal (mega-journal, open access) | Q1 (0.884; H 338); Q1 in CS (misc.) for 2025 | 2025 | https://www.scimagojr.com/journalsearch.php?q=21100374601&tip=sid | Y |
| Journal of Information Security and Applications (JISA) | Journal | Q1 (0.905; H 80) | 2025 | https://www.scimagojr.com/journalsearch.php?q=21100332403&tip=sid | Y (SJR value and Q1 seen; category breakdown not seen) |
| IEEE Trans. Information Forensics & Security (TIFS) | Journal | Q1 (2.193; H 195) | 2025 | https://www.scimagojr.com/journalsearch.php?q=4000149002&tip=sid&clean=0 | Y |
| IEEE Trans. Dependable & Secure Computing (TDSC) | Journal | Q1 (1.758; H 117) | 2025 | https://www.scimagojr.com/journalsearch.php?q=28918&tip=sid&clean=0 | Y |
| ACM Trans. Software Engineering & Methodology (TOSEM) | Journal | Q1 (1.590; H 95) | 2025 | https://www.scimagojr.com/journalsearch.php?q=18121&tip=sid&clean=0 | Y |
| IEEE Trans. Software Engineering (TSE) | Journal | Q1 (1.568), Software | 2025 | https://www.scimagojr.com/journalsearch.php?q=18711&tip=sid | Y |
| ACM Computing Surveys (CSUR) | Journal | Q1 (5.985; H 260) | 2025 | https://www.scimagojr.com/journalsearch.php?q=23038&tip=sid | Y |
| Information Fusion | Journal | Q1 (4.197) | 2025 | https://www.scimagojr.com/journalsearch.php?q=26099&tip=sid | Y |
| Applied Soft Computing | Journal | Q1 (1.456) | 2025 | https://www.scimagojr.com/journalsearch.php?q=18136&tip=sid&clean=0 | Y |
| ICT Express (Elsevier/KICS) | Journal | Q1 (0.977) | 2025 | https://www.scimagojr.com/journalsearch.php?q=21100836194&tip=sid&clean=0 | Y |
| Int. J. Network Dynamics and Intelligence (IJNDI, Scilight) | Journal (young, launched 2022) | Q1 (SJR 3.327; H 24) | 2025 | scimagojr.com category ranking tables (CS Networks & Comms, AI) plus https://scijournal.org/international-journal-of-network-dynamics-and-intelligence ; publisher says it is Scopus-indexed: https://www.sciltp.com/journals/ijndi/indexing | P. The SJR is unusually high for a 3-year-old journal. Check the SCImago page before relying on it. |
| Computers, Materials & Continua (CMC, Tech Science Press) | Journal | Q2 (0.513) overall; Q3 in Biomaterials | 2025 | https://www.scimagojr.com/journalsearch.php?tip=sid&q=24364 | Y |
| IEEE Software | Magazine/journal | **Q2** (0.627); Q1 only in 2019–2021 | 2025 | https://www.scimagojr.com/journalsearch.php?q=18709&tip=sid | Y |
| IEEE Security & Privacy (magazine) | Magazine | Q1 (0.643; H 95) | 2025 | https://www.scimagojr.com/journalsearch.php?q=28916&tip=sid | Y |
| Communications of the ACM | Magazine/journal | Q1 (1.540; H 259) | 2025 | https://www.scimagojr.com/journalsearch.php?q=13675&tip=sid | Y |
| ACM Trans. Privacy & Security (TOPS, formerly TISSEC) | Journal | Q1 (0.783) | 2025 | https://www.scimagojr.com/journalsearch.php?q=21100832567&tip=sid | Y |
| ACM Trans. Intelligent Systems & Technology (TIST) | Journal | Q1 (2.065) | 2025 | https://www.scimagojr.com/journalsearch.php?q=19700190323&tip=sid | Y |
| ACM Trans. Knowledge Discovery from Data (TKDD) | Journal | Q1 (1.317; H 83) | 2025 | https://www.scimagojr.com/journalsearch.php?q=5800173377&tip=sid&clean=0 | Y |
| Cybersecurity (SpringerOpen) | Journal | Q1 (1.056) | 2025 | https://www.scimagojr.com/journalsearch.php?q=21101019779&tip=sid&clean=0 | Y |
| Journal of Network and Computer Applications (JNCA) | Journal | Q1 (1.704; H 167) | 2025 | https://www.scimagojr.com/journalsearch.php?q=27277&tip=sid | Y |
| Neurocomputing | Journal | Q1 (1.465; H 233) | 2025 | https://www.scimagojr.com/journalsearch.php?q=24807&tip=sid | Y |
| Computer Networks (Elsevier) | Journal | Q1 (1.144; H 177) | 2025 | https://www.scimagojr.com/journalsearch.php?q=26811&tip=sid | Y |
| Future Internet (MDPI) | Journal | Q2 (0.762) in the 2024 profile; one undated export showed Q1 (0.845) | 2024 (Q2); later year unclear | https://www.scimagojr.com/journalsearch.php?q=21100409311&tip=sid&clean=0 | P |
| Electronics (MDPI, ISSN 2079-9292) | Journal | Q2 (0.623); Q2 in CS Networks 2020–2025 | 2025 | https://www.scimagojr.com/journalsearch.php?q=21100829272&tip=sid | Y |
| Applied Sciences (MDPI) / Information (MDPI) | Journal | not retrieved | – | – | N (general knowledge: usually Q2; verify) |

JCR impact factors: apart from Computers & Security (JIF 5.4, aggregator only), I did not retrieve JCR figures, to save search budget. All other JCR values are **UNVERIFIED**.

### 1b. Conferences: CORE / ICORE rank

| Venue | Type | Rank | Edition | Evidence | Verified? |
|---|---|---|---|---|---|
| IEEE S&P (Oakland) | Conference | A* | ICORE2026 (also A* in CORE2017/2018/2020) | https://portal.core.edu.au/conf-ranks/750/ | Y |
| USENIX Security | Conference | A* | ICORE2026 | https://portal.core.edu.au/conf-ranks/1841/ | Y |
| ACM CCS | Conference | A* | CORE2023 | https://portal.core.edu.au/conf-ranks/12/ | Y |
| NDSS | Conference | A* | CORE2023 and ICORE2026 | https://portal.core.edu.au/conf-ranks/1840/ | Y |
| IEEE EuroS&P | Conference | A | ICORE2026 | https://portal.core.edu.au/conf-ranks/2185/ | Y |
| AsiaCCS | Conference | A | ICORE2026 | https://portal.core.edu.au/conf-ranks/61/ | Y |
| ACSAC | Conference | A | ICORE2026 (a CORE2021 row showed "National: USA") | https://portal.core.edu.au/conf-ranks/117/ | Y |
| RAID | Conference | A | ICORE2026, and also A in CORE2023 | https://portal.core.edu.au/conf-ranks/1408/ | Y |
| ESORICS | Conference | A | ICORE2026 (a request to move to A* was declined) | https://portal.core.edu.au/conf-ranks/515/ | Y |
| DIMVA | Conference | B | ICORE2026 | https://portal.core.edu.au/conf-ranks/565/ | Y |
| ICSE | Conference | A* | ICORE2026 | https://portal.core.edu.au/conf-ranks/1209/ | Y |
| FSE (formerly ESEC/FSE) | Conference | A* | ICORE2026 | https://portal.core.edu.au/conf-ranks/52/ | Y |
| ASE | Conference | A* | ICORE2026 | https://portal.core.edu.au/conf-ranks/279/ | Y |
| ISSTA | Conference | A | ICORE2026 | https://portal.core.edu.au/conf-ranks/1412/ | Y |
| MSR | Conference | A | ICORE2026 (A since CORE2018) | https://portal.core.edu.au/conf-ranks/711/ | Y |
| ICML | Conference | A* | ICORE2026 | https://portal.core.edu.au/conf-ranks/1121/ | Y |
| NeurIPS | Conference | A* | ICORE2026 | https://portal.core.edu.au/conf-ranks/98/ | Y |
| ICLR | Conference | A* | ICORE2026, and also A* in CORE2023 | https://portal.core.edu.au/conf-ranks/2273/ | Y |
| ACL | Conference | A* | ICORE2026 | https://portal.core.edu.au/conf-ranks/196/ | Y |
| EMNLP | Conference | A* | ICORE2026 (an older, undated snapshot showed A) | https://portal.core.edu.au/conf-ranks/448/ | Y |
| NAACL | Conference | A | ICORE2026 | https://portal.core.edu.au/conf-ranks/1648/ | Y |
| AAAI | Conference | A* | ICORE2026 | https://portal.core.edu.au/conf-ranks/1629/ | Y |
| IJCAI | Conference | A* | ICORE2026 (also A* in 2023) | https://portal.core.edu.au/conf-ranks/1313/ | Y |
| WWW (The Web Conference) | Conference | A* | ICORE2026 (also A* in 2023) | https://portal.core.edu.au/conf-ranks/1548/ | Y |
| KDD | Conference | A* | ICORE2026 | https://portal.core.edu.au/conf-ranks/26/ | Y |
| AIES (AAAI/ACM AI, Ethics & Society) | Conference | **C** | ICORE2026 | https://portal.core.edu.au/conf-ranks/2354/ | Y |
| HotOS | Workshop | A | ICORE2026 | https://portal.core.edu.au/conf-ranks/1845/ | Y |
| ACM SAC | Multiconference | Unranked ("Multiconference" tag since Dec 2022; one ICORE2026 row still shows B, which is inconsistent) | ICORE2026 | https://portal.core.edu.au/conf-ranks/59/ | P |
| COMPSAC | Conference | B | ICORE2026 | CORE portal snippet (ICORE2026 listing) | Y |
| AISec (ACM Workshop on AI and Security, co-located with CCS) | Workshop | Not found in CORE | – | search on portal returned no entry | N (probably unranked) |
| CAMLIS | Conference/workshop | Not searched or found | – | – | N (probably unranked) |
| SCORED (ACM Workshop on Software Supply Chain Offensive Research & Ecosystem Defenses, co-located with CCS) | Workshop | Not found | – | – | N (probably unranked) |

Takeaways for venue choice:
- **AIES is CORE C.** Citing Iqbal et al. (AIES 2024) is fine, but it is not top-tier.
- **DIMVA is B.**
- **IEEE Software dropped to Q2 in SJR.**
- All the major security and SE journals the proposal could target are SJR Q1 in 2025: Computers & Security, TIFS, TDSC, TOPS, JISA, IEEE Access, ESWA, KBS, TOSEM and TSE.

---

## 2. Closest text analogues in Q1/Q2 journals (2020–2026)

Scope: detection of malicious or deceptive natural-language content, covering phishing and social-engineering text, malicious URLs, and semantic or embedding-based anomaly detection.

**Gap:** focused searches (sciencedirect.com, `"prompt injection"` with C&S/ESWA) found **no Q1/Q2 journal article on prompt-injection detection**. The only ScienceDirect hit was "Malicious Prompt Classifier with Leave-One-Out Deletion Approach for Prompt Sanitization", PII S1877050926016996, which is **Procedia Computer Science, a conference-proceedings series and not a Q1/Q2 journal** (venue inferred from the ISSN prefix 1877-0509; verify). This supports the novelty argument for a journal submission.

### J2-01. Devising and Detecting Phishing Emails Using Large Language Models
- Authors: Fredrik Heiding, Bruce Schneier, Arun Vishwanath, Jeremy Bernstein, Peter S. Park
- Journal: IEEE Access, vol. 12, pp. 42131–42146, 2024. DOI **10.1109/ACCESS.2024.3375882**
- Summary: Compares GPT-4-generated phishing emails, manually built V-Triad emails and a combination of both, in a study with 112 participants. Click-through was about 30–44% for GPT emails versus 69–79% for V-Triad emails. The authors also test GPT, Claude, PaLM and LLaMA as detectors of malicious intent; the models were strong, sometimes better than humans.
- Why it is an analogue: an LLM is used as a classifier of malicious intent in natural-language text. This is a direct baseline idea for an "LLM-as-judge" poisoning detector.
- Quartile: IEEE Access, SJR 2025 Q1.
- Verification: DOAJ record https://doaj.org/article/ac3d9ad383bb4e2092a20459752e356a ; IEEE Xplore document 10466545; Schneier archive page.

### J2-02. Evaluating Large Language Models' Ability to Automate Spear Phishing
- Authors: F. Heiding, S. Lermen, A. Kao or Koo (sources disagree), C. M. Verdun, B. Schneier, A. Vishwanath
- Journal: Expert Systems with Applications, vol. 314, article 131546, 2026. Online 6 Feb 2026 according to one snippet. DOI **UNVERIFIED**.
- Summary: Compares AI-generated spear phishing with human-expert spear phishing, and evaluates LLM-based detection. The snippet reported high detection accuracy with no false positives, and better performance when models are "primed for suspicion".
- Why it is an analogue: Q1 journal evidence on LLM-based detection of deceptive instructions or persuasion. The "primed for suspicion" finding is relevant to how a detector prompt should be framed.
- Quartile: ESWA, Q1.
- Verification: https://www.schneier.com/academic/archives/2026/06/evaluating-large-language-models-ability-to-automate-spear-phishing.html ; PDF on schneier.com. Check the author spelling and DOI on ScienceDirect.

### J2-03. An explainable transformer-based model for phishing email detection: A large language model approach
- Authors: Mohammad Amaz Uddin, Md Mahiuddin, Iqbal H. Sarker
- Journal: Computer Networks, vol. 277, article 112061, 2026. DOI **10.1016/j.comnet.2026.112061** (seen in an ECU repository record)
- Summary: Fine-tunes RoBERTa for phishing email classification and reports 98.45% test accuracy on a balanced dataset. It adds LITA, a hybrid explanation method combining LIME and Transformers Interpret. The earlier arXiv version (2402.13871) used DistilBERT.
- Why it is an analogue: a fine-tuned transformer classifier for malicious text plus token-level explanations. This maps directly to the "ML classifier" layer and to explaining REVIEW/BLOCK decisions.
- Quartile: Computer Networks, SJR 2025 Q1.
- Verification: ScienceDirect PII S1389128626000733 and https://ro.ecu.edu.au/ecuworks2022-2026/7557

### J2-04. A Systematic Literature Review on Phishing Email Detection Using Natural Language Processing Techniques
- Authors: Said Salloum, Tarek Gaber, Sunil Vadera, Khaled Shaalan
- Journal: IEEE Access, vol. 10, pp. 65703–65727, 2022. DOI **10.1109/ACCESS.2022.3183083**
- Summary: A systematic review of 100 papers from 2006–2022. It finds that TF-IDF and word embeddings are the most common NLP features, SVM is the most common classifier, and the Nazario corpus is the most common dataset.
- Why it is an analogue: a journal citation that justifies the **TF-IDF + linear classifier baseline** as the standard starting point in malicious-text detection.
- Quartile: IEEE Access, Q1.
- Verification: https://salford-repository.worktribe.com/output/1562809/ ; BUiD repository record.

### J2-05. Deep Learning for Phishing Detection: Taxonomy, Current Challenges and Future Directions
- Authors: Nguyet Quang Do, Ali Selamat, Ondrej Krejcar, Enrique Herrera-Viedma, Hamido Fujita
- Journal: IEEE Access, vol. 10, pp. 36429–36463, 2022. DOI **10.1109/ACCESS.2022.3151903**
- Summary: A systematic review of 81 papers with a taxonomy of deep-learning phishing detectors, plus an empirical experiment. The common weaknesses it identifies are manual hyper-parameter tuning, long training time and poor detection of unknown attacks.
- Why it is an analogue: its point about weak generalization to unseen attacks supports the proposal's RQ on unseen-pattern generalization.
- Quartile: IEEE Access, Q1.
- Verification: https://digibug.ugr.es/handle/10481/74654 ; DOAJ.

### J2-06. Utilizing Convolutional Neural Networks and Word Embeddings for Early-Stage Recognition of Persuasion in Chat-Based Social Engineering Attacks
- Authors: Nikolaos Tsinganos, Ioannis Mavridis, Dimitris Gritzalis
- Journal: IEEE Access, vol. 10, pp. 108517–108529, 2022. DOI **10.1109/ACCESS.2022.3213681**
- Summary: A CNN plus word-embedding classifier that detects persuasion cues in chat messages as early signs of social-engineering attacks.
- Why it is an analogue: detects *manipulative instructions* in free text. This is the human-targeted counterpart of LLM-targeted tool-description poisoning, where persuasion or urgency cues work like "IMPORTANT: before using this tool…".
- Quartile: IEEE Access, Q1.
- Verification: DOAJ record (IEEE Access, Jan 2022); University of Macedonia repository https://ruomo.lib.uom.gr/handle/7000/1708

### J2-07. Leveraging Dialogue State Tracking for Zero-Shot Chat-Based Social Engineering Attack Recognition
- Authors: Nikolaos Tsinganos, Panagiotis Fouliras, Ioannis Mavridis
- Journal: Applied Sciences (MDPI), vol. 13, no. 8, art. 5110, 2023. DOI **10.3390/app13085110**
- Summary: Zero-shot recognition of social-engineering attacks by tracking dialogue state, so that attacker intents not seen in training can be flagged. The same group published an annotated CSE corpus in Applied Sciences 11(22):10871 (2021).
- Why it is an analogue: zero-shot detection of malicious intent in text matches the proposal's unseen-pattern generalization question. The corpus paper is a model for building and annotating a SAFE/POISONED dataset.
- Quartile: Applied Sciences, **UNVERIFIED** (general knowledge says Q2; verify).
- Verification: DOAJ record (Applied Sciences, Apr 2023).

### J2-08. GramBeddings: A New Neural Network for URL Based Identification of Phishing Web Pages Through N-gram Embeddings
- Authors: Ahmet Selman Bozkir, Firat Coskun Dalgic, Murat Aydos
- Journal: Computers & Security, vol. 124, art. 102964, 2023. DOI **UNVERIFIED** (not shown in the snippets)
- Summary: Learns character n-gram embeddings of URLs for phishing-page detection, with no hand-crafted features.
- Why it is an analogue: an embedding-based detector for short, adversarial strings. Tool names and short descriptions have similar length and an obfuscation-prone character.
- Quartile: Computers & Security, Q1.
- Verification: the DBLP author listing for Bozkir, seen in search results.

### J2-09. LAnoBERT: System log anomaly detection based on BERT masked language model
- Authors: Yukyung Lee, Jina Kim, Pilsung Kang
- Journal: Applied Soft Computing, vol. 146, art. 110689, Oct 2023. Journal DOI **UNVERIFIED**; arXiv 2111.09564.
- Summary: Parser-free, unsupervised anomaly detection. A BERT model is trained by masked language modelling on normal logs, and the per-log-key MLM loss is used as the anomaly score. Evaluated on HDFS, BGL and Thunderbird.
- Why it is an analogue: **unsupervised, embedding/LM-based anomaly scoring trained only on "normal" text**. This is the same principle as scoring a received tool description against a trusted baseline (semantic drift, RQ2), and it is an alternative to Isolation Forest for text.
- Quartile: Applied Soft Computing, Q1.
- Verification: ScienceDirect listing snippet (S156849462300707X) with volume, article and date; Korea University repository record.

### J2-10. Semi-supervised log anomaly detection based on bidirectional temporal convolution network
- Authors: **UNVERIFIED**
- Journal: Computers & Security, vol. 140, art. 103808, May 2024 (ScienceDirect PII S0167404824001093)
- Summary: BERT encodes each log template into a semantic vector. Clustering estimates labels when labelled data is scarce, and a bidirectional TCN performs detection.
- Why it is an analogue: BERT semantic vectors plus pseudo-labelling under label scarcity. The proposal faces the same small-labelled-dataset problem.
- Quartile: Computers & Security, Q1.
- Verification: ScienceDirect snippet only. A second search could not confirm the authors.

### J2-11 (secondary). An improved transformer-based model for detecting phishing, spam and ham emails: a large language model approach
- Authors: Suhaima Jamal, Hayden Wimmer, Iqbal H. Sarker
- Journal: Security and Privacy (Wiley), vol. 7, no. 5, e402, 2024. DOI **UNVERIFIED**
- Summary: Fine-tunes BERT-family models into the "IPSDM" detector for phishing and spam.
- Why it is an analogue: a multi-class transformer text classifier for malicious messages.
- Quartile: **UNVERIFIED**.
- Verification: seen only in a reference list and in the arXiv record 2311.04913.

### Leads not verified enough to cite
- TCURL (Knowledge-Based Systems 258:109955, 2022): appeared in one reference list; a direct search failed. **UNVERIFIED**.
- TransURL (Computer Networks, 2024; arXiv 2312.00508): the venue appeared in one search summary only. **UNVERIFIED**.
- Yu et al., BERT malicious-URL detection (IEEE Access, 2024): seen only as a secondary citation. **UNVERIFIED**.

---

## 3. Verification of specific leads

| # | Lead | Verified venue / year | DOI or ID | Status and source |
|---|---|---|---|---|
| 1 | Iqbal, Kohno, Roesner, "LLM Platform Security: Applying a Systematic Evaluation Framework to OpenAI's ChatGPT Plugins" | AIES 2024: Proc. AAAI/ACM Conf. AI, Ethics & Society 7(1):611–623, published 2024-10-16. **AIES is CORE C.** | **10.1609/aies.v7i1.31664**; arXiv 2309.10254 | Verified: https://ojs.aaai.org/index.php/AIES/article/view/31664 |
| 2a | LLM app store security: Hou, Zhao, Wang, "On the (In)Security of LLM App Stores" | **No venue found.** arXiv 2407.08422 only. It covers 786,036 apps from 6 stores, 15,146 with misleading descriptions and 616 usable for malware or phishing. **The guess of IEEE S&P 2025 is UNVERIFIED.** | arXiv 2407.08422 | arXiv only |
| 2b | GPTracker: Shen, Shen, Backes, Zhang, "GPTracker: A Large-Scale Measurement of Misused GPTs" | **IEEE S&P 2025**, San Francisco (conference date 2025-05-12) | **10.1109/SP61157.2025.00118** (from a Saarland repository record; IEEE Xplore not opened) | Verified (DOI via repository): https://cispa.de/en/research/publications/84716-gptracker-a-large-scale-measurement-of-misused-gpts ; https://publikationen.sulb.uni-saarland.de/handle/20.500.11880/41313 . Relevant finding: builders evaded review by "hiding intention in descriptions". This is a peer-reviewed A* precedent for metadata-level deception. |
| 2c | Other GPT Store measurement studies: Su et al., "GPT Store Mining and Analysis" (arXiv 2405.10210); Zhang et al., "A First Look at GPT Apps: Landscape and Vulnerability" (arXiv 2402.15105) | No venue seen for either | arXiv IDs | arXiv only; venues **UNVERIFIED** |
| 3 | Zhao, Hou, Wang, Wang, "LLM App Store Analysis: A Vision and Roadmap" | **Not TOSEM, as far as I found.** One arXiv version's header names the "International Workshop on Software Engineering in 2030" (Nov 2024, Porto de Galinhas, Brazil, co-located with FSE 2024). That is a workshop venue. **No evidence of TOSEM publication was found.** | arXiv 2404.12737 | Partial; the TOSEM DOI is UNVERIFIED |
| 4 | Kapravelos, Grier, Chachra, Kruegel, Vigna, Paxson, "Hulk: Eliciting Malicious Behavior in Browser Extensions" | **USENIX Security 2014** (23rd symposium, San Diego). It analysed 48K Chrome extensions and found 130 malicious and 4,712 suspicious. | No DOI (USENIX does not assign DOIs); the page range was not seen | Verified: https://usenix.org/conference/usenixsecurity14/technical-sessions/presentation/kapravelos |
| 5 | Lin, Koishybayev, Dunlap, Enck, Kapravelos, "UntrustIDE: Exploiting Weaknesses in VS Code Extensions" | **NDSS 2024**, Distinguished Paper Award. 25,402 extensions analysed with CodeQL taint rules; 21 extensions had verified PoC code injection, affecting more than 6M installs. | No DOI seen (NDSS papers usually cite the NDSS URL) | Verified: https://www.ndss-symposium.org/ndss-paper/untrustide-exploiting-weaknesses-in-vs-code-extensions |
| 6 | Ladisa, Plate, Martinez, Barais, "SoK: Taxonomy of Attacks on Open-Source Software Supply Chains" | **IEEE S&P 2023**, pp. 1509–1526 according to citing papers. The paper has 107 attack vectors, 94 incidents and 33 safeguards. | **10.1109/SP46215.2023.10179304**: seen only as cited in other papers (arXiv 2405.14993, 2603.16694); IEEE Xplore not opened | **Partially verified**. Note: one Chinese blog says "S&P'22", which is wrong (that was the arXiv year). Do not confuse it with Ladisa et al., "Journey to the Center of Software Supply Chain Attacks", IEEE Security & Privacy magazine 2023, DOI 10.1109/MSEC.2023.3302066. |
| 7 | Inan et al. (Meta), "Llama Guard: LLM-based Input-Output Safeguard for Human-AI Conversations" | **arXiv preprint / industry report only** (Dec 7, 2023). No peer-reviewed venue was found. | arXiv 2312.06674 | Verified as a preprint: https://ai.meta.com/research/publications/llama-guard-llm-based-input-output-safeguard-for-human-ai-conversations/ |
| 8 | Yi, Xie, Zhu, Kiciman, Sun, Xie, Wu, "Benchmarking and Defending Against Indirect Prompt Injection Attacks on Large Language Models" (BIPIA) | **KDD 2025** (31st ACM SIGKDD, V.1, Toronto, Aug 3–7, 2025) | **10.1145/3690624.3709179**; arXiv 2312.14197 | Verified via the ACM reference format in the arXiv v4 HTML |
| 9 | Ruan, Dong, et al., "Identifying the Risks of LM Agents with an LM-Emulated Sandbox" (ToolEmu) | **ICLR 2024** (Spotlight). An earlier version was a NeurIPS 2023 workshop poster. 36 toolkits, 144 test cases; 68.8% of flagged failures were judged valid. | arXiv 2309.15817 (ICLR has no DOI) | Verified: https://iclr.cc/virtual/2024/poster/19037 |
| 10 | Andriushchenko et al., "AgentHarm: A Benchmark for Measuring Harmfulness of LLM Agents" | **ICLR 2025**. 110 malicious tasks (440 with augmentation), 11 harm categories. | arXiv 2410.09024 | Verified: https://proceedings.iclr.cc/paper_files/paper/2025/hash/c493d23af93118975cdbc32cbe7323f5-Abstract-Conference.html |
| 11 | Liao, Mo, ..., Li, Sun, "EIA: Environmental Injection Attack on Generalist Web Agents for Privacy Leakage" | **ICLR 2025**. Up to 70% attack success rate for stealing specific PII. | arXiv 2409.11295 | Verified: https://proceedings.iclr.cc/paper_files/paper/2025/hash/a73474c359ed523e6cd3174ed29a4d56-Abstract-Conference.html |
| 12 | Chen, Xiang, Xiao, Song, Li, "AgentPoison: Red-teaming LLM Agents via Poisoning Memory or Knowledge Bases" | **NeurIPS 2024** (poster, Dec 13, 2024). Over 80% average attack success rate with a poison rate below 0.1%. | arXiv 2407.12784 | Verified: https://neurips.cc/virtual/2024/poster/94715 |
| 13 | Deng, Guo, Han, Ma, Xiong, Wen, Xiang, "AI Agents Under Threat: A Survey of Key Security Challenges and Future Pathways" | **ACM Computing Surveys 57(7), Article 182, July 2025** (Q1) | **10.1145/3716628** | Verified via the arXiv journal-ref and related DOI (ACM DL not opened) |
| 14 | Pasquini, Strohmeier, Troncoso, "Neural Exec: Learning (and Learning from) Execution Triggers for Prompt Injection Attacks" | **AISec 2024** (17th ACM Workshop on AI & Security, co-located with CCS 2024), pp. 89–100, according to DBLP as shown in a search summary. **Workshop.** | ACM DOI **UNVERIFIED**; arXiv 2403.03792 | Venue partially verified (DBLP via search summary) |
| 15 | MCPLib: Guo, Liu, Ma, Deng, Zhu, Di, Xiao, Wen, "Systematic Analysis of MCP Security" (v1). It introduces MCPLib, 31 attack methods in 4 classes (direct tool injection, indirect tool injection, malicious user, LLM-inherent). | **arXiv only.** The same ID 2508.12538 now carries the title "MCPXKIT: The Unified Toolkit for Analyzing Model Context Protocol Security". | arXiv 2508.12538 | Preprint; no venue. Its finding that agents rely blindly on tool descriptions is directly relevant. |
| 16 | Hou, Zhao, Wang, Wang, "Model Context Protocol (MCP): Landscape, Security Threats, and Future Research Directions" | Listed in the **FSE 2026 journal-first** track, which implies TOSEM, but no TOSEM volume or DOI was seen. The PDF shows a placeholder DOI 10.1145/nnnnnnn.nnnnnnn. | arXiv 2503.23278 (v3, Oct 7, 2025); TOSEM DOI **UNVERIFIED** | Partial: https://conf.researchr.org/details/fse-2026/fse-2026-journal-first/37/Model-Context-Protocol-MCP-Landscape-Security-Threats-and-Future-Research-Direct |


---

## 4. Notes for the proposal
- Every Q1 journal target was confirmed in SJR 2025 data: Computers & Security, TIFS, TDSC, TOPS, JISA, IEEE Access, ESWA, KBS, Information Fusion, Applied Soft Computing, Computer Networks, CSUR, TOSEM and TSE.
- No Q1/Q2 journal paper on prompt-injection or tool-description-poisoning *detection* was found. The nearest journal analogues are in phishing and social-engineering text detection (J2-01 to J2-08) and BERT-based anomaly detection (J2-09, J2-10).
- For the related-work hierarchy: GPTracker (S&P 2025, A*) and Iqbal et al. (AIES 2024, CORE C) are the peer-reviewed precedents on deceptive metadata or descriptions in LLM app ecosystems. Llama Guard and MCPLib are preprints. Neural Exec is a workshop paper.
