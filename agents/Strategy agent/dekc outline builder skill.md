---
name: deck-outline-builder
description: Strategy Agent skill. Takes a presentation goal + audience and returns a slide-by-slide outline with action titles, visual suggestions, and talking points. Use when the user asks for a deck, pitch, presentation outline, or storyline.
---

# Deck Outline Builder

**Input:** goal (what decision/action you want) + audience. **Output:** a "ghost deck" —
slide-by-slide action titles, content, visual, talking points, timing.

## Method (synthesised)
- **Minto Pyramid:** lead with the answer (governing thought), then grouped supporting
  arguments (MECE), then evidence.
- **SCQA opening:** Situation → Complication → Question → Answer.
- **Duarte:** audience is the hero; alternate "what is" vs "what could be"; end with a clear
  call to action and the "new bliss". Define what you want them to *think, feel, do*.
- **Action titles:** full-sentence takeaways, ≤ 15 words, ≤ 2 lines. One idea per slide.
- **Storyline test:** read titles alone top to bottom — they must make the whole argument.

## Step 1 — Required inputs (ask if missing)
1. Goal: the single decision/action wanted (approve budget, sign, adopt plan, learn X)
2. Audience: who, seniority, what they know, what they fear/value, likely objections
3. Format + time: live/sent-ahead/webinar; minutes available
4. Must-include content/data the user has
5. Tone/brand constraints; tool (Gamma, Canva, PowerPoint, Google Slides)

## Step 2 — Frame before slides
- **Big Idea** (one sentence): your point of view + what's at stake.
- **Think / Feel / Do** for the audience.
- **Governing thought** + 3 (max 4) MECE key arguments.
- **Audience type → structure:**
  - Executives/board: answer first, exec summary slide 2, details to appendix
  - Sales/prospect: problem → cost of inaction → what could be → solution → proof → plan → ask
  - Client report/QBR: results vs goals → insights → next-period plan → asks
  - Internal pitch/strategy: SCQA → options → recommendation → plan → risks → ask
  - Workshop/training: objectives → modules → exercises → recap
- **Slide count (working heuristic):** ~1 slide per 1.5–2 min speaking time; appendix unlimited.

## Step 3 — Output format
```
BIG IDEA:
THINK / FEEL / DO:
STORYLINE (titles only — must read as one paragraph):

SLIDE n — [Section]
Action title: <full-sentence takeaway, ≤15 words>
Content: 2–4 bullets or the single exhibit
Visual: chart type / image / diagram (line = trend, bar = comparison, waterfall = bridge,
        2×2 = positioning, table = comparison, timeline = plan)
Talking points: 3–5 bullets, conversational, what you SAY not what's on the slide
Data needed: source or [PLACEHOLDER]
Time: m:ss
```
Always include: title slide, exec summary (BLUF), the ask slide, Q&A/objection-prep slide,
appendix list.

## Step 4 — Add-ons
- **Objection prep:** top 5 likely audience questions + 1–2 line answers.
- **Speaker notes tone:** Indian English, plain, no jargon unless audience is technical.
- **Build handoff:** if user wants the actual deck, offer to pass the outline to Gamma/Canva.

## Checklist
- [ ] Storyline test passes
- [ ] One idea per slide; titles are takeaways not topics
- [ ] Clear ask on a dedicated slide
- [ ] Timings sum to available time (leave ~20% for Q&A)
- [ ] No invented data — placeholders marked
