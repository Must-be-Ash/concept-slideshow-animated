# Concept Slideshow Guide

A reusable brief for turning **any new feature, protocol, or product launch** into a keynote
deck (HTML) for DevRel video content. This is the **voice + preference brief**; it captures how
I want these decks made so we get close on the first pass.

**Two build paths:**
- **Animated (default for launches):** use the **`concept-slideshow-animated` skill** — it owns the
  Reveal.js template, the components (before/after code, cards, explainer slides), the morph, brand
  fonts, and alignment hooks. The principles in this brief still apply; the skill is the engine.
- **Minimal static (bare-bones):** the self-contained template in §5 below (no animation).

**How to use:** paste this file with the thing you're launching (changelog, doc page, PR, or a few
sentences) **plus the source docs**, and say *"make me a concept slideshow for [feature]."* Follow
the rules below; render it and verify before handing back.

---

## 1. The voice (non-negotiable)

The narrator (me) explains it out loud; slides are visual punctuation, NOT the explanation.

- **Calibrate to the audience. Skip the primer.** These are usually launches to devs who already
  know the space. **Drop the title card and any "what is X" explainer — cold-open on the problem.**
  Real code and real API names are wanted, not dumbed down. Only teach fundamentals for a lay audience.
- **Lead with the problem — but respect the primitive.** Name the friction without trashing the thing
  you build on. "X is a great building block. But you lay every brick yourself." > "X was painful."
- **Benefit-first.** Per capability: the one-line **promise** first, then the code/proof that delivers it.
- **One idea per slide.** Statement/payoff slides ≤ ~10 words. But **explainer slides carry a real
  sentence or two** when a benefit needs its "why it matters" spelled out — not everything is a headline.
- **Be concrete.** Real function names / config / a one-line diff beat abstractions
  (`routes: { "GET /report": { price: "$0.01" } }` > "auto-configures your route").
- **No em dashes in on-screen copy.** Periods or commas. (Speaker notes can use them.)
- **Real-world analogies** (toll booth, valet, receipt) — one per idea, don't stack them.
- **Name actors precisely** — and **name the product/brand** (these are launches, not vendor-neutral).

---

## 2. The design system

| Thing | Rule |
|-------|------|
| Background | Off-white `#fbfbfd` (or near-black for a dark deck) |
| Text | Near-black `#0b0b0f`; muted gray for sub-labels/roles/captions; hairlines `#e7e7ee` |
| Accent | **Exactly one** hue (default Base blue `#0052ff`). Put it on the **product name** and the one word that matters. One **gradient** allowed, on one **number** (the metric). |
| Fonts | **Use the brand's real fonts for a brand launch** (embed WOFF2 as base64; verify authenticity; load only 400/500/700 and only write those weights — in-between weights over-bold pills/steps). System sans otherwise. Mono for code. |
| Icons | **SVG line icons** (Feather-style) in a solid-accent circle, white stroke, centered. Not unicode glyphs (they center unevenly). Semantically true (key = wallet/keys, ≤ = cap, pen = sign). |
| Type | Big, tight-tracked headlines (`letter-spacing: -0.025em`) |
| Layout | Centered, generous whitespace, one focal element. Cards/soft shadows/rounded corners allowed. |

**Alignment discipline (matters a lot).** When several slides share a layout (a title→turn pair,
a set of "section" explainer slides, a run of before/after code slides), their kicker + title
**must land at the same Y**. Reserve equal block heights (min-height on the headline, on the
explainer sub across the set, on the code container) and **verify by measuring** — don't eyeball.

**Before/after code is the money shot.** Dim the "before," full-strength the "after," accent only
the lines that changed. Never let code clip (wrap long lines; the container must not scroll).

**Banned:** logos, clip-art icons, emoji, multiple accent hues, rainbow gradients (incl. multicolor
code-highlight themes), dense paragraphs on statement slides, drop-shadows on text. If it feels like
a cringe pitch deck, delete it.

---

## 2b. Accuracy & honesty (hard rule)

- **Verify every capability claim against the source docs/PR before it goes on a slide.** Consolidate
  the source and reason; don't guess, and don't just react/defend when questioned.
- **Distinguish the thing being launched from what it sits on** — don't credit the SDK/wrapper for the
  underlying protocol/platform/facilitator's feature.
- **Be precise on security/custody wording** (e.g. "you own and control the wallet; the key is secured
  for you" — never imply the vendor holds the user's funds if it's non-custodial).
- **Soften and flag anything you can't verify**; park "what's true / what to verify / SDK-vs-platform"
  caveats in the **speaker notes** so I'm covered in Q&A. Accuracy beats a punchy overclaim.

---

## 3. The slide arc

1. **Problem** — cold-open on the pain (respect the primitive). Statement + a broken-flow row.
2. **The turn** — the fix in a short line; the product **name in accent** (this is the morph seed).
3. **The parts** — 2–4 cards previewing the capabilities. The name docks from the turn into the kicker.
4. **Per capability, a PAIR: promise → proof.**
   - a one-line **promise** slide (the benefit), then
   - a **before/after code** slide, *or* an **explainer** slide (headline + a real sentence or two +
     a minimal code snippet) for benefits that don't demo well (discovery, gas, custody, config).
   - **Group by persona/surface** (e.g. all buyer/client capabilities, then seller/server); lead with
     the most differentiated / most on-theme for the audience.
   - Minor bonuses not worth a dedicated pair → collapse into **one shared card slide**.
5. **Metric** — one big number (the deck's single gradient moment).
6. **CTA** — the one line + the install/import.

**Length is flexible.** Distill hard, but a thorough capability walkthrough can run 12–15 slides *if
every slide earns its place* and the speaker notes carry a **cut-order** for time-constrained delivery.
The invariants: *promise before proof*, *group related capabilities*, *one idea per slide*.

---

## 4. Reusable slide layouts

Mix and match per beat (the **animated skill's template** has richer versions of all of these):

- **Statement / promise** — one big centered line, optional muted sub, optional accent-pill flow.
- **Nodes row** — pills (regular weight) for a relationship or broken "before" state.
- **Cards trio** — 2–4 cards, each a solid-accent circle SVG icon + title + role. For "the parts."
- **Before/after code** — two panes side by side; before dimmed, after full-strength with the accent
  on changed lines; a one-line caption underneath ("10+ lines → 3 lines"). Panes appear together.
- **Explainer** — headline + a real sentence or two (the "why") + a minimal code snippet with a caption.
- **Metric** — one big number (the single gradient).

**Signature transition:** the product **name shrinks from the "turn" headline into the next slide's
kicker** (auto-animate; same element, identical text, same accent on both). Keep it; use other motion
sparingly.

---

## 5. The HTML template — bare-bones static fallback

> **For launches, prefer the `concept-slideshow-animated` skill** (motion, brand fonts, before/after
> code, cards, explainer slides, the morph, alignment hooks). Use the static template below only when
> you explicitly want a no-animation, no-dependency deck. The §1–§4 and §6 rules apply to both.

Self-contained. Replace the content between the `<!-- … -->` markers. Keep the CSS and the
`<script>` (it powers ← / → / spacebar / click navigation and the progress dots) untouched.

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>__CONCEPT__ — Slides</title>
<style>
  :root {
    --ink: #111111;
    --muted: #8a8a8a;
    --line: #e6e6e6;
    --accent: #0052ff;   /* the ONE accent — change hue if you like, but only one */
  }
  * { box-sizing: border-box; margin: 0; padding: 0; }
  html, body { height: 100%; }
  body {
    background: #ffffff; color: var(--ink);
    font-family: -apple-system, "SF Pro Display", "Inter", system-ui, sans-serif;
    -webkit-font-smoothing: antialiased; overflow: hidden;
  }
  .slide { position: fixed; inset: 0; display: none; flex-direction: column;
    align-items: center; justify-content: center; text-align: center; padding: 8vh 10vw; }
  .slide.active { display: flex; }
  .big   { font-size: clamp(2.4rem, 7vw, 5rem); font-weight: 600; line-height: 1.08; letter-spacing: -0.02em; max-width: 18ch; }
  .small { font-size: clamp(1rem, 2vw, 1.5rem); color: var(--muted); font-weight: 400; margin-top: 28px; }
  .accent { color: var(--accent); }
  .title { font-size: clamp(3rem, 9vw, 6.5rem); font-weight: 700; letter-spacing: -0.03em; }
  .row { display: flex; align-items: center; gap: 34px; margin-top: 8px; }
  .node { font-size: clamp(0.85rem, 1.5vw, 1.05rem); color: var(--muted); border: 1px solid var(--line); border-radius: 999px; padding: 10px 20px; }
  .dash { color: var(--muted); font-size: clamp(1rem, 2vw, 1.4rem); letter-spacing: 2px; }
  .tags { display: flex; gap: clamp(20px, 5vw, 64px); margin-top: 12px; flex-wrap: wrap; justify-content: center; }
  .tag { display: flex; flex-direction: column; align-items: center; gap: 14px; }
  .glyph { font-size: clamp(3rem, 8vw, 5.5rem); font-weight: 700; line-height: 1; }
  .tag .label { font-size: clamp(0.95rem, 1.8vw, 1.25rem); font-weight: 600; }
  .tag .role { font-size: clamp(0.8rem, 1.4vw, 1rem); color: var(--muted); }
  .steps { display: flex; flex-direction: column; gap: 26px; margin-top: 8px; text-align: left; }
  .step { display: flex; align-items: baseline; gap: 22px; font-size: clamp(1.2rem, 2.6vw, 2rem); font-weight: 500; }
  .step .num { color: var(--accent); font-weight: 700; width: 1.2em; flex: 0 0 auto; }
  .codes { margin-top: 36px; font-family: "SF Mono", ui-monospace, monospace; font-size: clamp(1rem, 2.2vw, 1.6rem); }
  .codes .k { color: var(--muted); }
  .dots { position: fixed; bottom: 28px; left: 0; right: 0; display: flex; gap: 9px; justify-content: center; }
  .dot { width: 7px; height: 7px; border-radius: 50%; background: var(--line); transition: background .2s; }
  .dot.on { background: var(--ink); }
  .hint { position: fixed; bottom: 26px; right: 30px; font-size: 0.78rem; color: var(--line); }
</style>
</head>
<body>

  <!-- 1 · TITLE -->
  <section class="slide active">
    <div class="title">__CONCEPT_NAME__</div>
    <div class="small">__WHAT_IT_IS_IN_4_TO_6_WORDS__</div>
  </section>

  <!-- 2 · PROBLEM (statement + optional nodes row) -->
  <section class="slide">
    <div class="big">__THE_PAIN_IN_ONE_SENTENCE__</div>
    <div class="row">
      <span class="node">__A__</span>
      <span class="dash">———›</span>
      <span class="node">__B__</span>
    </div>
  </section>

  <!-- 3 · IDEA (the accent moment) -->
  <section class="slide">
    <div class="big">__THE_FIX__ <span class="accent">__KEYWORD__</span>__.__</div>
  </section>

  <!-- 4 · THE PARTS (2–4 glyphs) -->
  <section class="slide">
    <div class="tags">
      <div class="tag"><div class="glyph">__x__</div><div class="label">__PART_1__</div><div class="role">__ROLE_1__</div></div>
      <div class="tag"><div class="glyph">__y__</div><div class="label">__PART_2__</div><div class="role">__ROLE_2__</div></div>
      <div class="tag"><div class="glyph">__z__</div><div class="label">__PART_3__</div><div class="role">__ROLE_3__</div></div>
    </div>
    <div class="small">__ONE_LINE_SUMMARY__</div>
  </section>

  <!-- 5 · FLOW (3 verbs) -->
  <section class="slide">
    <div class="steps">
      <div class="step"><span class="num">1</span><span>__STEP_ONE__</span></div>
      <div class="step"><span class="num">2</span><span>__STEP_TWO__</span></div>
      <div class="step"><span class="num">3</span><span>__STEP_THREE__</span></div>
    </div>
  </section>

  <!-- 6 · PAYOFF -->
  <section class="slide">
    <div class="big">__THE_RESULT__</div>
    <div class="codes"><span class="k">{</span> __OUTPUT__ <span class="k">}</span></div>
  </section>

<div class="dots" id="dots"></div>
<div class="hint">← / → or click</div>

<script>
  const slides = [...document.querySelectorAll('.slide')];
  const dotsEl = document.getElementById('dots');
  let i = 0;
  slides.forEach((_, n) => { const d = document.createElement('div'); d.className = 'dot' + (n === 0 ? ' on' : ''); dotsEl.appendChild(d); });
  const dots = [...dotsEl.children];
  function show(n) {
    i = Math.max(0, Math.min(slides.length - 1, n));
    slides.forEach((s, k) => s.classList.toggle('active', k === i));
    dots.forEach((d, k) => d.classList.toggle('on', k === i));
  }
  document.addEventListener('keydown', e => {
    if (e.key === 'ArrowRight' || e.key === ' ') show(i + 1);
    if (e.key === 'ArrowLeft') show(i - 1);
  });
  document.addEventListener('click', e => show(e.clientX < window.innerWidth / 2 ? i - 1 : i + 1));
</script>
</body>
</html>
```

---

## 6. Checklist before handing back

- [ ] **Rendered and screenshotted every slide** in a headless browser — never ship unseen.
- [ ] Audience-calibrated: no title/primer for an expert audience; cold-open on the problem.
- [ ] Each capability is a **promise → proof** pair; related capabilities grouped; one idea per slide.
- [ ] **One** accent hue; the one gradient (if any) on one number; accent on the product name.
- [ ] **Brand fonts** embedded + verified (brand deck); only loaded weights (400/500/700) used in CSS.
- [ ] **Same-type slides align** — kicker + title at the same Y across the set (measured, not eyeballed).
- [ ] Code **never clips**; before dimmed, after accent-highlighted; panes shown together.
- [ ] SVG icons, centered, semantically true. **No em dashes on-screen.** No emoji/logos/rainbow.
- [ ] The **name-into-kicker morph** works (identical text + accent on both) — animated build.
- [ ] Every claim **verified against source**; SDK-vs-platform correct; custody wording precise;
      unverifiable claims softened; caveats in speaker notes.
- [ ] Companion **talking script** produced and in sync; **cut-order** noted for time.
- [ ] Nav + notes (`S`) + overview (`Esc`) work. A smart reader gets the gist in 30 seconds.

---

## 7. Companions

- **Talking script (produce it by default for video):** timed per-slide narration, an analogy cheat
  sheet, delivery notes (which slides are the money, what to cut for time, live-demo cutaways), and a
  source-accuracy caveat section. Keep it in lockstep when slides move or reorder.
- **Tweet/hero image (if asked):** generate via the agentcash wallet using **GPT Image 2**
  (`stablestudio.dev` → `/api/generate/gpt-image-2/generate`, poll the `pollUrl`). Same aesthetic;
  keep on-screen text short and spelled correctly.
