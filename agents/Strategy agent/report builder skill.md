---
name: performance-report-builder
description: Strategy Agent skill (Monthly Performance Report Builder). Takes metrics input (traffic, engagement, leads, spend) and returns a narrative monthly report with trend analysis and prioritised actions. Use when the user shares marketing numbers, a GA4/ads/CRM export, or asks for a monthly report.
---

# Monthly Performance Report Builder

**Input:** metrics (pasted, CSV, screenshot transcription) for the current month + ideally
prior month, same month last year, and targets. **Output:** decision-oriented narrative report.

A good report answers three questions: What happened? Why? What do we do next month?

## Step 1 — Required inputs (ask if missing)
1. Reporting period + comparison periods available (MoM, YoY, target)
2. Metrics by channel. Minimum set:
   - **Traffic:** sessions, users, source/medium split
   - **Engagement:** GA4 engagement rate (engaged sessions ÷ sessions; engaged = ≥ 10 s, or
     ≥ 2 page views, or a key event), avg engagement time, social engagement rate
   - **Leads/outcomes:** GA4 key events (GA4's term for conversions), MQLs/SQLs, CPL, pipeline
     ₹, revenue ₹
   - **Spend:** by channel in ₹
   - **Email:** delivered, open, click, CTOR, unsubscribe, spam complaints
3. Context: launches, campaigns, site changes, tracking changes, seasonality (festive
   season, Diwali, year-end), competitor moves
4. Audience: founder/exec, client, or channel owner (sets depth)

Never fill missing numbers. Mark `—` and list under Data gaps.

## Step 2 — Analyse
- Compute for each KPI: current, previous, Δ abs, Δ %, vs target, YoY if available.
- Derived: CPL = spend ÷ leads; lead→SQL rate; CTOR = clicks ÷ opens; cost per key event.
- Separate signal from noise (working heuristic, not a statistical test): flag changes
  < ±10% on small bases (< 100 events) as "likely noise".
- For each major move, write a **hypothesis** (why) and the evidence for it. Label as
  hypothesis if not proven.
- Check tracking anomalies first (sudden 0s, spikes, consent-banner changes, GA4 config edits).
- Optional benchmarks — label source + period, never present as targets:
  MailerLite (Dec 2024–Nov 2025, 3.6 M campaigns): all-industry open 43.46%, click 2.09%,
  CTOR 6.81%, unsub 0.22%; Health & Fitness open 47.81% / click 1.45%; Software 39.31% / 1.15%;
  Marketing & Advertising 37.23% / 1.30%; Consulting 45.96% / 2.41%.
- Email health: spam complaint rate must stay < 0.3% (aim < 0.1%) for Gmail/Yahoo bulk senders.

## Step 3 — Report structure
1. **BLUF / Executive summary** (≤ 120 words): headline result vs target, the biggest win,
   the biggest miss, the #1 action.
2. **KPI scorecard** — outcome metrics first, activity metrics as context:
   | KPI | This month | Last month | Δ % | Target | Status (🟢/🟡/🔴) | One-line read |
3. **Trend analysis** — 3–5 trends, each: what moved → why (hypothesis + evidence) → so what.
4. **Channel performance** — same mini-structure per channel (organic search, paid, social,
   email, referral, direct). Summarise patterns; don't dump platform tables.
5. **Wins & misses** — outliers that teach something.
6. **Budget** — spend vs plan, variance explanation, efficiency (CPL, cost per key event).
7. **Priority actions next month** — max 3–5, ranked by impact × effort (ICE: Impact,
   Confidence, Ease, 1–10 each). Each: channel · action · expected outcome (quantified if
   possible) · owner · deadline. No "continue monitoring".
8. **Experiments** — 1–2 tests with hypothesis and success metric.
9. **Data gaps & methodology** — sources, attribution model, tracking caveats.

## Rules
- Lead with outcomes (leads, pipeline, revenue), not vanity metrics.
- Every claim of causation is a hypothesis unless proven.
- ₹, Indian number format (12,34,567), metric units.
- Suggest charts (line for trends, bar for channel comparison) but keep report readable as text.

## Checklist
- [ ] Every KPI has a comparison
- [ ] Each trend has a "why" and a "so what"
- [ ] 3–5 ranked, specific actions with owners
- [ ] Data gaps listed; no invented numbers
