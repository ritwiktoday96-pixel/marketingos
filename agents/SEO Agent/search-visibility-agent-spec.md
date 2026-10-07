# Search Visibility Agent — Spec v1.0
*Marketing Agent OS · Agent 3 (redefined) · Drafted 3 Oct 2026 · Status: Draft for Ritwik's review*
*Companion files: `search-visibility-agent-system-prompt.md` · `search-playbook-v1.0.md`*

---

## BLUF

One agent that owns search visibility across the full content lifecycle — **before the brief, before publish, and after publish** — for classic Google/Bing search and AI answer surfaces (AI Overviews, AI Mode, Copilot, ChatGPT, Perplexity).

- **Replaces** Agent 3 (SEO Review) and **absorbs** Agent 5 (SEO Audit / Webpage Audit) from Architecture V2.0.
- **Five call modes**, each a separate API call with its own trigger and prompt module: `research` · `review` · `audit` · `monitor` · `calibrate`.
- **Diagnoses and recommends; never scores, gates, edits or publishes.** The Editor Agent stays the only scoring gate.
- **Self-learning is human-calibrated.** Every recommendation is logged, its outcome is measured at +28/+56 days, and a weekly report proposes rule changes to the versioned **Search Playbook**. Ritwik approves; the agent never edits its own Playbook.
- **v1 data**: Google Search Console (API + manual monthly CSV for the Generative AI report) + agent web-search sampling. No paid tools.

---

## 1. Why this shape (decisions)

### Decision 1 — Absorb Agents 3 + 5 into one identity, five call modes
All three jobs (pre-brief research, draft review, live-page audit) plus monitoring read the same Playbook and the same Page Registry. Splitting them into separate agents would fork the rules. Keeping one identity means one Playbook, one Learning Ledger, one calibration loop.

### Decision 2 — "One job per call" replaces "one job per agent" (amends hard constraint #7)
Architecture V2.0 constraint #7 says *no agent does two jobs*. Its rationale is isolation: a failure in one stage must not block another, and context must not bleed. This spec keeps that rationale by making **each mode a separate API call** with its own trigger, its own prompt module, and its own write-back fields — the same pattern as Decision 4 (Li Agent, one profile per call).
> **⚠ Needs Ritwik's sign-off**: this is a wording change to a locked system-wide constraint. Proposed new text: *"Separation of concerns: no API call does two jobs. Research, review, audit and monitoring are always separate calls, even when owned by one agent."*

### Decision 3 — Diagnose, don't score
The Editor already scores GEO/AEO (B1), E-E-A-T (B2), Search metadata (B3) and Website technical hygiene (W3). A second score from this agent would create two numbers for the same thing. So:

| | Search Visibility Agent | Editor Agent |
|---|---|---|
| Output | Findings + specific fixes, each tagged `must_fix` / `should_fix` / `consider` | 100-pt score, PASS/REVISE/FAIL, revision brief |
| Gate? | Never blocks anything | The machine gate |
| Relationship | Its `review` output is **evidence** the Editor reads when scoring B1/B3/W3 | Consumes SVA findings; does not re-derive them |

### Decision 4 — Runs before the Editor, after the Blog Agent
Pipeline order: Blog Agent → **SVA `review`** → Editor → Human gate. The Editor then scores a draft that already carries the SEO layer, same as the existing "Editor runs after SEO Review" decision.

### Decision 5 — Google's official position is the baseline; third-party GEO studies are directional
Google's [Optimizing for generative AI features](https://developers.google.com/search/docs/fundamentals/ai-optimization-guide) guide (published 15 May 2026, updated 10 Jul 2026) states AI Overviews and AI Mode are rooted in core Search ranking and quality systems, using RAG and query fan-out. It explicitly says llms.txt, content "chunking", AI-specific rewrites and special schema are **not** needed for Google. A July 2026 critical survey of 45 GEO studies ([arXiv 2607.14035](https://papers.cool/arxiv/2607.14035)) found topical relevance and context position are the most reproducible levers, generic heuristics transfer poorly, citation-oriented rewrites can hurt retrieval, and no technique shows a stable long-term cross-platform causal effect.
**Consequence**: the Playbook ranks evidence. Google first-party docs = `T1`. Peer-reviewed / large-sample studies = `T2`. Vendor studies = `T3`, directional only. No rule built on `T3` alone can ever produce a `must_fix`.

### Decision 6 — No page-per-fan-out-query, ever
Google's guide classifies creating separate content for every query variation or fan-out query, primarily to manipulate rankings or AI responses, as a violation of its scaled content abuse spam policy. `research` mode maps fan-out sub-questions so **one** page covers them — it never recommends spinning out thin pages per sub-question.

### Decision 7 — Measured vs. sampled AI visibility are labelled separately
- **Measured (Google only)**: Search Console's Generative AI performance report (launched 3 Jun 2026, data from 18 May 2026, worldwide since 31 Aug 2026). It gives **impressions only**, by page/country/device/date — no queries, no clicks, and AI Overviews + AI Mode combined, not split ([Google](https://developers.google.com/search/blog/2026/06/gen-ai-performance-reports); [Hartzer](https://hartzer.it.com/guides/what-ai-search-analytics-can-and-cannot-tell-you/)).
- **Sampled (everything else)**: agent web-search checks. **Directional only** — see §8 limitation L1.
Every AI-visibility statement in any output carries a `source:` tag (`gsc_genai` / `gsc_web` / `sample`) and a confidence label.

### Decision 8 — Monitor runs on the Claude API, not Routines
Per Architecture Decision 2, Routines blocks arbitrary external domains. `monitor` needs the GSC API and web search → Claude API via Mobi's orchestration. Only `calibrate` (reads/writes Notion only) is Routines-eligible.

---

## 2. Field summary

| Field | Detail |
|---|---|
| **Name** | Search Visibility Agent (SVA) — Agent 3 |
| **Replaces** | Agent 3 SEO Review Agent; Agent 5 SEO Audit Agent |
| **Deliverables served** | #1 Blog posts (pre-brief + pre-publish + post-publish), #7 Webpage Audit, website-format pages, any published URL in the Page Registry |
| **Modes** | `research`, `review`, `audit`, `monitor`, `calibrate` |
| **Volume (est.)** | research 12/mo · review 12–24/mo (incl. revision cycles) · audit 4/mo + 1 per new publish · monitor 1/week · calibrate 1/week |
| **Model** | Claude Sonnet (all modes); `calibrate` may use a stronger model — decide at build |
| **Tools** | Notion MCP, web search, web fetch, GSC Search Analytics API (via Mobi), optional PageSpeed Insights API (via Mobi — see §8 O2) |
| **Reads** | Brief, draft, Page Registry, Search Playbook (current approved version), KB (ICP, positioning, funnel stages), Content Templates (`Format Key`), Learning Ledger |
| **Writes** | Dedicated SVA fields on brief/draft pages; Page Registry; Health Snapshots; Refresh Queue; Learning Ledger; Calibration Report; Error Log |
| **Never** | Edits draft body or live page · publishes · scores/gates · edits the Playbook · invents a metric · recommends fan-out page farms or inauthentic mentions |
| **Human gate** | Accepts / rejects / modifies each recommendation with an override code; approves Playbook changes |
| **Learning loop** | Weekly `calibrate` → proposals → Ritwik approves → Playbook version bump |

---

## 3. Pipeline

```
              ┌──────────────── SEARCH PLAYBOOK vX.Y (human-approved rules) ────────────────┐
              │                                                                              │
BRIEF STAGE   │  Blog Calendar: status "Brief Requested"                                     │
              │        ↓ webhook                                                             │
              │  [SVA · research] → Search Landscape fields on brief → "Research Complete"  │
              │        ↓ human writes/approves brief → "Ready for Draft"                     │
              │        ↓ Blog Scheduler (Routine)                                            │
DRAFT STAGE   │  Blog Agent → "Draft Complete"                                               │
              │        ↓ webhook                                                             │
              │  [SVA · review] → SEO layer fields on draft → "Search Review Complete"      │
              │        ↓ webhook                                                             │
              │  Editor Agent (scores; reads SVA findings as evidence) → human gate → publish│
              │        ↓ human pastes live URL into Page Registry                            │
LIVE STAGE    │  [SVA · audit]  (publish +7 days, or manual for client URLs / Deliverable #7)│
              │        ↓                                                                      │
              │  [SVA · monitor] weekly → Health Snapshots → Refresh Queue (if triggered)   │
              │        ↓ human approves refresh → new brief → loop back to BRIEF STAGE       │
LEARNING      │  [SVA · calibrate] weekly → Calibration Report → Ritwik approves → Playbook++│
              └──────────────────────────────────────────────────────────────────────────────┘
```

---

## 4. Modes in detail

### 4.1 `research` — Search Landscape (pre-brief)
**Trigger**: Blog Calendar status → `Brief Requested`, or manual.
**Inputs**: topic, seed query, target ICP segment, funnel stage, candidate `Format Key`, Page Registry (for cannibalisation).
**Steps**
1. **Intent read** — what the seed query's searcher wants (informational / commercial / transactional / navigational); confirm funnel stage matches.
2. **SERP sample** — top results for the seed query and 3–5 close variants: who ranks, what format, what they cover, what they all repeat (= commodity baseline).
3. **Fan-out map** — the 8–15 sub-questions an AI system is likely to fan out to (per Google's own fan-out example pattern). Marked `cover_in_page` / `link_to_existing` / `out_of_scope`. **Never** `new_page`.
4. **Information-gain angle** — what Reachify/client can say that the commodity baseline can't: first-party data, named client cases, operator experience (maps to the Thought Leadership evidence tiers 1–3). If none exists in KB, say so — that is a finding, not a gap to paper over.
5. **Cannibalisation check** — any existing Page Registry URL targeting the same cluster → recommend `merge` / `differentiate` / `refresh_existing_instead`.
6. **Internal link plan** — 3–5 existing URLs to link from/to.

**Output fields (on brief)**: `sva_intent`, `sva_fanout_map`, `sva_commodity_baseline`, `sva_information_gain`, `sva_cannibalisation`, `sva_internal_links`, `sva_recommended_format_key`, `sva_research_sources`, `sva_research_confidence`.
**No search volume / keyword difficulty numbers** — v1 has no keyword tool (§8 L2).

### 4.2 `review` — SEO layer (pre-publish; replaces old Agent 3)
**Trigger**: draft status → `Draft Complete` (and again on each Editor revision cycle).
**Inputs**: draft, brief incl. `research` fields, Playbook, `Format Key` template.
**Checks** (each → finding with severity + exact fix):
1. **Fan-out coverage** — each `cover_in_page` sub-question from `research`: answered / thin / missing.
2. **Extractability** — clear headings, a direct answer near the top of each section, claims stated plainly enough to be lifted with their source. Framed as reader clarity, not "AI chunking" (Google says chunking isn't required).
3. **Non-commodity check** — does the draft deliver the `sva_information_gain` angle, or has it regressed to the commodity baseline?
4. **Freshness hygiene** — any stat older than the Playbook's staleness threshold; any undated stat; "this year"-style relative dates.
5. **Title tag + meta description** — 2 options each, Playbook length rules.
6. **Internal links** — placements for the planned links; anchor text.
7. **Structured data recommendation** — which schema type fits (`Article`, `FAQPage` where an FAQ block exists, etc.). Note in output: FAQPage no longer earns a Google rich result (standing rule #12) and no special schema is needed for Google AI features; recommend only for general SEO eligibility.
8. **Cannibalisation re-check** against the final title/H1.

**Must not flag**: missing author byline/credentials or missing finished visuals (standing rule #13 — CMS/publish-stage additions).
**Output fields (on draft)**: `sva_review_findings` (JSON list), `sva_title_options`, `sva_meta_options`, `sva_schema_recommendation`, `sva_internal_link_placements`, `sva_must_fix_count`, `sva_review_version`, `sva_playbook_version`.

### 4.3 `audit` — Live page (absorbs old Agent 5)
**Trigger**: (a) publish +7 days for every new Page Registry URL; (b) manual for client URLs (Deliverable #7, 4/month).
**Checks**
1. **Indexability** — status code, `noindex`, canonical target, robots.txt block, whether the URL shows in GSC (own properties only).
2. **Rendered metadata** — live title/meta vs. what `review` recommended.
3. **Structured data present & parseable** — JSON-LD found in HTML; type matches recommendation. (Full validation = Rich Results Test, manual link in output.)
4. **Content parity** — live page still matches the approved draft (catches CMS truncation, missing sections, broken internal links).
5. **Performance** — Core Web Vitals via PageSpeed Insights API if Mobi wires it (§8 O2); otherwise listed as a manual check with a link.
6. **Gen-AI eligibility** — manual checklist item: confirm the property is *included* in Search generative AI features in GSC (Google states a site must be included to be eligible). The agent cannot read this toggle; it asks the human to confirm once per property.

**Output**: Audit report page → page-by-page findings, priority issues, recommended fixes (same format promised by old Agent 5). For own pages, also writes `audit_status` to Page Registry.

### 4.4 `monitor` — Post-publish health (weekly)
**Trigger**: weekly (Mobi's scheduler), Mondays.
**Inputs**: Page Registry (all `Live` URLs on GSC-verified properties), GSC Search Analytics API, latest manual Gen-AI CSV, web search.
**Steps**
1. **Pull GSC** per URL: clicks, impressions, CTR, average position, top queries — last 28 complete days vs. prior 28 days, and vs. publish baseline.
2. **Read Gen-AI impressions** per URL from the latest monthly CSV (manual — see §8 L3).
3. **Sample** — for each URL's top 3 GSC queries: is the page in the visible results; who displaced it; has the SERP shape changed (new formats, new competitor types).
4. **Content-age scan** — stats/claims past the staleness threshold; `last_substantive_update` age.
5. **Classify** each URL using the Playbook decay rules → `healthy` / `watch` / `decaying` / `refresh_now` / `cannibalising` / `insufficient_data`.
6. **Diagnose** — which signal fired and the most likely cause (ranking loss vs. CTR loss with stable impressions vs. AI-surface shift vs. content staleness vs. cannibalisation). Diagnoses are hypotheses, stated as such.
7. **Refresh brief** for `refresh_now` URLs → Refresh Queue (what to update, why, evidence). **Refresh = substantive update.** Never recommend date-only bumps — they're cosmetic and add nothing.

**Output**: one Health Snapshot row per URL per week; Refresh Queue entries; a short weekly digest page.

### 4.5 `calibrate` — Learning (weekly)
See §6.

---

## 5. Notion schema (new / changed)

| Table / fields | Purpose | Written by | Read by |
|---|---|---|---|
| **Page Registry** (new) — URL, Title, Format Key, Property (own/client), Publish date, Last substantive update, Target cluster, Primary queries, Status (Live/Redirected/Retired), Health, Next review, Baseline (clicks/impr/pos at +28d), Audit status | Spine for audit + monitor | Human (URL on publish), SVA | SVA, Analytics Agent |
| **Health Snapshots** (new) — URL (relation), Week, Clicks, Impr, CTR, Avg pos, Gen-AI impr, Δ vs prior, Health, Signals fired, Diagnosis, Source tags | Weekly time series | SVA `monitor` | SVA, human |
| **Refresh Queue** (new) — URL, Trigger rule, Evidence, Refresh brief, Priority, Human decision, Override code, Refreshed on | Turns decay into action | SVA, human | Human, Blog Calendar |
| **SVA Learning Ledger** (new) — Rec ID, Mode, Rule ID, Playbook version, URL/draft, Recommendation, Severity, Human decision (accept/reject/modify), Override code, Outcome +28d, Outcome +56d, Outcome verdict | Raw material for learning | SVA, human, SVA `monitor` (outcomes) | SVA `calibrate` |
| **SVA Calibration Report** (new) — Week, Rule stats, Proposals, Search-landscape changes, Approval status | Weekly learning output | SVA `calibrate` | Ritwik |
| **Search Playbook** (new page, versioned) | The rules | Ritwik only (on approval) | SVA all modes |
| **Gen-AI Report Drops** (new) — Month, CSV file, Property, Uploaded by | Manual data input | Human | SVA `monitor` |
| Blog Calendar briefs — 9 `sva_*` research fields (§4.1) | `research` output | SVA | Human, Blog Agent |
| Blog Drafts — 8 `sva_*` review fields (§4.2) | `review` output | SVA | Editor, human |

**Override codes** (same set as the Editor, for one learning vocabulary across the OS): `agree` · `false_flag` · `missed_issue` · `wrong_priority`.

---

## 6. Self-learning loop (human-calibrated)

**What "learning" means here**: the agent gets better at *which recommendations to make and how hard to push them*, measured against two signals — what the human accepted, and what actually happened to the page afterwards.

**Weekly `calibrate` run**
1. **Rule scorecard** — per Playbook rule: times fired, acceptance rate, override-code mix, outcome where measurable.
2. **Outcome check** — for refreshes and accepted `review` fixes now at +28/+56 days: GSC delta vs. the page's own prior trend **and** vs. a comparison group of similar unrefreshed pages (same Format Key, similar age). Without a comparison group, an "improvement" may just be seasonality or a core update.
3. **Landscape watch** — scan Google Search Central blog/docs updates, Search Console changes, Bing Webmaster blog, and new `T1`/`T2` research since last run. Flag anything that contradicts a current Playbook rule (e.g. the 7 May 2026 FAQ rich-result removal type of change).
4. **Proposals** — each one: rule ID, proposed change, evidence, evidence tier, expected effect, risk. Types: `tighten_threshold` / `loosen_threshold` / `change_severity` / `retire_rule` / `new_rule` / `fact_update`.
5. **Ritwik approves / rejects** each proposal in Notion → approved changes become Playbook vX.Y+1 with a changelog line.

**Guardrails on learning**
- **Minimum evidence before proposing**: a rule needs ≥10 fires *or* ≥5 measured outcomes before a threshold change is proposed (start values — calibrate later).
- **Correlation language only**: outcomes are reported as "associated with", never "caused". The GEO survey and the freshness studies themselves are correlational.
- **No rule auto-promotes to `must_fix`** without at least one `T1` or `T2` source.
- **Retire before you add**: if a rule's acceptance rate is < 30% over 4 weeks, propose retiring or downgrading it before proposing new rules.

---

## 7. Hard constraints

1. Never edits a draft body, brief body, or live page. Writes only to its own fields/tables.
2. Never publishes, never triggers a publish.
3. Never scores or gates. The Editor is the only scoring gate.
4. Never edits the Search Playbook. Proposes only.
5. **No fabricated metrics.** Every number traces to a GSC API row, a dated CSV drop, or a cited source URL. No estimated search volume, traffic, or "AI citation share" numbers.
6. Every AI-visibility claim carries a `source:` tag and confidence label (Decision 7).
7. Never recommends one page per fan-out query, doorway/variant pages, or inauthentic mention-seeking (Google spam policies).
8. Never recommends date-only "refreshes".
9. Never flags missing byline/credentials or finished visuals (standing rule #13).
10. One mode per API call. A failed run of one mode never blocks or overwrites another mode's output.
11. GSC data only for properties the client has verified and granted access to.
12. Every failure → Notion Error Log (timestamp, mode, URL/draft, error type).

---

## 8. Limitations, options, open items

**Limitations (accepted for v1 — know them before relying on the output)**
- **L1 — Web-search sampling cannot see AI answers.** The agent's web search returns ranked pages, not the text of an AI Overview, AI Mode, ChatGPT or Perplexity answer. It can confirm SERP presence and who outranks you; it cannot confirm you were *cited* in an AI answer. All `sample` AI-visibility signals are therefore proxies. Treat as directional.
- **L2 — No keyword volume or difficulty.** GSC only reports queries a page already appears for. `research` gives intent, coverage and gap analysis — not volume numbers.
- **L3 — Gen-AI report is manual.** As of the latest information found, Google hasn't exposed this report through the Search Analytics API — only via CSV export in the UI ([Fivetran support thread](https://support.fivetran.com/hc/en-us/community/posts/42165801610135-Google-Search-Console-Generative-AI-performance-reports?page=1); secondary source, re-check before build). v1 = monthly CSV dropped into Notion by a human, same as Analytics Agent Phase 1.
- **L4 — Gen-AI impressions ≠ citations ≠ clicks.** The report counts impressions only, with AI Overviews and AI Mode combined. Clicks from AI features are counted inside the normal Web search type, not separable.
- **L5 — Google-only measurement.** Nothing in v1 measures ChatGPT, Perplexity or Copilot citations.

**Options worth considering (not in your v1 selection — free, flagged for a decision)**
- **O1 — Bing Webmaster Tools AI Performance report.** Free. Public preview since Feb 2026. Reports citations across Microsoft Copilot, Bing AI summaries and select partner integrations, with "grounding queries" (the retrieval queries the AI used) and citation share per query ([Practical Ecommerce](https://www.practicalecommerce.com/?p=1564581)). This is the only *measured* citation data available for free, and it covers L5 partly. Setup imports sites from GSC. Recommend adding as a second manual CSV input — API availability unverified.
- **O2 — PageSpeed Insights API** for `audit` Core Web Vitals. Free Google API; Mobi wires it as a deterministic tool.
- **O3 — v1.1 AI-answer probe.** Mobi calls engines that return citations via their own APIs for a fixed prompt set per cluster, logging cited URLs over time. Low cost, but still sampling (answers vary run to run), and needs its own design. Park until v1 baselines exist.

**Open items**
1. **Constraint #7 wording change** (Decision 2) — Ritwik to approve.
2. **Architecture V2.0 update** — roster: Agent 3 renamed and redefined, Agent 5 retired into SVA `audit`; Blog pipeline diagram and Part 6 schema need the new tables.
3. **Editor dependency** — Editor's trigger currently fires "after SEO Review". Update to fire on `Search Review Complete`.
4. **Tension to watch** — templates (TOFU/MOFU) instruct 40–60-word answer-first blocks and standing rule #12 leans on the ~81% FAQ-citation figure. Google says no special formatting or chunking is needed for its AI features, and the GEO survey says generic heuristics transfer poorly. These blocks are still good for readers, so no change now — but the Playbook tags them `T3 / reader-clarity`, not `must_fix`, and `calibrate` should test them against outcomes.
5. **Client properties** — GSC access model for client sites (service account vs. user grant) — Mobi.

---

## 9. Build sequence

| Step | What | Owner | Unblocks |
|---|---|---|---|
| 1 | Approve this spec + constraint #7 change + O1/O2 decision | Ritwik | Everything |
| 2 | Create Page Registry, Health Snapshots, Refresh Queue, Learning Ledger, Calibration Report, Gen-AI Report Drops; Search Playbook page (v1.0) | Ritwik | 3–6 |
| 3 | Add the 9 research `sva_*` fields to Blog Calendar and the 8 review `sva_*` fields to Blog Drafts | Ritwik | 4 |
| 4 | Ship `review` first (closes the blog pipeline — highest volume, replaces an already-planned P2 agent) | Mobi + Ritwik (prompt) | Editor trigger |
| 5 | Backfill Page Registry with existing live URLs; GSC API wiring; first manual Gen-AI CSV | Ritwik + Mobi | 6 |
| 6 | `monitor` in shadow mode — 4 weeks, outputs reviewed, no Refresh Queue actions taken | Mobi | thresholds |
| 7 | `audit` (own pages at publish +7d, then client URLs) | Mobi | Deliverable #7 |
| 8 | `research` | Mobi + Ritwik | Brief quality |
| 9 | `calibrate` — first run after ≥4 weeks of Ledger data | Mobi (Routine) | Learning loop |

---

## Sources
- [Google — Optimizing your website for generative AI features on Google Search](https://developers.google.com/search/docs/fundamentals/ai-optimization-guide) (T1)
- [Google — Introducing Search Generative AI performance reports in Search Console, 3 Jun 2026](https://developers.google.com/search/blog/2026/06/gen-ai-performance-reports) (T1)
- [Hartzer — What AI search analytics can and cannot tell you](https://hartzer.it.com/guides/what-ai-search-analytics-can-and-cannot-tell-you/) (report limits)
- [Let's Data Science — GSC AI reports worldwide, 31 Aug 2026](https://letsdatascience.com/news/google-search-console-extends-ai-reports-worldwide-0dcbac29)
- [Fivetran support — Gen-AI report not in Search Analytics API](https://support.fivetran.com/hc/en-us/community/posts/42165801610135-Google-Search-Console-Generative-AI-performance-reports?page=1) (secondary)
- [Practical Ecommerce — Bing AI Performance report](https://www.practicalecommerce.com/?p=1564581)
- [Optimizing Visibility in Generative Engines: A Critical Survey of GEO (2023–2026), arXiv 2607.14035](https://papers.cool/arxiv/2607.14035) (T2)
- [Ahrefs — AI assistants prefer to cite fresher content (17M citations)](https://ahrefs.com/blog/do-ai-assistants-prefer-to-cite-fresh-content/) (T3)
