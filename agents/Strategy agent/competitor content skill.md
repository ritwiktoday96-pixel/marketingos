---
name: competitor-content-writer
description: Strategy Agent skill. Takes a competitor + product category and returns a comparison ("X vs Y") or alternatives ("best X alternatives") piece structured for BOFU conversion. Use when the user asks for a vs page, alternatives page, comparison article, or switching guide.
---

# Competitor Content Writer

**Input:** competitor name + product category. **Output:** one publish-ready BOFU piece
(markdown) + SEO pack + fact sheet with sources.

## Why this format
- Grow and Convert's analysis of 95 client articles: "alternatives"/competitor keywords
  converted at 8.43%, "A vs B" at 5.45%, "best [category]" at 4.85%. Treat as one agency's
  dataset, not a universal benchmark.
- Google's reviews system evaluates head-to-head comparisons and ranked lists; it rewards
  in-depth research and first-hand evidence over thin summaries.

## Step 1 — Required inputs (ask if missing)
1. Client product name + URL
2. Competitor name + URL
3. Page type: **vs** (buyer comparing two named tools) / **alternatives** (buyer unhappy with
   competitor) / **best-of roundup** (category-level). Default: vs if both named, else
   alternatives.
4. Dominant intent — one per page: comparison shopper, switcher, or problem-aware buyer.
5. Target buyer (role, company size, market) — default: India, SMB decision-maker
6. Proof the client can actually provide: case studies, migration stories, ratings, data.
7. Primary CTA — **one** only (demo / trial / migration guide / consult).

## Step 2 — Research (live, cite everything)
- Competitor: pricing page, feature/docs pages, changelog, integrations list, ToS limits.
- Third-party: G2, Capterra, Trustpilot, Reddit, app stores — extract recurring praise and
  complaints (paraphrase; quote ≤ 1 line with link).
- Client: same pages for parity.
- Build a **fact sheet** table: claim | client | competitor | source URL | access date.
  Anything unverified → `[UNVERIFIED]`, and it may not appear as fact in the copy.

## Step 3 — Structure

### A. "[Client] vs [Competitor]" page
1. **H1:** "[Client] vs [Competitor]: [honest differentiator] ([Year])"
2. **Quick verdict (BLUF, 60–100 words):** who each tool is best for. State where the
   competitor wins.
3. **Comparison table** — 5–7 categories that matter to the buyer (outcomes, pricing model,
   integrations, support, deployment/data handling, ease of use). Not 40 checkmarks.
4. **Category deep dives** — per category: what each does, user impact, evidence.
5. **Pricing comparison** — real example quotes in ₹ for a typical buyer size; note GST and
   billing currency; link both pricing pages with access date.
6. **What users say** — aggregated third-party sentiment, both tools, linked.
7. **Who should choose which** — explicit buyer profiles: "Pick [Competitor] if… Pick [Client]
   if…"
8. **Switching / migration** — steps, timeline, support offered, data portability.
9. **FAQ** — 5–8 named-competitor questions (pricing, migration, feature parity, contract).
   Write answers as standalone 40–60-word passages so AI answer engines can cite them.
10. **Single CTA** — repeated top, after table, end (same action each time).

### B. "Best [Competitor] alternatives" page
1. H1: "[N] Best [Competitor] Alternatives in [Year]"
2. Opening: validate why people leave the competitor (sourced complaints)
3. Client section first (400–600 words): differentiators, pricing, proof, CTA
4. 3–5 genuine other alternatives (200–300 words each) with honest pros/cons and "best for"
5. Comparison table across all options
6. FAQ: switching, migration, parity
7. CTA

### C. Optional high-trust angle
"Why [Client] might not be right for you" section or page — honesty reads as credibility.

## Step 4 — Writing rules
- Plain language. Short sentences. Translate features into buyer outcomes.
- Speak to the buying committee: finance (TCO), IT/security (data, compliance), end user (workflow).
- Frame differences as "We do X; they do Y." Never "they're bad."
- Proof above the CTA. Named, quantified case studies > logo walls. No proof? Use
  `[PLACEHOLDER: proof]` — never invent.
- Superlatives ("best", "fastest", "#1") only with substantiation + source.

## Step 5 — Compliance (India)
ASCI Code Ch. IV: compared aspects clearly stated; factual, accurate, capable of
substantiation; not chosen to give artificial advantage; no denigration; no imitation of
competitor's layout/creative. Add a footer: "Comparison based on publicly available
information as of [date]. Features and pricing may change." Flag trademark use for client's
legal review.

## Step 6 — Deliverables
1. Full article (markdown, H1–H3)
2. SEO pack: primary keyword, 5–10 secondaries ("[comp] pricing", "[comp] review",
   "[comp] alternative for [use case]"), meta title ≤ 60 chars, meta description ≤ 155 chars,
   URL slug, internal-link suggestions, schema suggestion (FAQPage; Table markup)
3. Fact sheet with sources
4. Paid repurpose: 3 conquest search-ad headline/description sets (message-matched to the page)
5. Sales repurpose: 5-line summary for reps (hand-off to `sales-enablement-generator`)
6. Refresh date: +90 days

## Checklist
- [ ] One page type, one intent, one CTA
- [ ] Competitor strengths acknowledged
- [ ] Every comparative claim sourced and dated
- [ ] Pricing in ₹ with source
- [ ] No invented proof
- [ ] ASCI disclaimer present
