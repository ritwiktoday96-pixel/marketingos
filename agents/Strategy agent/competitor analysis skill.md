---
name: competitor-analysis
description: Strategy Agent skill. Studies one or more competitors' digital footprint through their direct sources (site, blog, social, ads, email, reviews) and turns it into MOFU-focused intelligence — gaps, angles, and specific content pieces to create or repurpose. Use when the user asks to analyse, audit, or benchmark competitors' content or marketing.
---

# Competitor Analysis → MOFU Content Plan

**Input:** client + 1–5 competitors (names/URLs). **Output:** footprint audit, gap matrix,
and a prioritised list of MOFU content pieces to create or repurpose.

MOFU = consideration stage: buyers know the problem and are comparing approaches/vendors.
MOFU formats: case studies, comparison guides, webinars, product demos/walkthroughs,
white papers/reports, ROI calculators/assessments, email nurtures, templates/checklists.

## Step 1 — Required inputs (ask if missing)
1. Client name, URL, offer, ICP
2. Competitors (direct + 1 aspirational). If unknown → hand to `market-research` or find
   via search ("[category] alternatives", ad libraries, G2 category).
3. Market/geo (default India)
4. Client's existing content inventory (URL/sitemap/list) — needed for gaps
5. Depth: Quick (1 competitor, top channels) or Full (all sources below)

## Step 2 — Collect from direct sources (cite URL + access date)
| Source | How | Extract |
|---|---|---|
| Website | homepage, product, pricing, about, sitemap.xml | Positioning line, ICP, offers, pricing model, CTAs, lead magnets |
| Blog/resources | sitemap, /blog, /resources | Topics, formats, funnel stage, cadence, gated vs ungated |
| Case studies | /customers | Industries, outcomes claimed, proof style |
| Webinars/events | /webinars, YouTube | Topics, frequency, speakers |
| Social | LinkedIn, Instagram, YouTube, X, Facebook | Content pillars, formats (carousel, reel, doc, video), cadence, engagement on top posts (likes+comments ÷ followers, labelled as estimate) |
| Meta Ad Library | facebook.com/ads/library | Active ads, creative type, CTA, landing page, run duration, variants (= what they're testing) |
| Google Ads Transparency Center | adstransparency.google.com | Search/Display/YouTube ads, region, date history, launch timing |
| LinkedIn Ad Library | linkedin.com/ad-library | Ads since Jun 2023, up to 1 yr after last impression; formats, gated offers; filter by company/keyword/country/date |
| Email | sign up to their newsletter/lead magnet (only with user's OK; use a test inbox) | Nurture sequence, cadence, offers |
| Reviews/community | G2, Capterra, Trustpilot, Google reviews, app stores, Reddit, Quora | Praise/complaint themes — buyer language for MOFU content |
| SEO (optional, if user has Ahrefs/Semrush/Similarweb) | content gap, top pages | Keywords they rank for that client doesn't |

Ad libraries show no spend/performance. Long-running ads and many variants are a *signal* of
what's working — say "likely", never "proven".

## Step 3 — Analyse
1. **Positioning map:** each competitor's core promise, ICP, price tier, proof style.
2. **Funnel inventory:** count competitor content by TOFU / MOFU / BOFU and by format.
3. **Gap matrix** (rows = buyer MOFU questions; columns = client + competitors):
   ✅ strong · ◐ thin · ❌ missing. Questions come from reviews, Reddit, Answer the Public, PAA.
4. **Gap types:** topic gap (no one covers it), format gap (covered only as blog, no
   calculator/webinar), depth gap (thin coverage), proof gap (claims without case studies),
   freshness gap (outdated).
5. **Opportunity score** per idea: Impact (0–5) × Ease (0–5); tie-break on fit with client proof.

## Step 4 — Output
1. **BLUF:** 3 lines — biggest threat, biggest gap, first 3 pieces to ship.
2. **Competitor snapshots:** one table per competitor (positioning, channels, cadence,
   top-performing themes, active ad angles, lead magnets, weaknesses from reviews).
3. **Gap matrix.**
4. **MOFU content plan** — 8–12 pieces:
   | # | Title (working) | Format | Buyer question it answers | Gap type | Create / Repurpose (from what) | Channel + distribution | CTA → next stage | KPI | Score |
5. **Repurpose map:** existing client assets → MOFU formats (e.g. blog → webinar → LinkedIn
   carousel → nurture email; case study → 60-s reel + sales one-pager).
6. **Watchlist:** pages/ads/accounts to re-check monthly + triggers (pricing change, new
   feature, new ad angle).
7. Hand-offs: vs/alternatives pieces → `competitor-content-writer`; objections surfaced →
   `sales-enablement-generator`.

## Rules
- Only public sources. No scraping behind logins, no fake accounts, no misrepresentation.
- Don't copy competitor copy/creative; ASCI Ch. IV bars imitation that misleads.
- Engagement/traffic figures from third-party tools are estimates — label them.
- Wellness/finance: note which competitor claims look unsubstantiated (a risk for them, and
  a "trust" angle for the client) — don't accuse; describe.

## Checklist
- [ ] Every observation has a source URL + date
- [ ] Gap matrix built from buyer questions, not our assumptions
- [ ] Plan items tied to a gap, a format, a channel, and a KPI
- [ ] Watchlist included
