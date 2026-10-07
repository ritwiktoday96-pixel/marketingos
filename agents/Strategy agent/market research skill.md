---
name: market-research
description: Strategy Agent skill (Research). Researches industry sources against a client's requirement and recommends the best course of action — organic and paid campaign plans, emailers, offers, and competitors/pages to watch. Use when the user shares a client brief or asks "what should we do for <client/goal>".
---

# Research → Recommended Course of Action

**Input:** client requirement/brief. **Output:** research summary + recommended plan
(organic, paid, email, offer) + watchlist, each recommendation tied to evidence.

## Step 1 — Required inputs (ask if missing; max 5 questions)
1. Client, offer, price point (₹), business model (B2B/B2C/D2C/service)
2. Goal + timeframe (leads, sales, awareness, launch) and target number
3. Budget (₹/month) split appetite: organic only / paid / both
4. ICP + geography (city tier, language)
5. Current assets & data: site, socials, email list size, past campaign results, CRM

## Step 2 — Research (live; source + date for each finding)
| Layer | Sources |
|---|---|
| Market & demand | Google Trends (relative interest 0–100, seasonality, regional; free; weak for niche B2B), Answer the Public (question clusters), Google autocomplete/PAA, industry reports, news |
| Audience voice | Reddit, Quora, YouTube comments, reviews (G2/Trustpilot/Google/app stores), community groups — capture exact phrases, pains, objections |
| Competitors | names + positioning; for depth hand to `competitor-analysis` |
| Ads landscape | Meta Ad Library, Google Ads Transparency Center, LinkedIn Ad Library, TikTok Creative Center (if market allows) — angles, offers, formats |
| Platform rules | Current official docs for any channel you recommend (Meta, Google, LinkedIn) |
| Regulation | ASCI Code; DPDP Act/Rules 2025; sector regulators (SEBI/RBI/IRDAI for finance; health claims for wellness) |

Workflow: Trends to confirm a topic is worth pursuing/timing → ATP/PAA/Reddit to decide
what exactly to say.

## Step 3 — Diagnose
- Stage of awareness of the ICP (unaware → most aware) and buying cycle length.
- **95-5 lens (LinkedIn B2B Institute + Ehrenberg-Bass):** in B2B, ~5% of buyers are
  in-market at a time. Recommend brand/mental-availability work for the 95% alongside
  demand capture for the 5%. Adjust for B2C impulse categories.
- Channel–ICP fit; budget sufficiency (paid needs enough conversions for algorithms to
  learn — Google suggests ≥ 15 conversions/month per PMax campaign for tROAS).

## Step 4 — Recommendations

### A. Organic plan
Content pillars (3–5), formats per channel, cadence, TOFU/MOFU/BOFU mix, SEO targets,
community plays, partnerships/collabs. 30-60-90 day roadmap.

### B. Paid plan (only if budget)
- **Channel choice + rationale** (Google Search for demand capture; Meta for D2C/B2C demand
  creation; LinkedIn for B2B role targeting).
- **Google:** fewer, larger campaigns; PMax / AI Max for Search with broad match + Smart
  Bidding once conversion tracking is clean; set tROAS on ≥ 30 days or 3 conversion cycles of
  data; manage negatives/search terms.
- **Meta (Andromeda era):** consolidated structure — roughly one campaign per objective per
  offer, broad targeting, Advantage+ defaults; creative diversity is the targeting lever
  (distinct concepts: testimonial, demo, problem/solution, founder, UGC — not near-duplicates);
  refresh creative regularly. Treat practitioner-reported ranges (e.g. 10–50 ads, refresh every
  7–14 days) as starting points, not rules.
- **LinkedIn:** document ads/lead gen forms for gated MOFU assets; thought-leader ads for
  brand.
- Budget split in ₹, test plan, KPIs, kill/scale rules.

### C. Emailers
Sequence type (welcome, nurture, launch, re-engagement, win-back), # of emails, timing,
subject-line angles, one CTA each. Compliance: Gmail/Yahoo bulk senders (≥ 5,000/day) need
SPF+DKIM+DMARC, RFC 8058 one-click unsubscribe, opt-outs honoured within 2 days, spam rate
< 0.3% (aim < 0.1%). DPDP: explicit, purpose-specific, withdrawable consent (binding
13 May 2027 — design for it now). Benchmarks (MailerLite 2025) only as context.

### D. Offers
Use the value equation (Hormozi): Value = (Dream outcome × Perceived likelihood) ÷
(Time delay × Effort & sacrifice). Propose 2–3 offers (lead magnet, entry offer, core
offer) with ₹ pricing logic, guarantee/risk reversal (compliant for segment), bonuses, urgency
that is real (no fake scarcity — ASCI).

### E. Watchlist
Competitors, specific pages (pricing, comparison, top blog posts), ad accounts, creators,
communities, keywords/trends to re-check — with frequency and trigger.

## Step 5 — Output structure
1. BLUF (3–5 lines: recommended course of action + why)
2. Key findings (5–8, each with source)
3. Recommended plan A–E (only sections relevant to brief)
4. 30-60-90 roadmap table: week | action | owner | KPI
5. Budget table (₹) if paid
6. Risks & assumptions; compliance flags
7. Sources, Open items, Next skill

## Rules
- Separate **finding** (sourced) from **recommendation** (your judgement) explicitly.
- No platform CPC/CPM numbers unless sourced for India and dated.
- If evidence is thin, say so and recommend a small test instead of a big bet.

## Checklist
- [ ] Every recommendation traces to a finding or is labelled judgement
- [ ] Budget, timeline, KPIs in ₹ / dates
- [ ] Compliance flags for segment
- [ ] Watchlist included
