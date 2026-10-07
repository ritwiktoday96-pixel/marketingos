# Search Playbook — v1.0
*Rule set for the Search Visibility Agent (SVA) · 3 Oct 2026 · Owner: Ritwik · The agent reads this; it never edits it.*

---

## 0. How to read this

- **Rule ID** — stable; the Learning Ledger tracks every fire against it.
- **Evidence tier** — `T1` Google/Bing first-party documentation · `T2` peer-reviewed or large-sample, method-disclosed research · `T3` vendor/practitioner study or convention, directional.
- **Max severity** — the highest severity the rule may produce. **A rule with only `T3` evidence can never produce `must_fix`.**
- **Thresholds marked ⚙ are start values, uncalibrated.** `calibrate` proposes changes once the evidence minimums in spec §6 are met.

Severity: `must_fix` (Editor should treat as blocking evidence) · `should_fix` · `consider`.

---

## 1. Research rules (`research`)

| ID | Rule | Tier | Max sev. |
|---|---|---|---|
| R1 | Fan-out sub-questions map to `cover_in_page`, `link_to_existing` or `out_of_scope` — never `new_page`. Separate pages per query variation/fan-out query to manipulate rankings or AI responses = scaled content abuse. | T1 | must_fix |
| R2 | State the information-gain angle (Tier 1–3 evidence: first-party data, named client case, operator experience). If KB has none, report `no_information_gain_available` — do not invent one. | T1 (Google: "non-commodity content") | must_fix |
| R3 | If an existing Registry URL targets the same cluster, recommend `merge` / `differentiate` / `refresh_existing_instead` before a new page. | T3 | should_fix |
| R4 | No search volume, keyword difficulty or traffic estimates (no source in v1). | — (constraint) | — |

## 2. Review rules (`review`)

| ID | Rule | Tier | Max sev. |
|---|---|---|---|
| V1 | Every `cover_in_page` fan-out sub-question is answered substantively. `missing` → finding; `thin` → finding. | T1 (fan-out mechanism) | must_fix if the **primary** question is missing; else should_fix |
| V2 | Extractability for readers: descriptive headings; a direct answer near the top of each section; claims stated with their source in the same sentence/paragraph. Frame as clarity, not "AI chunking". | T1 (headings/organisation) + T3 (answer-first) | should_fix |
| V3 | Draft delivers the brief's `sva_information_gain` angle. Draft that only restates the commodity baseline → finding. | T1 | must_fix |
| V4 | Stale stats ⚙: any statistic dated > 24 months, or > 12 months for fast-moving topics (AI, pricing, platform features, regulation). Undated stat → finding. | T3 (freshness studies) | should_fix |
| V5 | No relative time phrases ("this year", "recently", "last month") without an absolute date. | T3 | should_fix |
| V6 | Title tag: 2 options, primary topic early, ⚙ ~50–60 characters to limit truncation. Meta description: 2 options, ⚙ ~140–160 characters. (Google sets no hard limit — convention only.) | T3 | consider |
| V7 | Internal links ⚙ 3–5 contextual links to/from Registry URLs, descriptive anchor text. | T3 | consider |
| V8 | Schema: recommend the type that fits the Format Key. State that no special schema is needed for Google AI features and that FAQPage no longer earns a Google rich result (removed 7 May 2026). | T1 | consider |
| V9 | Title/H1 must not collide with an existing Registry URL's primary cluster. | T3 | should_fix |
| V10 | Do **not** flag missing byline/credentials or finished visuals (standing rule #13). | — (constraint) | — |

## 3. Audit rules (`audit`)

| ID | Rule | Tier | Max sev. |
|---|---|---|---|
| A1 | Page returns 200, is not `noindex`, canonical points to itself (or the intended URL), not blocked by robots.txt. A page must be indexed and snippet-eligible to appear in Google's AI features. | T1 | must_fix |
| A2 | Live title/meta match the approved `review` choice (or a deliberate human edit). | T3 | should_fix |
| A3 | Content parity with the approved draft — no missing sections, broken internal links, truncated FAQ/schema. | T3 | must_fix (missing sections / broken links) |
| A4 | Core Web Vitals: LCP ≤ 2.5 s, INP ≤ 200 ms, CLS ≤ 0.1 (matches `landing_page` template). Only if PSI API is wired; else manual check. | T1 | should_fix |
| A5 | Human has confirmed the property is **included** in Search generative AI features in Search Console (once per property). | T1 | must_fix until confirmed |
| A6 | Recommended JSON-LD present and of the right type; link to Rich Results Test for full validation. | T1 | consider |

## 4. Monitor rules (`monitor`)

All comparisons: **last 28 complete days vs. prior 28 complete days** unless stated. Exclude incomplete recent days (GSC data lags).

| ID | Signal | Threshold ⚙ | Tier | Health effect |
|---|---|---|---|---|
| M0 | Minimum data | < 100 impressions in 28 days → `insufficient_data`; no other rule fires | — | gate |
| M1 | Ranking loss | Avg position on top-3 queries worsens ≥ 3 places → `watch`; ≥ 5 places → `decaying` | T1 (GSC metric) | watch / decaying |
| M2 | CTR loss, stable demand | Impressions within ±15% **and** clicks −25% or worse → `watch`; diagnose as possible SERP/AI-surface intercept (hypothesis) | T1 metric / T3 interpretation | watch |
| M3 | Visibility loss | Impressions −30% **and** clicks −30% or worse → `decaying` | T1 metric | decaying |
| M4 | Gen-AI impressions drop | Month-over-month Gen-AI impressions −40% or worse, with ≥ 50 Gen-AI impressions in the prior month → `watch` | T1 metric | watch |
| M5 | Content age | `last_substantive_update` > 180 days (MOFU/BOFU/commercial) or > 365 days (TOFU/evergreen) → `watch` | T3 (freshness studies) | watch |
| M6 | Cannibalisation | Two Registry URLs share ≥ 3 of their top-5 GSC queries **and** swap position on them in the window → `cannibalising` | T3 | cannibalising |
| M7 | Escalation | `decaying` for 2 consecutive weeks, **or** `decaying` + M5 → `refresh_now` → Refresh Queue | — | refresh_now |
| M8 | Refresh = substantive | Refresh briefs must change content (new data, new section, fixed fan-out gap, updated claims). Date-only bumps never recommended. | T3 | constraint |

**Diagnosis vocabulary** (pick one primary, label as hypothesis): `ranking_loss` · `ctr_intercept` · `demand_drop` · `ai_surface_shift` · `content_staleness` · `cannibalisation` · `technical` · `unknown`.

## 5. AI-visibility source labels (all modes)

| Tag | Means | Confidence |
|---|---|---|
| `source:gsc_web` | GSC Search Analytics API (clicks incl. clicks from AI features, impressions, position) | Measured |
| `source:gsc_genai` | GSC Generative AI report CSV — impressions only, AI Overviews + AI Mode combined, Google only | Measured, narrow |
| `source:bing_ai` | Bing Webmaster AI Performance CSV (only if option O1 approved) | Measured, Microsoft surfaces only |
| `source:sample` | Agent web-search check — ranked pages, **not** AI answer text | Directional |

## 6. Evidence register

| Claim used in rules | Source | Tier |
|---|---|---|
| AI Overviews/AI Mode use core Search ranking + RAG + query fan-out; llms.txt, chunking, AI rewrites, special schema not needed; fan-out page farms = scaled content abuse; must be indexed + snippet-eligible + included in gen-AI features | [Google AI optimization guide](https://developers.google.com/search/docs/fundamentals/ai-optimization-guide) | T1 |
| Gen-AI report: impressions only, page/country/device/date, data from 18 May 2026 | [Google Search Central blog, 3 Jun 2026](https://developers.google.com/search/blog/2026/06/gen-ai-performance-reports) | T1 |
| Relevance + context position most reproducible; generic heuristics transfer poorly; citation-oriented rewrites can hurt retrieval | [GEO critical survey, arXiv 2607.14035](https://papers.cool/arxiv/2607.14035) | T2 |
| AI-cited URLs average 1,064 days old vs 1,432 for organic (25.7% fresher); AI Overviews skew slightly older than organic | [Ahrefs, 17M citations](https://ahrefs.com/blog/do-ai-assistants-prefer-to-cite-fresh-content/) | T3 |

---

## Changelog
- **v1.0 — 3 Oct 2026** — Initial rule set. All ⚙ thresholds uncalibrated; first `calibrate` proposals expected after ≥ 4 weeks of Ledger data.
