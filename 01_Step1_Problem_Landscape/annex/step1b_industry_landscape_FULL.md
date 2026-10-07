# Step 1b — Industry landscape of MCP tool poisoning (2025 – Oct 2026)

Compiled 2026-10-07. Scope: industry and government material, not academic papers.

## How this was gathered, and its limits

- **Evidence levels used below:**
  - **[F]**: I fetched the page myself and read it.
  - **[S]**: I saw the claim only in a web-search result summary, not on the primary page.
  - **[S-2nd]**: the search summary attributes the claim to a secondary source, such as a news or vendor blog, not the primary disclosure.
- **Many fetches were blocked.** The egress proxy blocked fetches from these domains: invariantlabs.ai, modelcontextprotocol.io, owasp.org, osv.dev, nvd.nist.gov (API), labs.cloudsecurityalliance.org, blog.checkpoint.com, blogs.cisco.com, enkryptai.com, stacklok.com, blogs.windows.com, code.visualstudio.com, appsecsanta.com, ox.security and mcp.directory.
- **Fetches that worked:** github.com, pypi.org, docker.com and code.claude.com.
- **Search budget ran out.** The shared web-search budget (200 calls per turn) was used up partway through section D. As a result:
  - VS Code and Cursor client-side behaviour could not be confirmed.
  - The Pillar, Prompt Security and Lakera product pages could not be checked.
- **Verify before citing.** Any **[S]** or **[S-2nd]** item should be checked against the primary URL before it goes into the paper. The URLs given are the ones the search engine returned.
- **Source types.** Every item in this file is an industry report, vendor blog, advisory, news article, government document or standards-body document. None of it is peer-reviewed.

---

## A. Incidents and disclosures (timeline)

| # | Date | What | Disclosed by | Attack class | Impact / key facts | URL(s) | Evidence |
|---|---|---|---|---|---|---|---|
| 1 | 2025-03-29 (UNVERIFIED date; per secondary source) | Equixly blog "MCP server: new security nightmare": scan of popular MCP servers | Equixly | Implementation bugs (cmd injection, path traversal, SSRF) | 43% command injection, 22% path traversal, 30% SSRF; 45% of notified vendors dismissed the risk (all figures come from a secondary source; primary not seen) | equixly.com/blog/2025/03/29/mcp-server-new-security-nightmare (URL as cited in search; not opened) | [S-2nd] |
| 2 | 2025-04-01 | **Tool Poisoning Attacks** disclosure (hidden instructions in the `add` tool description; exfiltrate `~/.cursor/mcp.json` and SSH key via a "sidenote" parameter). Also covers **rug pull** and **tool shadowing**. Cursor was found vulnerable to all four tested vectors. | Invariant Labs | Tool poisoning / rug pull / shadowing | First public PoC; the reference definition | https://invariantlabs.ai/blog/mcp-security-notification | [S] |
| 3 | 2025-04 (launch) | MCP-Scan released. Includes tool pinning by hashing, to catch rug pulls. | Invariant Labs | Defense | See section D | https://invariantlabs.ai/blog/introducing-mcp-scan | [S] |
| 4 | 2025-04-07 (update 04-09) | **WhatsApp MCP exfiltration.** A malicious "sleeper" server rug-pulls and poisons the agent, which forwards the chat history via the trusted whatsapp-mcp server. The 04-09 variant needs no malicious server: an injected WhatsApp message alone leaks contacts. | Invariant Labs | Rug pull + tool poisoning + cross-server shadowing | Full chat history exfiltrated in the PoC. The Cursor approval UI did not show the changed recipient number. | https://invariantlabs.ai/blog/whatsapp-mcp-exploited ; https://www.docker.com/blog/mcp-horror-stories-whatsapp-data-exfiltration-issue/ | [S] |
| 5 | 2025-04-28 | Microsoft developer blog defines tool poisoning as a form of indirect prompt injection and recommends Prompt Shields | Microsoft | Guidance | n/a | https://developer.microsoft.com/blog/protecting-against-indirect-injection-attacks-mcp/ | [S] |
| 6 | 2025-05-19 | Windows "Securing MCP" post. Lists tool poisoning as a risk. Plans a registry with mandatory code signing and a rule that "tool definitions cannot be changed at runtime." These were preview commitments. | Microsoft Windows | Guidance / platform control | n/a | https://blogs.windows.com/windowsexperience/2025/05/19/securing-the-model-context-protocol-building-a-safer-agentic-future-on-windows/ | [S] |
| 7 | 2025-05-26 | **GitHub MCP "toxic agent flow."** A malicious public issue hijacks the agent, which leaks private-repo data into a public PR. Described as architectural, not a code bug. | Invariant Labs | Indirect prompt injection (via data, not descriptions) | GitHub MCP had about 14k stars; no clean fix | https://invariantlabs.ai/blog/mcp-github-vulnerability ; https://devclass.com/ai-ml/2025/05/27/researchers-warn-of-prompt-injection-vulnerability-in-github-mcp-with-no-obvious-fix/1623458 | [S] |
| 8 | 2025-06 (found 06-04, disclosed about 06-18) | **Asana MCP cross-tenant data exposure** (logic bug in tenant isolation) | Asana (self-disclosed) | Access-control bug | About 1,000 customers potentially affected. Server offline about 2 weeks. Exposure-window dates differ across sources. | https://www.bleepingcomputer.com/news/security/asana-warns-mcp-ai-feature-exposed-customer-data-to-other-orgs/ ; https://upguard.com/blog/asana-discloses-data-exposure-bug-in-mcp-server | [S] |
| 9 | 2025-06 (disclosure; fixed in 0.14.1) | **CVE-2025-49596** MCP Inspector RCE (no auth between client and proxy; DNS rebinding / 0.0.0.0) | Oligo Security | Dev-tool RCE | CVSS 9.4 | https://www.oligo.security/blog/critical-rce-vulnerability-in-anthropic-mcp-inspector-cve-2025-49596 ; https://thehackernews.com/2025/07/critical-vulnerability-in-anthropics.html | [S] |
| 10 | 2025-06-13 report, fixed by 06-15; public about Oct 2025 | **Smithery.ai path traversal** (`dockerBuildPath: ".."`) leaked an over-privileged fly.io token covering 3,243 apps (mostly MCP servers) | GitGuardian | Registry/hosting supply chain | Patched quickly; no evidence of exploitation | https://scworld.com/news/smithery-ai-fixes-path-traversal-flaw-that-exposed-3000-mcp-servers | [S-2nd] |
| 11 | 2025-06-25 | Backslash Security: >7,000 MCP servers analysed. "NeighborJack": hundreds bound to 0.0.0.0. Dozens allowed arbitrary command execution. | Backslash (vendor PR) | Misconfig / cmd exec | see B | https://markets.financialcontent.com/pawtuckettimes/article/gnwcq-2025-6-25-backslash-security-exposes-critical-flaws-in-hundreds-of-public-mcp-servers | [S] |
| 12 | 2025-07 (fix in 0.1.16) | **CVE-2025-6514** mcp-remote OS command injection via a malicious `authorization_endpoint` during OAuth | JFrog | Client-side RCE from malicious server | CVSS 9.6; affects 0.0.5–0.1.15 | https://jfrog.com/blog/2025-6514-critical-mcp-remote-rce-vulnerability/ | [S] |
| 13 | 2025-07 (fix 2025.7.1) | **CVE-2025-53109 / CVE-2025-53110 "EscapeRoute"** in Anthropic Filesystem MCP server (symlink bypass; prefix-match directory escape) | Cymulate | Sandbox escape | NVD 7.3; Cymulate scored 53109 at 8.4 | https://cymulate.com/blog/cve-2025-53109-53110-escaperoute-anthropic/ | [S] |
| 14 | 2025-07-06 | **Supabase MCP + Cursor "lethal trifecta."** A support-ticket injection makes the agent (service_role) read `integration_tokens` and write them into the ticket thread. | General Analysis; analysed by Simon Willison | Indirect prompt injection + excessive privilege | Demonstration; least privilege is the recommended fix | https://simonwillison.net/2025/Jul/6/supabase-mcp-lethal-trifecta/ | [S] (primary General Analysis post not seen) |
| 15 | 2025-07 | CVE-2025-53355 mcp-server-kubernetes: command injection via `execSync` | (GitLab advisory DB) | Cmd injection | n/a | https://advisories.gitlab.com/pkg/npm/mcp-server-kubernetes/CVE-2025-53355/ | [S] |
| 16 | 2025-08 | **CVE-2025-54136 "MCPoison" (Cursor).** An approved `.cursor/rules/mcp.json` can later be swapped for a malicious command with no re-prompt. This is a **rug pull at the config layer**. | Check Point Research | Rug pull / trust-on-first-use bypass | CVSS 7.2 (THN) vs 8.8 (Tenable). Fixed version not confirmed here. | https://blog.checkpoint.com/research/cursor-ide-persistent-code-execution-via-mcp-trust-bypass/ ; https://thehackernews.com/2025/08/cursor-ai-code-editor-vulnerability.html | [S] |
| 17 | 2025-09-15/17 | **postmark-mcp**: first malicious MCP server in the wild. In v1.0.16, one added line BCC'd every email to the attacker's domain. | Koi Security | Supply-chain rug pull (benign versions, then malicious update) | 1,643 downloads before removal | https://thehackernews.com/2025/09/first-malicious-mcp-server-found.html | [S] |
| 18 | 2025-09 / 2025-10 | MITRE ATLAS adds agent techniques: AML.T0110 AI Agent Tool Poisoning; AML.T0104 Publish Poisoned AI Agent Tool; AML.T0109 AI Supply Chain Rug Pull. Case studies AML.CS0053 (postmark-mcp) and AML.CS0054 (remote poisoned MCP tool). | MITRE (with Zenity Labs contributions) | Taxonomy | see C | https://d3fend.mitre.org/offensive-technique/attack/AML.T0110/ ; (summaries) https://www.startupdefense.io/mitre-atlas-case-studies/aml-cs0053-poisoned-postmark-mcp-server-email-exfiltration | [S] — confirm on atlas.mitre.org |
| 19 | 2025-12 fixes; publicised 2026-01 | **CVE-2025-68143 / 68144 / 68145** in Anthropic `mcp-server-git` (unrestricted git_init; argument injection in git_diff/checkout; `--repository` path bypass). Triggerable via prompt injection; RCE when chained with Filesystem MCP. | Cyata | Prompt-injection-reachable server bugs | Fixed in about 2025.12.18. CVSS figures differ by source. | https://thehackernews.com/2026/01/three-flaws-in-anthropic-mcp-git-server.html ; https://www.theregister.com/2026/01/20/anthropic_prompt_injection_flaws/ | [S] |
| 20 | 2026-01-27 | CoSAI "Model Context Protocol (MCP) Security" white paper (OASIS) | CoSAI / OASIS | Standards | see C | https://www.oasis-open.org/2026/01/27/coalition-for-secure-ai-releases-extensive-taxonomy-for-model-context-protocol-security | [S] |
| 21 | 2026-01 to 02 | "30+ CVEs in 60 days" against MCP servers, clients and infrastructure, about 43% command-injection patterns | Blog aggregations | Mixed | Loose tally; not authoritative | https://www.heyuan110.com/posts/ai/2026-03-10-mcp-security-2026/ | [S-2nd] |
| 22 | 2026-04 (about 04-15) | **OX Security "MCP STDIO RCE by design."** Official SDKs' stdio transport launches the `command` field without validation. Anthropic reportedly called it expected behaviour. Downstream CVEs include LiteLLM CVE-2026-30623 and Windsurf CVE-2026-30615. | OX Security | Design-level command execution via config | Claimed scale: 150M downloads, 7,000+ public servers, 200+ projects. These are vendor figures, quoted second-hand. | https://labs.cloudsecurityalliance.org/wp-content/uploads/2026/04/CSA_research_note_mcp-sdk-rce-by-design_20260422-csa-styled-1.pdf (AI-assisted CSA note) ; https://www.flyingpenguin.com/ox-security-report-anthropic-mcp-is-execute-first-validate-never/ | [S-2nd] |
| 23 | 2026-04 | CVE-2026-5058 aws-mcp-server, CVSS 9.8 RCE (secondary) | n/a | Implementation | n/a | https://calmara.app/blog/is-mcp-safe-security-risks | [S-2nd] |
| 24 | 2026-05 | "chain-key-validator" campaign: 10 npm packages posing as Web3 security MCP servers steal credentials, wallet keys and SSH keys | (advisory DB) | Malicious MCP packages | n/a | https://db.gcve.eu/vuln/MAL-2026-4202 | [S] (not opened) |
| 25 | 2026-05-20 | **NSA AISC Cybersecurity Information Sheet** "MCP: Security Design Considerations for AI-Driven Automation" | NSA | Government guidance | see C | https://www.nsa.gov/Press-Room/Press-Releases-Statements/Press-Release-View/Article/4496698/ ; https://www.nsa.gov/Portals/75/documents/Cybersecurity/CSI_MCP_SECURITY.pdf | [S] |
| 26 | 2026-06 | MAL-2026-5479: unscoped npm package impersonating `@modelcontextprotocol/server-github`. Its install script POSTs host, cwd and env details to a hardcoded endpoint. | OSV | Typosquat malicious MCP server | n/a | https://osv.dev/vulnerability/MAL-2026-5479 | [S] (fetch blocked) |
| 27 | 2026-08 | Shai-Hulud worm variant "evolves into MCP." >440 npm packages compromised; infected Claude Code / VS Code settings files distributed via 5 GitHub repos. | OX Security | Supply-chain worm reaching agent config | Vendor figures | https://www.ox.security/blog/shai-hulud-outbreak-debrief-the-worm-evolves-into-mcp/ | [S] (fetch blocked) |
| 28 | 2026-08 | "GhostSplice" disclosure: a controlled PoC, not a real intrusion. The same source states no public breach had been attributed to MCP tool poisoning as of Aug 2026. | (per Calmara blog) | Tool poisoning PoC | **Key point: no confirmed in-the-wild tool-description-poisoning breach found** | https://calmara.app/blog/is-mcp-safe-security-risks | [S-2nd] |
| 29 | 2026-08-04 | Anaconda acquires Enkrypt AI after Enkrypt's scan of 25,000 servers | n/a | Market signal | see B | https://letsdatascience.com/blog/a-scanner-checked-25000-mcp-servers-anaconda-just-bought-it | [S-2nd] |
| 30 | 2026-10 (ongoing) | GitHub Advisory DB: ongoing MCP-related advisories, e.g. `@modelcontextprotocol/client` CVE-2026-104850 (High, 2026-10-06), `modelcontextprotocol/go-sdk` GHSA-xw59-hvm2-8pj6 (High, 2026-04-01), googleapis/mcp-toolbox GHSA-76g7-m3xw-x9gr (Critical, 2026-06-13), awslabs.aws-api-mcp-server GHSA-29w2-fq35-v728 (High, 2026-07-24) | GitHub | Mixed | see the CVE-count note below | https://github.com/advisories?query=%22model+context+protocol%22 | [F] |

**Takeaways from the timeline**

- **The poisoning incidents are proofs of concept, not field breaches.**
  - Every disclosure specific to tool-description poisoning (#2, #4, #28) is a PoC.
  - The real in-the-wild malicious servers (#17 postmark-mcp, #24, #26, #27) poisoned the **code or package**, not the tool description.
  - postmark-mcp was a **version-level rug pull**: benign versions shipped first, then a malicious update. MITRE models this as AML.T0109.
- **The config-layer rug pull is a real CVE.** MCPoison (#16) is a rug pull at the configuration layer, so "approve once, trust forever" is a documented weakness with a CVE number.

**MCP CVE / advisory count (fetched 2026-10-07)**

- GitHub Advisory DB, query `"model context protocol"`: **33 advisories**. [F] https://github.com/advisories?query=%22model+context+protocol%22
- GitHub Advisory DB, query `mcp`: **919 advisories**. This is a full-text match and includes noise such as Langflow and SiYuan entries that merely mention MCP, so it is an upper bound only. [F] https://github.com/advisories?query=mcp
- **Neither number is a clean count of "MCP CVEs."** A defensible count needs a manual pass over the results; the NVD API was blocked.
- Other published tallies:
  - "≥7 NVD CVEs on named MCP servers as of Apr 2026" (mcp.directory) [S-2nd]
  - "≥14 CVEs, 5 with CVSS ≥9.0, Apr 2025–Apr 2026" (Zealynx breach index, https://www.zealynx.io/research/adversarial-security/mcp-breach-index-2025-2026) [S-2nd]
  - "30+ CVEs Jan–Feb 2026" [S-2nd]
  - **These tallies disagree because they count different scopes.**

---

## B. Quantitative ecosystem studies (industry)

| Study (date) | Sample | Headline numbers | Caveats | URL | Evidence |
|---|---|---|---|---|---|
| Equixly (Mar 2025) | "popular MCP servers" (n not seen) | 43% command injection; 22% path traversal; 30% SSRF | Primary not opened; sample size unknown | equixly.com/blog/2025/03/29/mcp-server-new-security-nightmare | [S-2nd] |
| Backslash Security (2025-06-25) | >7,000 servers | Hundreds bound to 0.0.0.0 ("NeighborJack"); dozens allow arbitrary command execution | Vendor PR; no exact percentages seen | link in A#11 | [S] |
| Knostic (about Jul 2025) | Shodan fingerprinting | **1,862** internet-exposed MCP servers. A manual sample of 119 found **119/119** returned tools/list with no authentication. | Public-internet only | https://www.knostic.ai/blog/mapping-mcp-servers-study ; https://darkreading.com/vulnerabilities-threats/2000-mcp-servers-security | [S] |
| Trend Micro (Jul 2025, plus update) | Internet scan | **492** exposed servers with no client auth or encryption; 1,402 tools; >90% of tools give direct read access to data; about 74% on major clouds | | https://www.trendmicro.com/vinfo/hk/security/news/cybercrime-and-digital-threats/mcp-security-network-exposed-servers-are-backdoors-to-your-private-data | [S] |
| Pynt "Quantifying Risk Exposure Across 281 MCPs" (2025) | 281 servers | 72% expose ≥1 sensitive capability; 13% accept untrusted inputs; 9% high-risk. Modelled exploitable-configuration probability is 9% (1 server), 36% (2), >50% (3) and **92% (10)**. | The 92% is a compounded-probability model, not observed breaches | https://www.pynt.io/blog/llm-security-blogs/state-of-mcp-security ; https://venturebeat.com/security/mcp-stacks-have-a-92-exploit-probability-how-10-plugins-became-enterprise | [S] |
| Astrix "State of MCP Server Security 2025" (2025-10-15) | >5,200 OSS servers | 88% need credentials; **53% use long-lived static secrets**; 8.5% use OAuth; 79% pass API keys via env vars | Credential hygiene, not poisoning | https://astrix.security/learn/blog/state-of-mcp-server-security-2025/ | [S] |
| Enkrypt AI (Oct 2025) | 1,000 servers | **33%** had critical vulnerabilities | Methodology not seen | https://enkryptai.com/blog/we-scanned-1-000-mcp-servers-33-had-critical-vulnerabilities | [S] |
| Enkrypt AI (about mid-2026) | 25,000 servers / 268,000 tools | 143,000 findings; **73%** of servers affected (all severities) | Not comparable with the 33% figure | https://letsdatascience.com/blog/a-scanner-checked-25000-mcp-servers-anaconda-just-bought-it | [S-2nd] |
| Securin | 1,770 repos | 70% contain command-injection-type flaws | Secondary | https://www.securin.io/articles/mcp-servers-risk-assessment | [S-2nd] |
| "1,808-server audit" (Jan 2026) | 1,808 servers | 66% have ≥1 finding; 43% shell/command injection | **Attribution conflicts** (AgentSeal vs AppSecSanta vs Invariant) | https://www.everydev.ai/developers/agentseal | [S-2nd] — do not cite without the primary |
| Registry auth audit (Feb 2026) | 518 servers in the official MCP Registry | 41% (214) had no authentication | Secondary only | via https://www.knostic.ai/... search summary | [S-2nd] |
| MintMCP claim | "public MCP servers" | 5.5% contain confirmed tool-poisoning vulnerabilities | Vendor; methodology unknown | https://www.mintmcp.com/blog/mcp-tool-poisoning | [S-2nd] |
| Snyk ToxicSkills (2026) | 3,984 agent **skills** (not MCP) | 13.4% (534) have ≥1 critical issue | Sibling ecosystem | (via search summary) | [S-2nd] |
| **AppSec Santa audit (2026)**, the only scanner-accuracy check found | 33 MCP servers; MCP-Scan v0.4.3 and Cisco mcp-scanner v4.3.0 | Cisco YARA engine flagged 27 patterns in 10 servers; on manual review **only 6 were genuine**. That is 21/27, about 78% false positives; I computed this, the article does not state it. Main cause: normal tool-dependency instructions get flagged as injection. | Small n; single reviewer | https://appsecsanta.com/research/mcp-server-security-audit-2026 | [S] (fetch blocked) |
| CSA research note (lab) | >45 real MCP servers | Attack success rates >60%; best agent model 72.8% | Lab benchmark relayed by an AI-assisted CSA note (probably MCPTox, an academic source) | https://labs.cloudsecurityalliance.org/research/csa-research-note-mcp-tool-poisoning-ai-agent-exfiltration-2/ | [S-2nd] |

**Observation.**
- Industry numbers are plentiful for **exposure and implementation bugs**: command injection, missing auth, static secrets.
- Almost no industry study measures the **prevalence of poisoned tool descriptions**. The only such figure is MintMCP's unverifiable 5.5%.
- Almost no study measures the **accuracy of detectors** either. The only one is the small AppSec Santa audit, which points to high false-positive rates.

---

## C. Standards and guidance

| Body / document | Date | What it says relevant to tool poisoning | URL | Evidence |
|---|---|---|---|---|
| **MCP spec, Security Best Practices** | Introduced in 2025-06-18; carried into 2025-11-25 | Main topics found: **confused deputy** (OAuth proxy needs per-client consent) and **token passthrough** (explicitly forbidden). Other topics such as SSRF and session hijacking are not confirmed. I found **no evidence that the page covers tool-description poisoning, rug pulls, pinning or signing**, but I could not fetch the page to confirm. | https://modelcontextprotocol.io/specification/latest/basic/security_best_practices ; https://modelcontextprotocol.io/specification/2025-06-18/basic/security_best_practices | [S] |
| MCP spec, `notifications/tools/list_changed` | n/a | The protocol signals tool-list changes. The spec does **not** require clients to re-prompt for trust. Cursor CLI and Claude Code reportedly ignore it mid-session (forum report). | https://ts.sdk.modelcontextprotocol.io/v2/servers/notifications.html ; https://forum.cursor.com/t/mcp-notifications-tools-list-changed-not-acted-on-mid-session/161459 | [S] |
| **Official MCP Registry** | Preview since 2025-09-08 | Namespace ownership checked at publish time (GitHub OAuth/OIDC, DNS/HTTP challenge). **No signing, provenance or integrity of server.json described.** Security scanning is delegated to npm, PyPI and Docker Hub. | https://github.com/modelcontextprotocol/registry ; https://modelcontextprotocol.io/registry/about | [F] (GitHub README) |
| **OWASP Top 10 for LLM Apps 2025** | 2024-11 / 2025 edition | LLM01 Prompt Injection (direct and indirect, including via tool responses); LLM03 Supply Chain (moved from #5 to #3, includes plugins); LLM06 Excessive Agency (excess functionality, permissions or autonomy) | https://genai.owasp.org/llm-top-10/ (official; not fetched) ; summary: https://promptfoo.dev/docs/red-team/owasp-llm-top-10/ | [S] |
| **OWASP Top 10 for Agentic Applications 2026** | 2025-12-09 | ASI01–ASI10. Relevant here: ASI02 Tool Misuse & Exploitation, ASI03 Identity & Privilege Abuse, ASI04 (Agentic) Supply Chain, ASI08 Cascading Failures. | https://www.giskard.ai/knowledge/owasp-top-10-for-agentic-application-2026 ; https://cycode.com/blog/owasp-top-10-agentic-applications/ | [S-2nd] |
| OWASP Agentic Threats & Mitigations (ASI, "T2 Tool Misuse") | 2025 | Search did not confirm the T-numbering; marked UNVERIFIED | n/a | UNVERIFIED |
| **OWASP MCP Top 10** | 2025 (beta/pilot phase per secondary source) | **MCP03:2025 Tool Poisoning**: attacker compromises tools, plugins or their outputs. Mitigations listed by secondary sources: treat metadata as untrusted, sign manifests, re-review on version change, runtime proxies. | https://owasp.org/www-project-mcp-top-10/ ; also OWASP community page https://owasp.org/www-community/attacks/MCP_Tool_Poisoning | [S] |
| **CoSAI MCP Security white paper** (OASIS) | Approved 2026-01-08; released 2026-01-27 | Covers threat modelling, MCP supply chain, IAM, deployment, and recommended protocol changes. Counts: ">40 threats" (Adversa) or "12 threat categories" (CoSAI guide). | https://www.coalitionforsecureai.org/wp-content/uploads/2026/03/model-context-protocol-security-1.pdf ; https://www.oasis-open.org/2026/01/27/coalition-for-secure-ai-releases-extensive-taxonomy-for-model-context-protocol-security | [S] |
| **CSA** | 2026 | I found no official, peer-reviewed CSA MCP standard. CSA "Labs" research notes exist (tool poisoning 2026-07-11, auto-execution 2026-07-01, tool-poisoning/rug-pull white paper 2026-05-06, STDIO RCE 2026-04-22, ATLAS gap analysis 2026-03-27, MCPA certification 2026-09-25). At least some are labelled **AI-generated and not officially reviewed**. | https://labs.cloudsecurityalliance.org/research/csa-research-note-mcp-tool-description-poisoning-20260711-cs/ ; https://labs.cloudsecurityalliance.org/research-rb/csa-whitepaper-mcp-security-tool-poisoning-20260506-csa-styl/ | [S] |
| **NIST AI 100-2e2025** (Adversarial ML taxonomy) | 2025-03 | The GenAI section covers supply-chain attacks, direct and **indirect prompt injection**, and (new in 2025) security of AI agents. Each attack is paired with mitigations and their limits. MCP is not confirmed to be named. | https://nvlpubs.nist.gov/nistpubs/ai/nist.ai.100-2e2025.pdf ; doi:10.6028/NIST.AI.100-2e2025 | [S] |
| **MITRE ATLAS** | v5.x, 2025-09 onward | AML.T0110 AI Agent Tool Poisoning (Persistence: altered tool descriptions or parameters); AML.T0104 Publish Poisoned AI Agent Tool; AML.T0109 AI Supply Chain Rug Pull; AML.T0080 AI Agent Context Poisoning; AML.T0086 Exfiltration via AI Agent Tool Invocation. Case studies AML.CS0053 (postmark-mcp) and AML.CS0054. CSA gap analysis says tool-chain poisoning and MCP-server-as-pivot are still under-represented. | https://d3fend.mitre.org/offensive-technique/attack/AML.T0110/ ; https://labs.cloudsecurityalliance.org/research/csa-research-note-atlas-agentic-gap-analysis-20260327/ | [S] — confirm IDs on atlas.mitre.org |
| **NSA AISC CSI on MCP** | 2026-05-20 | MCP adoption has outpaced its security model. Names risks: dynamic tool invocation, implicit trust, context sharing, weak access control, serialization, approval workflows, token lifecycle, audit logging. | https://www.nsa.gov/Portals/75/documents/Cybersecurity/CSI_MCP_SECURITY.pdf | [S] |
| Microsoft (Windows MCP registry; MCP-for-Beginners) | 2025-05 / 2025 | Planned: code signing, **immutable tool definitions at runtime**, proxy-mediated access, isolation. The course maps tool poisoning to integrity verification and Prompt Shields. | link in A#6 ; https://learn.microsoft.com/windows/ai/mcp/servers/mcp-server-overview | [S] |
| EU / ENISA / BSI / UK NCSC | n/a | **None found** for MCP-specific guidance (one search). Treat as not found, not as absent. | n/a | n/a |

---

## D. Existing defensive tools and products

### D.1 Tool notes

- **Invariant MCP-Scan → Snyk Agent Scan** ([F] https://github.com/snyk/agent-scan ; [F] https://github.com/snyk/agent-scan/blob/v0.3.0/README.md)
  - **Hash pinning.** v0.3.0 "detects changes to MCP tools via hashing" to catch rug pulls. It keeps a whitelist of (type, name, hash).
  - **Proxy and guardrails.** v0.3.0 has a `proxy` mode with local guardrails (PII, secrets, tool restrictions, custom rules).
  - **Current scanning.** The current README (v0.5/v0.6) sends tool names and descriptions to the **Agent Scan API**, with secrets redacted. Detected risks:
    - E001 prompt injection in description
    - E002 tool shadowing
    - W015–W020 toxic-flow labels
    - W021 hidden Unicode
  - **Risk score.** v0.6 adds 0–1000 risk scores ([F] docs/risks.md).
  - **Hashing gone from current docs.** The current README, issue-codes and risks docs make **no mention of hash pinning or change detection**.
  - **No metrics.** No published precision or recall.
  - **Ownership.** Snyk acquired Invariant (reported June 2025) [S].
- **Invariant Guardrails / Gateway** ([F] https://github.com/invariantlabs-ai/invariant)
  - A transparent MCP/LLM proxy with a Python-like rule language. It supports flow rules, e.g. "read inbox → send email to an unknown address", and has a prompt-injection detector with a threshold.
  - No metrics published.
- **Cisco AI Defense mcp-scanner** ([F] https://github.com/cisco-ai-defense/mcp-scanner ; [F] https://pypi.org/project/cisco-ai-mcp-scanner/4.8.0/)
  - Detection engines: YARA, LLM-as-judge, and the Cisco AI Defense API.
  - **Behavioral Analyzer**: LLM-based check that docstrings match the code, with cross-file dataflow.
  - Prompt-defense regex (12 vectors), VirusTotal hash lookups for binaries, pip-audit, and sandboxed package scanning.
  - **No pinning or diffing. No evaluation metrics.**
  - Latest release seen: 4.8.5 (2026-10-02).
  - The only third-party accuracy evidence is the AppSec Santa audit (high false positives).
- **Docker MCP Gateway** ([F] https://www.docker.com/blog/docker-mcp-gateway-secure-infrastructure-for-agentic-ai/ (2025-07-09) ; [F] https://github.com/docker/mcp-gateway)
  - Security flags: `--verify-signatures` (provenance of the MCP **container image**), `--block-secrets` (scans inbound and outbound payloads), `--log-calls`.
  - Pluggable interceptors.
  - Each server runs in its own container.
  - Per-profile tool allowlists.
  - No description scanning or pinning documented.
- **Lasso MCP Gateway** ([F] https://github.com/lasso-security/mcp-gateway)
  - `--scan` gives a reputation score from Smithery, npm and GitHub data, with a block threshold of 30.
  - It also scans tool descriptions for hidden instructions, sensitive file patterns and malicious actions, and writes `blocked` into the config.
  - Plugins: basic (secret masking), presidio (PII), lasso (API-based prompt injection and custom policy), xetrack (tracing).
  - No hashing or signatures. No metrics.
- **Stacklok ToolHive** ([F] https://github.com/stacklok/toolhive ; [S] https://stacklok.com/blog/from-unknown-to-verified-solving-the-mcp-server-trust-problem/)
  - Each server runs in a container with a minimal permission profile and network isolation.
  - **Sigstore/GitHub attestation image verification** with `--image-verification=disabled|warn|enforce` [S].
  - **Cedar** authorization policies [S].
  - Registry that can "verify provenance and sign servers" [F].
  - Tool filtering and description overrides, framed as a token-saving feature.
  - Audit logs and OpenTelemetry.
  - No description scanning documented.
- **EQTY Lab MCP Guardian** ([F] https://github.com/eqtylab/mcp-guardian)
  - Proxy with message logging and real-time human approve/deny of tool calls.
  - Automated safety scanning is "Coming Soon."
  - No hashing.
- **Enkrypt AI Secure MCP Gateway + MCP Scanner** ([F] https://github.com/enkryptai/secure-mcp-gateway ; [S] https://www.enkryptai.com/blog/how-enkrypts-secure-mcp-gateway-and-mcp-scanner-prevent-top-attacks)
  - Gateway "with guardrails at each MCP server," plus a static scanner (command injection, secrets).
  - Specific poisoning or change-detection features are not documented on the pages seen.
- **Cloudflare MCP Server Portals / Gateway** ([S] https://blog.cloudflare.com/zero-trust-mcp-server-portals ; https://developers.cloudflare.com/cloudflare-one/access-controls/ai-controls/mcp-portals/index.md)
  - Access-authenticated portal, per-portal tool curation, MCP traffic detection, and tool-call blocking ("WriteGuard").
  - **No tool-description inspection documented.** AI-WAF prompt-injection rules were a roadmap item.
- **Microsoft**
  - Windows MCP registry plans: signing, immutable tool definitions, containment [S].
  - Azure Prompt Shields / Content Safety, mapped to MCP in training material [S].
  - **Azure API Management MCP-specific poisoning controls not found.**
- **Pillar Security, Prompt Security, Lakera**
  - Only a third-party comparison was found:
    - Lakera: runtime enforcement
    - Prompt Security: MCP inventory and risk scoring
    - Pillar: posture management and red teaming
  - Product documentation was **not seen**, because the search budget was exhausted. https://toolradar.com/guides/best-mcp-gateways [S-2nd]
- **ETDI (Enhanced Tool Definition Interface)** ([S] https://arxiv.org/html/2506.01333v1 ; https://pypi.org/project/mcp-etdi ; https://github.com/modelcontextprotocol/python-sdk/pull/845)
  - Proposal: cryptographically signed, immutable, versioned tool definitions, OAuth-scoped permissions, and a policy engine.
  - Reference SDK on PyPI. The PR to the official SDK has an unknown merge state.
  - **Not adopted into the MCP spec** (none found).
  - Note: the arXiv paper is academic, but it is listed here as the origin of the tool.
- **Official MCP Registry**
  - Namespace verification only. No signing of server.json [F].
- **Clients**
  - **Claude Code** ([F] https://code.claude.com/docs/en/security):
    - Workspace trust dialog.
    - Separate approval prompt for project `.mcp.json` servers; `-p` mode shows neither prompt.
    - Managed MCP allow/deny configuration.
    - Permission rules per MCP tool; Auto mode classifier.
    - Sandboxed bash.
    - The documentation says Anthropic "does not security-audit or manage any MCP server." There is **no documented detection of tool-description changes.**
    - A Repello write-up reports that `.mcp.json` approval is keyed to the server **name**: changing the command under the same name ran without a re-prompt in v2.1.170. https://repello.ai/blog/claude-code-mcp-name-keyed-trust [S]
  - **Cursor**: MCPoison (CVE-2025-54136) showed approve-once behaviour. The fix details were not verified. https://thehackernews.com/2025/08/cursor-ai-code-editor-vulnerability.html [S]
  - **VS Code**: not verified (docs blocked, search budget exhausted).

### D.2 Feature matrix

Legend:
- **Y** = documented feature, with source.
- **P** = partial or adjacent feature (scope noted).
- **ND** = not documented on the pages I could see.
- **n/a** = out of scope for the product.

| Tool | Description pinning / hash | Signature verification | Rule / LLM description scanning | Semantic drift between versions | Explicit capability policy | Runtime sandbox / monitoring | Risk scoring | Published evaluation with metrics |
|---|---|---|---|---|---|---|---|---|
| mcp-scan / Snyk Agent Scan | **Y** in v0.3.0 (hash whitelist; https://github.com/snyk/agent-scan/blob/v0.3.0/README.md); ND in the current README | ND | **Y** (remote API: E001/E002/W021; https://github.com/snyk/agent-scan/blob/main/docs/issue-codes.md) | ND (hash = exact change only, no semantic comparison) | P (v0.3 guardrail rules: tool restrictions) | P (v0.3 `proxy` monitoring; current "background mode" re-scans) | **Y** (0–1000; https://github.com/snyk/agent-scan/blob/main/docs/risks.md) | ND |
| Invariant Guardrails / Gateway | ND | ND | P (prompt-injection detector; https://github.com/invariantlabs-ai/invariant) | ND | **Y** (rule language incl. flow rules) | **Y** (proxy on every MCP call) | ND | ND |
| Cisco mcp-scanner | ND | ND | **Y** (YARA + LLM judge + AI Defense; https://github.com/cisco-ai-defense/mcp-scanner) | ND | ND | P (Docker sandbox for package analysis; static behavioural code analysis) | P (severity per finding) | ND (third-party: about 78% FP of YARA flags, n=33 servers; https://appsecsanta.com/research/mcp-server-security-audit-2026) |
| Docker MCP Gateway | ND | **Y** (image provenance `--verify-signatures`; https://www.docker.com/blog/docker-mcp-gateway-secure-infrastructure-for-agentic-ai/) | ND | ND | P (tool allowlist per profile; https://github.com/docker/mcp-gateway) | **Y** (container per server; secret blocking; call logging) | ND | ND |
| Lasso MCP Gateway | ND | ND | **Y** (`--scan` of descriptions, plus Lasso API plugin; https://github.com/lasso-security/mcp-gateway) | ND | ND | P (proxy with masking/guardrail plugins; tracing) | **Y** (reputation score, threshold 30) | ND |
| Stacklok ToolHive | ND | **Y** (Sigstore/attestation image verification; https://stacklok.com/blog/from-unknown-to-verified-solving-the-mcp-server-trust-problem/ [S]) | ND | ND | **Y** (Cedar authz [S]; permission profiles; https://github.com/stacklok/toolhive) | **Y** (container isolation, network isolation, audit/OTel) | ND | ND |
| EQTY Lab MCP Guardian | ND | ND | ND ("coming soon"; https://github.com/eqtylab/mcp-guardian) | ND | P (human approve/deny per call) | **Y** (logging proxy) | ND | ND |
| Enkrypt Secure MCP Gateway / Scanner | ND | ND | P ("guardrails" claimed; specifics ND; https://github.com/enkryptai/secure-mcp-gateway) | ND | ND | P (gateway) | ND | ND (ecosystem scan counts only, not detector accuracy) |
| Cloudflare MCP Server Portals | ND | ND | ND | ND | **Y** (tool curation; WriteGuard blocking of tool calls; https://developers.cloudflare.com/cloudflare-one/access-controls/ai-controls/mcp-portals/index.md [S]) | P (traffic detection and logging) | ND | ND |
| Microsoft (Windows MCP registry / Prompt Shields) | P ("tool definitions cannot change at runtime", planned; https://blogs.windows.com/windowsexperience/2025/05/19/securing-the-model-context-protocol-building-a-safer-agentic-future-on-windows/ [S]) | P (mandatory code signing, planned) | P (Prompt Shields, general; https://developer.microsoft.com/blog/protecting-against-indirect-injection-attacks-mcp/ [S]) | ND | P (agent session containment) | **Y** (contained agent session; https://learn.microsoft.com/windows/ai/mcp/servers/mcp-server-overview [S]) | ND | ND |
| Pillar / Prompt Security / Lakera | ND (not checked) | ND | ND (vendor claims only via a third party) | ND | ND | ND | P (Prompt Security "risk scoring" per third party; https://toolradar.com/guides/best-mcp-gateways) | ND |
| ETDI (proposal + SDK) | **Y** (immutable versioned definitions; https://arxiv.org/html/2506.01333v1 [S]) | **Y** (signed tool definitions) | ND | ND | **Y** (OAuth scopes + policy engine) | ND | ND | ND (no industry evaluation seen) |
| Official MCP Registry | ND | ND (namespace ownership only; https://github.com/modelcontextprotocol/registry) | ND | ND | n/a | n/a | ND | n/a |
| Claude Code (client) | ND (no description change detection documented; name-keyed approval per https://repello.ai/blog/claude-code-mcp-name-keyed-trust [S]) | ND | ND | ND | **Y** (per-tool permission rules, managed MCP allow/deny; https://code.claude.com/docs/en/security) | **Y** (bash sandbox; Auto-mode classifier) | ND | ND |
| Cursor (client) | ND (MCPoison showed none at disclosure) | ND | ND | ND | P (tool approval prompts) | ND | ND | ND |
| VS Code (client) | ND (not verified) | ND | ND | ND | ND | ND | ND | ND |

**Matrix result.**
- **No product publicly documents semantic-drift detection** between a trusted and a received tool description. The one hash-based change detector, mcp-scan v0.3, flags any byte-level change and no longer appears in the current docs.
- **No product publishes detection metrics** (precision, recall, FPR, latency) for its description scanner.

---

## E. Conclusion: which of the proposed layers are commoditized, and which lack public evaluation

Mapped against the user's five layers (see BRIEF.md):

### 1. Integrity checker (SHA-256 pinning; Ed25519 signatures)

- **Commoditized in practice: yes.**
  - Hash pinning of tool definitions shipped in mcp-scan from April 2025 (v0.3.0 docs).
  - Signing exists, but at the **container-image** level (Docker `--verify-signatures`, ToolHive Sigstore) and in proposals (ETDI, the Windows registry plan).
- **Gap: tool metadata itself is not signed.** No deployed product signs the tool-definition metadata (name, description, schema), and the official MCP Registry has no signing.
- **Evidence the gap matters:** real incidents show the weakness of trusting on first use without re-verification (MCPoison, the postmark-mcp version rug pull, Claude Code's name-keyed approval).
- **Novelty is low for plain hashing.** Any contribution would need:
  - (a) signing at the metadata level, end to end,
  - (b) a measured comparison against exact-hash pinning, e.g. false alarms from benign updates, which are never reported.

### 2. NLP / semantic poisoning detector

- **Commoditized: partly.** Rule-based and LLM-based scanning of descriptions is widespread:
  - Snyk Agent Scan (API)
  - Cisco (YARA + LLM judge + behavioural code alignment)
  - Lasso `--scan`
  - Invariant prompt-injection detector
- **No public evaluation.** None of these publishes precision, recall or FPR.
- **The only independent check found** (AppSec Santa, n=33 servers) suggests about 78% false positives for YARA flags. Small sample, my arithmetic, not peer-reviewed.
- **Semantic drift (trusted vs received embedding distance) is not offered by any product found.** This is the clearest open space, and it maps to the user's **RQ2**.

### 3. Permission / policy checker (capabilities from explicit policy, not from descriptions)

- **Commoditized.** Explicit capability policy is standard:
  - ToolHive Cedar
  - Docker and Cloudflare tool allowlists
  - Invariant rule language
  - Claude Code permission rules
  - ETDI scopes
- **Backed by guidance:** OWASP LLM06, ASI02/ASI03, and NSA least privilege.
- **Little novelty** unless the contribution is how policies are derived or checked against descriptions.

### 4. Runtime behaviour monitor (Docker sandbox, file/network monitoring, anomaly detection)

- **Sandboxing and call logging are commoditized:**
  - Docker MCP Gateway and ToolHive containers
  - Claude Code sandbox
  - MCP Guardian, Invariant and Lasso proxies
- **Anomaly detection over runtime behaviour is not documented** by any product found. Isolation Forest-style detection on file and network telemetry of MCP servers has no public evaluation.
- **Guidance supports it:** OWASP ASI02 describes "unexpected tool chaining", and the MCP03 mitigations recommend baselines.

### 5. Risk engine (weighted score → ALLOW/REVIEW/BLOCK)

- **Present in simple forms:**
  - Snyk 0–1000 risk scores
  - Lasso reputation threshold
  - Prompt Security risk scoring (third-party claim)
- **No public calibration or evaluation** of these scores.

### Key gaps confirmed across the landscape

| Gap | Evidence |
|---|---|
| **G1. No public, labelled benchmark from industry for tool-description poisoning detection, and no vendor precision/recall/FPR/latency figures.** | Every vendor README fetched lacks metrics (Snyk, Cisco, Lasso, Invariant, Docker, ToolHive, Guardian, Enkrypt). |
| **G2. Nobody detects semantic drift between versions.** Current change detection is exact-hash only (mcp-scan v0.3). Benign updates cannot be told apart from poisoned ones. | See D. |
| **G3. Layered (combined) defences have no published ablation.** Products combine scanning, proxy and policy, but no one reports whether combining helps (RQ3) or what the overhead is (RQ5). | See D. |
| **G4. The threat model is grounded but field prevalence is thin.** | **For the threat:** standards now name it (OWASP MCP03, ATLAS AML.T0110/T0109, CoSAI, NSA CSI), and there are real supply-chain rug pulls (postmark-mcp) and a CVE for config rug pulls (MCPoison). **Against claiming prevalence:** no confirmed in-the-wild breach via tool-*description* poisoning was found as of Aug 2026 (one secondary source). The paper should frame the threat as demonstrated and plausible, not as a measured epidemic. |
| **G5. The MCP spec leaves the trust model open.** It defines `tools/list_changed` but no re-consent requirement, and the official registry does not sign metadata. That leaves room for a protocol-compatible gateway contribution. | See C. |

### Follow-ups if more budget is available

- Fetch the primary pages blocked here: invariantlabs.ai, owasp.org MCP Top 10, the modelcontextprotocol.io security page, the NSA CSI PDF, the CoSAI PDF, atlas.mitre.org, appsecsanta.com.
- Check VS Code and Cursor current behaviour on tool-description change.
- Check Pillar, Prompt Security and Lakera documentation.
- Make a manual, filtered count of MCP CVEs in NVD.
