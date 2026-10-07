# Step 1a — What practitioners discuss, need and complain about: MCP tool poisoning, rug pulls, shadowing, server trust

Compiled 2026-10-07. Scope: Jan 2025 – Oct 2026. Covers practitioner discussions, not research papers.

---

## 0. Method and limitations (read first)

**What was accessible:**
- **GitHub web pages** (issues, PRs, discussions) via WebFetch. GitHub was the main source.
- **The official spec repo**, cloned at commit `0a11bf68`, dated 2026-10-06. Spec text, SEP files, docs and blog were read directly from disk.
- **WebSearch**, for a few searches before the shared per-turn search budget ran out (200 calls, shared with the other agents). No further searches were possible.

**What was blocked.** The egress proxy blocked these (EGRESS_BLOCKED / "unable to fetch"), so no thread on them could be read:
- reddit.com (WebSearch also refuses `reddit.com` as a domain filter)
- news.ycombinator.com and hn.algolia.com
- dev.to
- simonwillison.net
- lobste.rs
- forum.cursor.com
- security.stackexchange.com
- invariantlabs.ai

Per the hard rules, I did not route around the blocks.

**Consequences:**
- Reddit, HN, Stack Exchange and dev.to/Medium are **not represented** by threads I read. I have no Reddit or HN quotes and invent none.
- The sample is GitHub-heavy. That skews toward people who propose solutions (SEP authors, tool vendors). Many commenters promote their own scanners or proxies, and I flag this where visible. Ordinary end-user complaints ("I clicked approve") are under-represented.
- Section 1b lists a few items seen **only as search-result snippets**. They are not counted in theme tallies and not quoted.

**Quote fidelity:**
- Quotes come from the WebFetch output of each GitHub page, which is produced by a summarizing model told to quote verbatim. They should be exact, but **spot-check the wording against the URL before publication**.
- Quotes taken from spec, SEP and blog files in the cloned repo are exact.

**Engagement data:**
- GitHub reactions were mostly reported as "Reactions are currently unavailable" to the anonymous fetcher.
- Engagement is therefore the **comment count shown in GitHub search listings**, plus upvotes for Discussions.
- For PRs, the listing date is sometimes the close or merge date. This is marked.

**Governance context.** On 2025-09-25 (per the close notes) and around 2026-09-22/25, maintainer @localden closed most open "Ideas – Security" Discussions with: "We've limited Discussions in this repository to meeting notes and are closing this thread." Several SEP PRs were also closed because "every new SEP should be developed with a Working Group first" (see PR #3140). So a "closed" status usually reflects **process, not rejection on merits**, unless noted.

---

## 1. Source log

### 1a. Sources actually read (counted)

Abbreviations: **Spec** = github.com/modelcontextprotocol/modelcontextprotocol; **D#** = a Discussion; **c** = comments; **up** = upvotes.

| ID | Title (verbatim) | Platform / type | Date | URL | Engagement / status |
|---|---|---|---|---|---|
| S1 | SEP-1766: Digest-Pinned Tool Versioning and Interceptor-Based Validation in MCP | Spec repo issue (SEP proposal) | opened 2025-11-05; closed 2026-06-24 | https://github.com/modelcontextprotocol/modelcontextprotocol/issues/1766 | 12c in listing; closed, no sponsor |
| S2 | docs(security-ig): shared tool-definition drift (rug-pull) test corpus | Spec PR | opened & closed 2026-06-16 | https://github.com/modelcontextprotocol/modelcontextprotocol/pull/2924 | 2c; closed (go through IG first) |
| S3 | Add Enhanced Tool Definition Interface (ETDI): Prevents Tool Poisoning and Rug Pull Attacks with Immutable Versioned… | Spec PR | opened 2025-06-04; closed 2025-09-24 | https://github.com/modelcontextprotocol/modelcontextprotocol/pull/649 | 1c, 3 "hooray" reactions; closed (needs SEP) |
| S4 | SEP-1913: Trust and Sensitivity Annotations | Spec PR (SEP, GitHub + OpenAI authors) | opened 2025-11-27; active Oct 2026 | https://github.com/modelcontextprotocol/modelcontextprotocol/pull/1913 | 86c; **open**, draft, `roadmap/security` |
| S5 | SEP-2809: Attested Tool-Server Admission (ATSA) | Spec PR | opened 2026-05-28; updated 2026-09-30 | https://github.com/modelcontextprotocol/modelcontextprotocol/pull/2809 | 11c; **open**, no sponsor |
| S6 | SEP-2575 Regression: security gap around server identity being completely optional | Spec issue | opened 2026-06-02; closed 2026-08-30 | https://github.com/modelcontextprotocol/modelcontextprotocol/issues/2842 | 16c in listing; closed, "bug" |
| S7 | MCP "Server" terminology creates dangerous user misconceptions | Spec issue | opened 2025-06-02 | https://github.com/modelcontextprotocol/modelcontextprotocol/issues/630 | 13c in listing; closed "not planned" |
| S8 | Spec wording may create a False sense of Security | Spec issue | opened 2025-07-04; closed 2026-03-25 | https://github.com/modelcontextprotocol/modelcontextprotocol/issues/913 | 2c; closed via PR #2464 |
| S9 | docs: add local server security guide (+ resulting doc `local-server-security.mdx`) | Spec PR and official doc | opened 2026-07-10; merged 2026-10-05 | https://github.com/modelcontextprotocol/modelcontextprotocol/pull/3072 | 19c; **merged** |
| S10 | SEP-3140: Signed Capability Declarations & Trustworthy Trust Labels | Spec PR | opened 2026-07-27; closed 2026-09-22 | https://github.com/modelcontextprotocol/modelcontextprotocol/pull/3140 | 17c; closed (needs a Working Group) |
| S11 | Security: Recommend pre-installation scanning tools in the spec | Spec issue | opened 2026-03-13 | https://github.com/modelcontextprotocol/modelcontextprotocol/issues/2393 | 1c; closed |
| S12 | SEP-2091: Server Capability Signatures | Spec PR (by Sam Morrow, GitHub) | 2026-01-15 → closed 2026-01-28 | https://github.com/modelcontextprotocol/modelcontextprotocol/pull/2091 | 3 reactions; closed draft |
| S13 | MCP-2026-015: server/discover instructions field enables prompt injection (amplified by cacheScope:public) | Spec issue | opened 2026-08-07 | https://github.com/modelcontextprotocol/modelcontextprotocol/issues/3213 | 12c in listing; open |
| S14 | Signed tool manifests : additive extension for tool-poisoning / "rug pull" defense | Spec D#2913 | 2026-06-14 → 2026-09-22 | https://github.com/modelcontextprotocol/modelcontextprotocol/discussions/2913 | **30c**, 1up |
| S15 | Client-Side Tool Description Substitution as a Defense Against Indirect Prompt Injection in MCP | Spec D#2457 | 2026-03-24 | https://github.com/modelcontextprotocol/modelcontextprotocol/discussions/2457 | 5c, 2up |
| S16 | Measured the auth and capability posture of 13,000 public MCP endpoints - data and method inside | Spec D#3303 | 2026-08-25 | https://github.com/modelcontextprotocol/modelcontextprotocol/discussions/3303 | 15c, 1up |
| S17 | A free heuristic scanner for common MCP server security issues, looking for feedback | Spec D#3301 | 2026-08-24 | https://github.com/modelcontextprotocol/modelcontextprotocol/discussions/3301 | 3c, 1up |
| S18 | Security Concern: Systematic Forking and Republishing of MCP Servers as Supply-Chain Risk | Spec D#2444 | 2026-03-23 | https://github.com/modelcontextprotocol/modelcontextprotocol/discussions/2444 | 6c, 2up |
| S19 | Proposal: Model Context Protocol - Tool Layer Security (MCP-TLS) | Spec D#441 | 2025-04-30 | https://github.com/modelcontextprotocol/modelcontextprotocol/discussions/441 | 9c, 2up |
| S20 | handling tool bloat - hundreds of tools | Spec D#2036 | 2025-12-30 | https://github.com/modelcontextprotocol/modelcontextprotocol/discussions/2036 | 21c, 3up |
| S21 | Proposal: Permission Specification for MCP Tool Calls | Spec D#2498 | 2026-03-30 | https://github.com/modelcontextprotocol/modelcontextprotocol/discussions/2498 | **51c**, 2up |
| S22 | Runtime verification of declared vs observed MCP server capabilities | Spec D#3211 | 2026-08-07 | https://github.com/modelcontextprotocol/modelcontextprotocol/discussions/3211 | 1c, 1up |
| S23 | Proposal: Client-side Scope-Based Tool Filtering | Spec D#814 | 2025-06-21 | https://github.com/modelcontextprotocol/modelcontextprotocol/discussions/814 | 4c, 5up |
| S24 | SEP-1763: Interceptors for Model Context Protocol | Spec issue (SEP) | opened 2025-11-04; closed 2026-04-22 | https://github.com/modelcontextprotocol/modelcontextprotocol/issues/1763 | **111c** in listing; closed |
| S25 | [notes] Security IG - October 7, 2025 | Spec issue (official IG meeting notes) | 2025-10-07 | https://github.com/modelcontextprotocol/modelcontextprotocol/issues/1629 | 1c |
| S26 | [BUG] A changed MCP tool description never reaches a session that already loaded the tool, even after reconnect or --resume (deferred_tools_record is replayed) | anthropics/claude-code issue | 2026-09-26 | https://github.com/anthropics/claude-code/issues/97369 | 6c; open |
| S27 | [FEATURE] Tool result transform hook for content sanitization | anthropics/claude-code issue | 2026-01-16 | https://github.com/anthropics/claude-code/issues/18653 | **26c**; closed; `area:security` |
| S28 | Tool Pinning hashes only the description; the artifact layer moves on 74.6% of releases | snyk/agent-scan (formerly invariantlabs-ai/mcp-scan) issue | 2026-09-20 | https://github.com/snyk/agent-scan/issues/482 | 1c; open |
| S29 | Potential false positive in blender-mcp | snyk/agent-scan issue #2 | 2025-04-11 (opened) | https://github.com/snyk/agent-scan/issues/2 | 9c; closed |
| S30 | False positives for repository documentation read by default agent workflows | snyk/agent-scan issue | 2026-07-07 | https://github.com/snyk/agent-scan/issues/392 | 4c; open |
| S31 | Naming/supply-chain confusion affecting the Invariant mcp-scan you acquired | snyk/agent-scan issue | 2026-07-26 | https://github.com/snyk/agent-scan/issues/409 | 2c; closed |
| S32 | MCP tool calls execute without user approval when Auto-approve is OFF | cline/cline issue | 2026-05-01 | https://github.com/cline/cline/issues/10499 | 8c; open |
| S33 | Exfiltrate information from private repositories | github/github-mcp-server issue | 2025-08-08 | https://github.com/github/github-mcp-server/issues/844 | 9c; closed/stale |
| S34 | MCP Governance - Allow/Deny List for MCP for Organizations and Teams | github/github-mcp-server issue | 2025-09-04 | https://github.com/github/github-mcp-server/issues/1048 | 14c in listing; open/stale |
| S35 | Add an opt-in way to limit issue, comment and PR input from users without push access | github/github-mcp-server issue | 2025-05-23 | https://github.com/github/github-mcp-server/issues/427 | closed |
| S36 | Trust at first contact for MCP: adopt AID DNS record + key handshake (portable, decentralized, ongoing) | modelcontextprotocol/registry issue | 2025-09-10 | https://github.com/modelcontextprotocol/registry/issues/406 | 3c in listing; open |
| S37 | fix(mcp): disclose that Plan Mode read-only status is a server claim | google-gemini/gemini-cli PR | 2026-07-27 → closed 2026-08-11 | https://github.com/google-gemini/gemini-cli/pull/28549 | 6c; closed by stale bot |
| S38 | feat(plan): opt-in trust for MCP readOnlyHint via general.plan.trustReadOnlyHint | google-gemini/gemini-cli PR | 2026-05-16 → 2026-05-23 | https://github.com/google-gemini/gemini-cli/pull/27156 | 7c; closed |
| S39 | Where does validation of a peer's declarations belong? Four things the client accepts today | modelcontextprotocol/typescript-sdk issue | 2026-09-09 | https://github.com/modelcontextprotocol/typescript-sdk/issues/2777 | 1c; open |
| S40 | Tool Annotations as Risk Vocabulary: What Hints Can and Can't Do | Official MCP blog (O. Hungerford, S. Morrow, L. Chang) | 2026-03-16 | https://blog.modelcontextprotocol.io/ (repo file `blog/content/posts/2026-03-16-tool-annotations.md`; source PR https://github.com/modelcontextprotocol/modelcontextprotocol/pull/2230, 62c) | blog |
| S41 | SEP-2395: MCPS — Cryptographic Security Layer for MCP | Spec PR | 2026-03-13 → closed 2026-03-15 | https://github.com/modelcontextprotocol/modelcontextprotocol/pull/2395 | 10c; closed |

That is **41 distinct sources read.**

**Spec documents read from the clone** (used in section 5, not counted as practitioner sources):
- `docs/specification/2026-07-28/server/tools.mdx`
- `docs/docs/2026-07-28/tutorials/security/local-server-security.mdx`
- `docs/docs/2026-07-28/tutorials/security/security_best_practices.mdx`
- `docs/docs/2026-07-28/develop/clients/client-best-practices.mdx`
- SEP files `seps/2575-stateless-mcp.md`, `seps/2549-TTL-for-list-results.md`, `seps/2127-mcp-server-cards.md`, `seps/1024-...md`
- `docs/specification/2026-07-28/changelog.mdx`

**Listing-only items.** These titles were seen in GitHub search listings but the pages were not opened. They are used only as evidence that the topic exists:
- Spec #3004 "SEP-3004: Tamper-Evident Audit Record Contract" (56c, closed)
- #2828 "SEP: Server-Side Signed Execution Record for MCP Tool Calls" (43c, closed)
- #2787 "SEP-2787: Tool call attestation" (36c, closed)
- #2267 "SEP: MCP Server Identity and Tool Attestation" (closed)
- #2061 "SEP-2061: Action Security Metadata for MCP Tools" (closed draft)
- #1862 "SEP-1862: Tool Resolution" (27c, closed)
- #2636 "SEP-2636: Tool Manifests for Incremental Catalog Synchronization" (16c, closed)
- #2901 "Security Capabilities Declaration for MCP Servers — Feedback from 12 Production Servers" (7c)
- #3207 "MCP-2026-008: CacheableResult cacheScope:public enables cross-user cache poisoning" (open)
- #1932 "SEP-1932: DPoP Profile for MCP" (67c, open)
- #2817 "SEP-2817: AI Invocation Audit Context in Request _meta" (42c, open)
- registry PR #208 "feat: dns record verification" (28c, merged)
- registry PR #219 "feat: continuous verification job" (19c, closed draft)
- typescript-sdk #2868 "[v2] tools.listChanged defaults to true even when a server can never send the notification"

### 1b. Seen only as search-result snippets (NOT counted, NOT quoted)

These could not be opened because the domains were blocked or the search budget ran out:
- Simon Willison, "The lethal trifecta for AI agents" (2025-06-16): https://simonwillison.net/2025/Jun/16/the-lethal-trifecta/. It is cited and quoted by the official MCP blog (S40), so its framing enters via S40.
- Invariant Labs, "MCP Security Notification: Tool Poisoning Attacks": https://invariantlabs.ai/blog/mcp-security-notification-tool-poisoning-attacks
- Trail of Bits, "Jumping the line: How MCP servers can attack you before you ever use them" (2025-04-21): https://blog.trailofbits.com/2025/04/21/jumping-the-line-how-mcp-servers-can-attack-you-before-you-ever-use-them/
- The Hacker News, "Microsoft Warns Poisoned MCP Tool Descriptions Can Make AI Agents Leak Data" (2026-06): https://thehackernews.com/2026/06/microsoft-warns-poisoned-mcp-tool.html
- OWASP, "MCP Tool Poisoning": https://owasp.org/www-community/attacks/MCP_Tool_Poisoning
- OffSeq radar page that quotes an unidentified Reddit post about the "mcpwn" testing tool: https://radar.offseq.com/threat/are-mcp-servers-becoming-the-next-api-security-nig-21b1c46f. The subreddit and thread are UNVERIFIED.

**No HN thread IDs or Reddit thread URLs were obtained.** Any HN or Reddit evidence in the final paper must be gathered separately.

---

## 2. Thematic analysis

Counts are the number of distinct S-IDs (from section 1a) that raise the theme, either as a complaint or as a request.

### T1. "A tool definition can silently change after I approved it" (rug pull / drift), with demand for pinning, diffing and re-approval
**Count: 16.** Sources: S1, S2, S3, S5, S9, S10, S12, S14, S15, S16, S18, S19, S25, S26, S28, S41.

- "Detecting that the tool description changed between approval and reconnect is exactly the rug-pull case" (vaaraio, S14)
- "Definitions are not fixed at install time either: a server can quietly change them after you approved it (a rug pull), so a one-time consent dialog and package pinning do not cover this surface." This is the **official** guide (S9, `local-server-security.mdx`); it runs over 30 words but is exact and cited for its status.
- "Prefer clients that pin tool definitions… The protocol does not require this, so it is a property worth choosing a client for." (S9, official guide)
- "Capability drift is not addressed for parties without a live session" (taladari, S16, paraphrased by the fetcher). The dataset: **8% of hosts changed tool inventory between observations days apart, rising to 10.9% when descriptions and annotations are included.**
- "The server's behaviour changes immediately, but a long-lived session keeps obeying the _old_ description" (RaulPiresCoelho, S26). This is the inverse problem: client caching freezes definitions with no signal.
- "Digest pinning provides tamper evidence and integrity but NOT authenticity or non-repudiation." (ev3rl0ng, S1)
- Official Security IG notes say registry "fixed metadata… doesn't prevent 'rugpull' attacks, since servers can change behavior without changing metadata" (S25, summary).

Proposed solutions from practitioners:
- SHA-256 digest per tool version in `tools/list` with client pinning (S1).
- Ed25519-signed manifests (S14).
- JWS-signed manifests with content hash, version, and `list_changed` change semantics (S10).
- Signed tool definitions (S41, S3).
- A "signature" superset declaration that bounds future `list_changed` (S12).
- Hash on first trust, then re-approval on widening changes (S18, jagmarques).
- An ETag or capabilities revision for out-of-session checks (S16). A maintainer, SamMorrowDrums, says this is "already in the transports working group".
- A labeled baseline→twin drift corpus to test detectors (S2).

### T2. No provenance, signing or verifiable server identity
**Count: 13.** Sources: S3, S5, S6, S10, S12, S14, S16, S18, S19, S25, S36, S41, S9.

- "A host today takes a server's identity and its advertised `tools/list` on faith." (metereconsulting, S5)
- "Client may NEVER invoke `server/discover` to retrieve the server identity information." (Angelomirabella, S6)
- On registry namespace verification: "it proves who published the listing, not who runs the service the listing points at." (BerkantACUN, S16)
- "Today a one-off registry token proves control once and only to this registry." (nembal, S36)
- "A registry could sign or hash server metadata to alert clients when a server's state changes." (S25, IG notes)
- "Even if the current forks contain no malicious modifications, the infrastructure is in place." (CSCSoftware, S18, on mass fork-and-republish)

Proposed solutions:
- AID DNS record plus Ed25519 key handshake, with periodic re-verification (S36).
- Offline-signed admission assertion against a locally pinned trust root (S5).
- Identity carried in every server response (S6).
- A verified-publisher program (S18).
- Registry-level signing or hashing of metadata (S25).

### T3. Metadata is an injection surface beyond the top-level description: nested schema fields, server instructions, Unicode/bidi tricks, and approval-UI fidelity
**Count: 9.** Sources: S2, S9, S13, S14, S15, S16, S17, S27, S39.

- "100% of the prompt-injection payloads landed through _nested_ schema fields" (msaleme, S15, from tests of 10 production servers)
- "the client unconditionally trusts whatever text the server puts in `tool.description`" (Anwita17, S15)
- "The human in the loop is then approving a string that does not exist." (BerkantACUN, S39). The TS SDK accepts tool names containing zero-width and RTL-override characters, duplicate names, and 100,000-tool lists.
- "A malicious server can inject arbitrary instructions that are passed directly into the LLM's system prompt" (shunfeng8421, S13, on the `instructions` field)
- "Descriptions are the field to refuse to narrow, because that is the one tool poisoning uses." (Santoshkumarpuppala, S16)
- Encoding evasion: Base64, ROT13 and non-English text defeat keyword checks (Santoshkumarpuppala, S17, summary).

Proposed solutions:
- Replace server descriptions with locally pinned trusted strings (S15).
- Normalize descriptions schema-wide (S15).
- Cap and isolate `instructions` (S13).
- SDK-level rejection of control and bidi characters (S39).
- A hook that transforms results before they enter context (S27).

### T4. Server-supplied annotations and self-claims cannot be trusted, yet clients act on them
**Count: 8.** Sources: S4, S5, S8, S10, S37, S38, S39, S40.

- "Plan Mode should not trust unvalidated metadata from external MCP servers by default." (emersonbusson, S38). A review bot flagged the original auto-allow on `readOnlyHint` as a "security bypass".
- "The approval prompt is the control that catches this case, so it should carry the doubt." (cybrdude, S37). This came from a Google VRP report closed "Won't Fix (Infeasible)".
- "I'm not going to trust the implementation of malicious content detection of random MCP servers." (connor4312, VS Code, S4)
- "An untrusted server can lie. A server can claim `readOnlyHint: true` and delete your files anyway." (official MCP blog, S40)
- "no MCP client lets users filter tools by annotation values, and none surface annotations as context in approval prompts." (S40)
- "A few wording choices could inadvertently give implementers a false sense of security" (vinaybist, S8)

Proposed solutions:
- Trust and sensitivity annotations with session taint propagation (S4).
- Signed trust labels (S10).
- Opt-in trust settings that default off (S38).
- Disclaimers in approval prompts (S37).
- Graduated trust: enterprise internal servers versus random installs (S40).

### T5. Signed or unchanged does not mean safe; demand for runtime verification of declared versus observed behavior
**Count: 9.** Sources: S9, S10, S14, S21, S22, S25, S28, S15, S41.

- "a manifest can be signed, never tampered with, and still be malicious from the moment it was first published" (boy-hack, S14)
- "a signed manifest proves the description did not change, it does not prove what the tool actually did when called." (vaaraio, S14)
- "They do not, by themselves, constrain what the implementation does afterward." (Tetsurohhori, S10)
- "There's no way other than full trust, from scanning/building the binary, to fully protect against a malicious server." (PederHP, S9 review)
- "How can an MCP client verify what a server actually does at runtime" (dj2313, S22)
- "Alert on capability expansion — a newly reachable host, a newly read secret" (stillmarcus24, S28)

Proposed solutions:
- Sandbox the server, record filesystem, environment, network and process activity, and diff against declared behavior per version (S22).
- Alert on capability expansion instead of artifact hash (S28).
- Per-call signed execution records (S14 → SEP-2828).
- Sandbox enforcement demo (S10).
- Containers with seccomp, AppArmor or SELinux (S9 review, JAORMX).

### T6. Scanners are noisy, easy to evade, or easy to confuse; static snapshots are not enough
**Count: 9.** Sources: S11, S14, S17, S18, S28, S29, S30, S31, S22.

- The author of the S17 scanner self-reports **~65% detection with a 95% false-positive rate** on a held-out set: "it will produce false positives and it will miss real issues." (Ventrova, S17)
- "A scan at admission can't see the failure people actually get hit by." (Santoshkumarpuppala, S17)
- "Can `mcp-scan` differentiate between malicious and non-malicious prompt injection?" (christianboyle, S29)
- "it may produce a significant number of false positives that make it harder to identify real issues." (orassayag, S30)
- "Tool Pinning hashes the description string and nothing else." (stillmarcus24, S28, on mcp-scan/agent-scan). Using a plain artifact pin raises the alarm on 74.6% of releases.
- "diffing tool definitions between versions catches more real issues than static analysis of a single snapshot." (jagmarques, S18)
- Supply-chain irony: after Invariant unpublished the npm name `mcp-scan`, an unrelated package took it. It never called `tools/list` and missed a poisoned description (S31).

Proposed solutions:
- Report false-positive rates per check (S17).
- Re-scan on every version change (S17).
- Version-to-version diffing (S18).
- Flag and print the description for manual review instead of a verdict (S29).
- Suppression or allowlists for expected patterns (S30).
- Publish-time static or LLM review (S14, boy-hack).

### T7. Need policy, allowlists or permissions that do not come from the server's own description
**Count: 9.** Sources: S5, S15, S20, S21, S23, S24, S27, S34, S35.

- "there is no centralized, enterprise-level control to enforce which tools are approved for use." (ChrisMcKee1, S34)
- "There is no provision for e.g. "ACLs" on individual tools." (tysoekong, S21, paraphrased by the fetcher)
- "routing alone is not an authorization boundary." (maxmansonkiv, S20)
- "a prompt-injected model can "discover" a powerful tool just because the description sounds relevant" (tamish-max, S20)
- "enforce tool-level policies at the proxy layer before requests even reach the server" (tomjwxf, S15)
- "Interceptor enforcement must be at the transport layer" (sambhav, S24)

Proposed solutions:
- Org and team deny-by-default lists (S34).
- A JSON permission spec with parameter conditions (S21).
- Building on OPA, Cedar or AuthZEN (S21, davidjbrossard).
- OAuth-scope-based tool filtering (S23).
- Gateway or proxy filtering of `tools/list` (S20).
- A closed per-server tool allow-list after admission (S5).
- An interceptor framework (S24).
- Trusted-author content filtering (S35).

### T8. Lethal trifecta: exfiltration through tool combinations and untrusted content in tool results
**Count: 8.** Sources: S4, S5, S20, S21, S27, S33, S35, S40.

- "Prompt injection via public repository issues can result in LLM agents publishing information from private repositories" (sei-renae, S33)
- "The token with only permission to public repositories did read the private repositories" (sei-renae, S33)
- "It's data leaving through the client's other tools: web fetch, shell, email, images that load automatically." (bertiespell, S5)
- "A tool's risk depends on what else is in the session." (S40). The post also quotes a reader of Willison's newsletter asking for `reads_private_data / sees_untrusted_content / can_exfiltrate` metadata and runtime enforcement.
- "no hook can intercept and transform tool results before they enter Claude's context window" (evilfurryone, S27)

Proposed solutions:
- Session taint tracking and escalation (S4).
- Trifecta-aware policy engines (S40).
- Composed sensitivity labels, where "sensitivity should take the max of all sources" (aman210122, S21).
- Read-path sanitization in the GitHub MCP server (PRs #3035, #3039 and #3040 in listings).

### T9. Human-in-the-loop approval is weak in practice: auto-approve, buried details, and bugs
**Count: 6.** Sources: S32, S33, S37, S38, S39, S40.

- "realistically, users cannot be expected to click "See More" before clicking the much bigger "Continue" button" (sei-renae, S33)
- "Impact is high — write operations (posting PR comments, modifying work items, etc.) execute without user consent" (bgale12, S32, Cline bug)
- "Developers building autonomous agents treat confirmations as friction and lean on sandboxing instead." (S40)
- "In practice most clients still treat installation itself as the trust signal and don't distinguish further" (S40)

### T10. Local servers run with full user privileges, and supply-chain risk follows
**Count: 7.** Sources: S7, S9, S11, S18, S25, S28, S31.

- "I'm downloading and executing arbitrary code with my full user permissions." (DennisTraub, S7)
- "Users don't understand the difference between local execution and remote services." (DennisTraub, S7)
- "If a server does not require access to local resources then there is no good reason for it to be a stdio server" (PederHP, S9)
- "Pinning a package version with a launcher such as `npx` or `uvx` fixes only the top-level package" (S9, official guide)
- "MCP servers run with significant privileges (file access, network, tool execution)." (elliotllliu, S11)

### T11. Legitimate change is common, so naive hash pinning is noisy and change detection must be semantic
**Count: 6.** Sources: S12, S15, S16, S20, S28, S10.

- "Hash pinning only stayed stable on 4/10 servers because the tool definition legitimately changes per tenant" (msaleme, S15)
- "pin a capability fingerprint - the tool name, parameter names, and parameter types" (jagmarques, S15)
- In S16's corpus, only **0.38% of description changes were cosmetic** (Santoshkumarpuppala → taladari recomputation, S16). Practitioners disagree on how noisy description pinning is in practice.
- A full artifact pin alarms on **74.6%** of releases. A capability-expansion trigger alarms on 13.0% after adjudication, at 57.1% precision (S28).
- "A label is a claim the producer gets to write; a hash is not." (damoclais, S10). The commenter also asks for RFC 8785 canonicalization; the MCPS review (S41) shows Node and Python canonicalizing floats differently.
- Dynamic or per-user tool sets are legitimate. S12 separates "what is possible" from "what is currently available".

### T12. Tamper-evident audit and accountability
**Count: 5.** Sources: S5, S15, S21, S24, S14.

- "tamper-proof audit is named everywhere and specified nowhere." (scottrhodes, S5)
- Proposals: hash-chained admission logs (S5), signed audit receipts (S15), hash-chained logs (S21), observability interceptors (S24), and per-call execution records (S14). Listing-only items SEP-3004, SEP-2828 and SEP-2787 also cover this.

### T13. Too many tools and context bloat as a security amplifier
**Count: 3.** Sources: S20, S39, S9.

- "We already see latency with 70 tools, and high costs with the token bloat." (tzookb, S20)
- "Keep the roster small. Because all configured servers share the model's context, every server you add extends the surface the others are exposed to." (S9, official guide; tool shadowing rationale)

---

## 3. Disagreement and skepticism

1. **"Protocol-level checksums from an untrusted server are worthless; this is a client problem."**
   - nbarbettini (collaborator) on MCP-TLS: "I'm not clear on what threat this mitigates." He argued a server-supplied checksum adds nothing, and that clients can hash descriptions themselves (S19, summary).
   - Erfouni: "MCP deliberately does not prescribe how a host exposes tools to its model." (S20)
   - Agent-Hellboy asked why rules belong in the protocol rather than in infrastructure egress controls (S4).
   - This is the main argument why the spec still leaves pinning to clients.
2. **"Signing does not address malicious-from-day-one servers."** Raised by boy-hack, darklordVirtual and vaaraio (S14), Tetsurohhori (S10), and PederHP: "no way other than full trust" (S9). Supporters reply that signing is scoped narrowly to integrity, as one layer.
3. **Skepticism of bespoke crypto, and proposal quality.** localden on MCPS: "I am a bit skeptical of any bespoke/custom solutions that are not validated by the industry at large." He also flagged broken canonicalization, `schema_hash` that omits `description`, and suspected AI-generated content (S41). Many security discussions contain self-promotion or spam-hidden comments (S2, S14, S17, S18, S20, S21).
4. **Scanners as unreliable.** The S17 author self-reports a 95% false-positive rate. False-positive complaints appear in S29 and S30, and S28 argues mcp-scan's pinning covers the wrong field. Contrast S11, which wants scanners recommended in the spec; it was closed without a visible response.
5. **"The permission layer is mostly theater."** (blah-mad, S21). Also: "a call can be structurally valid and authorized, yet still be the wrong call for the user's intended effect." (darklordVirtual, S21)
6. **Hash pinning: brittle or fine?**
   - Brittle: 4/10 servers stable (S15) and a 74.6% artifact alarm rate (S28).
   - Fine: descriptions rarely change cosmetically, 0.38% (S16).
   - Middle position: a capability fingerprint (S15).
7. **Can annotations be useful if untrusted?** The question goes back to the original annotations PR, as recounted in S40. Justin Spahr-Summers: "I wonder how a client makes use of this flag knowing that it's _not_ trustable." VS Code's connor4312 rejects server-side malicious-content flags (S4). The `maliciousActivityHint` field was removed from SEP-1913.
8. **Two user camps.** Autonomy-focused developers see confirmations as friction, while enterprises want richer metadata and controls (S40). This explains why "just ask the user" is not accepted as a solution.

---

## 4. What practitioners say is MISSING (unmet needs, ranked by evidence count)

| Rank | Unmet need | Evidence (distinct sources) | Status today |
|---|---|---|---|
| 1 | **Standard detection of post-approval tool-definition change (rug pull)**, with client re-approval and a canonical per-tool digest or version | 16 (T1) | Not in spec. The official guide says "The protocol does not require this" (S9). SEP-1766, SEP-3140 and ETDI were closed; signed manifests (S14) are in discussion only. An ETag-style revision is "being worked on" in the transports WG (S16; no SEP number seen). |
| 2 | **Verifiable provenance and identity** for servers and tool definitions (signing, trust roots, ongoing ownership proof) | 13 (T2) | No signing in spec. Registry has DNS/GitHub namespace verification at publish time (registry PR #208 merged), but it "proves who published the listing, not who runs the service" (S16). ATSA (S5) is open without a sponsor. Server identity via `server/discover` is optional (S6). |
| 3 | **Runtime verification that behavior matches declared capabilities**, beyond integrity | 9 (T5) | Nothing in spec. Individual tools only (S22, S28). |
| 4 | **Robust handling of all metadata as untrusted input**: nested schema text, `instructions`, Unicode/bidi, approval-UI fidelity | 9 (T3) | Spec has no sanitization rules. TS SDK accepts bidi names and duplicates (S39). The `instructions` injection issue is open (S13). |
| 5 | **Detectors and scanners with acceptable false-positive rates**, plus shared labeled evaluation corpora | 9 (T6) | The community drift corpus PR was closed (S2). The self-reported scanner has a 95% false-positive rate (S17). Practitioners ask for per-check false-positive reporting and "tests that assert your scanner returns clean on payloads you know it misses" (S17). |
| 6 | **Description-independent policy and allowlists** (org-level, per-tool ACLs, gateways or interceptors) | 9 (T7) | Interceptors SEP-1763 closed. Permission-spec discussion closed. Implemented ad hoc in clients and vendors. |
| 7 | **Trustworthy risk metadata** (annotations a client can act on) | 8 (T4) | Spec: annotations MUST be treated as untrusted unless from trusted servers. SEP-1913 is still open. "No MCP client… surface[s] annotations as context in approval prompts" (S40). |
| 8 | **Session-level, trifecta-aware data-flow control** (taint tracking, exfiltration-channel limits) | 8 (T8) | SEP-1913 trust-annotations extension is in draft. |
| 9 | **Approval UX that actually works** (no auto-approve bugs, visible full details, warnings about server claims) | 6 (T9) | Spec has SHOULD-level guidance only. Client bugs persist (S32, S37). |
| 10 | **Low-noise, semantic change classification** (cosmetic versus capability-widening), with stable fingerprints across tenants and versions | 6 (T11) | No standard. Proposals: capability fingerprint (S15), capability expansion trigger (S28), content hash plus RFC 8785 (S10). |
| 11 | **Tamper-evident audit** of admission, approval and tool calls | 5 (T12) | Several audit SEPs closed (3004, 2828, 2787 in listings). SEP-2817 is open. |
| 12 | **Out-of-session and ecosystem-level drift monitoring** (registry or third parties) | 4 (S16, S25, S36, S12) | Registry continuous-verification PR #219 closed as a draft (listing). IG notes propose registry hashing (S25). |

**Notes for the user's proposal.** These are factual mappings, not recommendations.
- **Pinning and integrity (RQ1).** Ranks 1, 2 and 10 directly motivate a SHA-256 pinning and integrity layer. The S15, S16 and S28 numbers show that the *granularity* of what is hashed is a live, contested question. Options seen: description only (mcp-scan), full definition, capability fingerprint, or artifact.
- **Semantic drift (RQ2).** Rank 10, with S28's 74.6% versus 13% alarm rates and S15's per-tenant instability, is practitioner evidence that hash-only pinning produces alert fatigue. Practitioners want something that tells legitimate change from poisoned change.
- **False positives (RQ4).** Rank 5 (the 95% false-positive scanner, and false-positive complaints S29 and S30) supports making FPR a headline metric.
- **Labeled corpus.** S2 shows demand for a labeled baseline→twin drift corpus.
- **Not addressed by description analysis.** Rank 3 and T5 are the main criticism the proposal should pre-empt: a signed or unchanged but malicious-from-day-one server. The proposal's runtime monitor layer is the relevant answer.

---

## 5. Spec-level status (as of spec version 2026-07-28 and the draft in the repo on 2026-10-06)

| Topic | What the spec / official docs say | Source |
|---|---|---|
| **Tool annotations** | "For trust & safety and security, clients **MUST** consider tool annotations to be untrusted unless they come from trusted servers." This is present in spec versions 2025-03-26, 2025-06-18, 2025-11-25 and 2026-07-28. The annotations themselves are `readOnlyHint`, `destructiveHint`, `idempotentHint` and `openWorldHint`, all hints. | `docs/specification/2026-07-28/server/tools.mdx` lines ~302–306; https://modelcontextprotocol.io/specification/2026-07-28/server/tools ; S40 |
| **Human in the loop** | "there **SHOULD** always be a human in the loop with the ability to deny tool invocations." Applications SHOULD show which tools are exposed and give confirmation prompts. In Security Considerations, clients SHOULD "Show tool inputs to the user before calling the server, to avoid malicious or accidental data exfiltration", "Validate tool results before passing to LLM", and "Log tool usage for audit purposes". **Nothing requires showing full tool descriptions or detecting definition changes.** | same file, "User Interaction Model" and "Security Considerations" |
| **Change notification** | Servers that declare `listChanged` **SHOULD** send `notifications/tools/list_changed`. Since SEP-2575 (Final; spec 2026-07-28) this is delivered only to clients that opened `subscriptions/listen` with `toolsListChanged: true`, so it is opt-in. The notification carries **no diff, hash or version**; the client must re-fetch `tools/list`. Reviewer imran-siddique noted that after SEP-2575 a server can stay silent about a swap toward non-subscribed clients (S10). | `tools.mdx` "List Changed Notification"; `seps/2575-stateless-mcp.md` |
| **Caching / TTL** | SEP-2549 (Final) adds `ttlMs` and `cacheScope` to list results. Its Security Implications section calls the stale-cache risk "minimal". Issue #3207 (open, listing only) claims `cacheScope: public` enables cross-user cache poisoning. Client best-practices say to "treat a cached list as stale once a `list_changed` notification arrives". | `seps/2549-TTL-for-list-results.md`; `client-best-practices.mdx`; changelog 2026-07-28 item 5 |
| **Pinning tool definitions** | **Not required.** The official guide (merged 2026-10-05, S9) says: "Some clients record tool definitions when you first approve a server and ask again when they change. The protocol does not require this". It recommends "Treat Tool Definitions as Untrusted Input", reading tool lists via MCP Inspector, keeping the roster small, version pinning, and digest-pinned containers. | `docs/docs/2026-07-28/tutorials/security/local-server-security.mdx`; PR #3072 |
| **Tool poisoning in the Security Best Practices doc** | The main `security_best_practices.mdx` covers confused deputy, token passthrough, SSRF, state-handle hijacking, local server compromise, OAuth URL validation, mix-up, scope minimization and related topics. **It has no tool-poisoning or rug-pull section.** That coverage lives only in the newer local-server guide. | `docs/docs/2026-07-28/tutorials/security/security_best_practices.mdx` (section headings read) |
| **Signing / provenance of tool definitions** | **None in the spec.** Proposals closed: ETDI PR #649 (2025-09), SEP-2091 (2026-01), SEP-2267 (2026-02, listing), SEP-2395 MCPS (2026-03), SEP-1766 digest pinning (2026-06), SEP-3140 signed declarations (2026-09). Still open: SEP-2809 ATSA (no sponsor) and SEP-1913 trust annotations (draft, `roadmap/security`). | S1, S3, S5, S10, S12, S41, S4 |
| **Server identity / discovery** | `server/discover` exists but invoking it is optional. S6 calls this a regression; the issue was closed with no visible rationale. **Server Cards (SEP-2127, Final, extension)** deliberately exclude tools, resources and prompts "so clients cannot trust a static manifest for access-control or safety decisions". Cards are advisory, and no signing is mentioned. | `server/discover.mdx`; `seps/2127-mcp-server-cards.md` lines 147–150; S6 |
| **Registry verification** | The official registry verifies namespace ownership at publish time: GitHub OAuth/OIDC for `io.github.*`, and DNS/HTTP for domains (registry PR #208 merged 2025-08; PR #279 "auth: Add DNS auth" merged). There is no continuous verification (PR #219 closed as a draft) and no signing of tool metadata. S36 proposes AID DNS plus a key handshake (open, no response). | registry repo listings; S36; S16 |
| **Local install consent** | SEP-1024 (Final): clients must show the full command and get explicit consent before one-click local server installation. | `seps/1024-mcp-client-security-requirements-for-local-server-.md` |
| **Server `instructions` field** | Server-controlled text with no sanitization or length rules. A reported injection vector, MCP-2026-015, is open with no maintainer reply (S13). | S13 |
| **Auth** | OAuth 2.1-based authorization for HTTP transports, with PRM (RFC 9728) and CIMD. DPoP is SEP-1932, open, 67 comments in the listing. `tools/list` auth is not specifically addressed: "`tools/list` has no authentication guidance in the spec" (S16, summary); 37.8% of hosts require auth before listing. | spec `basic/authorization`; S16 |
| **Process** | New SEPs must come through a Working or Interest Group. A Tool Annotations Interest Group is forming (S40). Security IG notes exist (S25). An ETag/versioning idea is in the transports WG (S16, maintainer comment). **No accepted SEP addresses rug-pull detection as of 2026-10-06.** | S10, S40, S16 |

---

## 6. Gaps in this collection, for follow-up

- Reddit (r/mcp, r/ClaudeAI, r/LocalLLaMA, r/netsec, etc.), Hacker News, Stack Exchange, dev.to, Medium and simonwillison.net are **unverified**, because every one of those domains was blocked. Collecting them needs a session with those domains allowed, or manual collection by the user.
- The WebSearch budget ran out after about 6 queries in this agent; the 200-call limit is shared across all agents in the turn.
- Commercial client behaviour was not verified from primary sources: Cursor (forum blocked), Claude Desktop, and VS Code's handling of changed tool definitions.
