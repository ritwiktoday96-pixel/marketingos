---
name: sales-enablement-generator
description: Strategy Agent skill. Takes a buyer objection or a deal stage and returns an objection-handling one-pager or a competitive/stage battlecard. Use when the user asks for a battlecard, talk track, objection handler, or sales one-pager.
---

# Sales Enablement Generator

**Input:** an objection ("too expensive", "we use X", "not now") OR a deal stage
(discovery, demo, proposal, negotiation, renewal) — optionally a competitor.
**Output:** one-screen, scannable asset reps can use mid-call.

## Design principles (from research)
- Rep must find the answer in ~10 seconds. One screen. Bullets, short sentences, seller language.
- Cards that get used include **both** talk tracks and proof points; cards missing either get
  ignored (Avoma/Klue findings; one audit found only 43% of cards had talk tracks, 19% had evidence).
- Refresh every 30–90 days, and immediately on competitor pricing/feature change or new
  objections from calls.

## Step 1 — Required inputs (ask if missing)
1. Client product + ICP
2. Objection verbatim OR deal stage
3. Competitor (if competitive)
4. Proof available (case studies, metrics, reviews, guarantees, pricing flexibility)
5. Where reps will use it (call, email, WhatsApp, in-person) — default: live call

## Step 2 — Classify
Objection type: **Price/budget · Need/fit · Urgency/timing · Trust/risk · Authority
(not decision-maker) · Competitor/status quo.** State the likely root cause (often not the
stated one).

## Step 3A — Objection-handling one-pager
```
TITLE: "[Objection verbatim]"                       (Fact)
WHY THEY SAY IT: 2–3 likely root causes              (Impact)
SIGNALS IT'S REAL vs A SMOKESCREEN: bullets
DISCOVERY QUESTIONS (Explore — ask before answering): 3–4 open questions
TALK TRACK (Act):
  - LAER: Listen → Acknowledge (1 line) → Explore (question) → Respond (2–3 lines)
  - Emotional/sceptical variant: Feel–Felt–Found (only with a real customer story)
  - Reframe line: agree, then shift the lens (cost → cost of inaction / TCO / ROI)
PROOF: 2–3 points with source  ([PLACEHOLDER] if client hasn't supplied)
DON'T SAY: 2–3 lines that backfire
NEXT STEP: one concrete action to advance the deal
FOLLOW-UP ASSET: link/attachment to send after call
```
For price objections include a small ROI/TCO table in ₹ (inputs marked as assumptions).

## Step 3B — Competitive battlecard (one screen)
```
SETUP: who the competitor wins with; who we win with
WEDGE: 3 outcome-led differentiators (why we win)
WHERE THEY'RE STRONG: 2 honest points + how to neutralise
LANDMINES / TRAP-SETTING QUESTIONS: 3 discovery questions that surface competitor gaps — fair, factual
OBJECTIONS: top 3–5 "But [competitor] does X" → response
PRICING: side-by-side (sourced, dated, ₹)
PROOF: switch story / case study / rating (sourced)
QUICK DISMISS: one sentence for FUD
LAST UPDATED + OWNER
```

## Step 3C — Deal-stage card
| Stage | Buyer's question | Rep goal | Assets | Exit criteria |
|---|---|---|---|---|
Fill for the requested stage: likely objections at this stage, 3 talk tracks, mutual action
plan next step, and the asset to send.

## Rules
- Seller language, not marketing copy. Read-aloud test: would a rep actually say this?
- Never disparage competitors; facts only (ASCI Ch. IV applies if reused in ads/collateral).
- Wellness/finance clients: no outcome guarantees or return promises in talk tracks.
- Every competitor fact sourced + dated, or tagged `[UNVERIFIED]`.

## Deliverables
1. The card/one-pager (markdown, ≤ ~350 words for one-pagers; battlecards one screen)
2. 3-line Slack/WhatsApp version for quick reference
3. Follow-up email draft (≤ 120 words)
4. Sources + refresh date (+30–60 days)

## Checklist
- [ ] Talk track AND proof present
- [ ] Discovery question before rebuttal
- [ ] Scannable in 10 seconds
- [ ] One clear next step
