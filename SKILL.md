---
name: concept-slideshow-animated
description: >
  Turn any feature, protocol, or concept into an ANIMATED, presentable keynote
  deck (a single self-contained HTML file built on Reveal.js) with slide-to-slide
  morph transitions (auto-animate), step-in fragment reveals, and designed
  component cards. Use when the user wants a concept/explainer slideshow, a
  keynote deck, or "slides" for DevRel/video content that they will click through
  and present manually — and wants it animated and richer than a plain minimal
  deck (motion, transformations between slides, well-designed components). For a
  minimal static white-keynote with no animation, use the plain concept-slideshow
  guide instead; for a rendered MP4 video, use hyperframes.
metadata: { "tags": "slideshow, deck, keynote, reveal.js, auto-animate, animation, devrel, concept, explainer" }
---

# Concept Slideshow (animated)

Produce a **single self-contained `.html`** deck the user clicks through live to present a
feature/concept. Built on **Reveal.js** so you get real slide-to-slide **morph** transitions
(auto-animate), **fragment** step-reveals, speaker notes, an overview mode, and PDF export —
without hand-rolling a transition engine. It keeps the disciplined DevRel voice + slide arc of
the minimal deck, but with designed components and motion.

## How to use this skill

1. **Get the subject — and the source of truth.** The user pastes a changelog, doc page, PR, or a
   few sentences. **Read the actual source docs** if provided; you'll need them to get claims right.
   If nothing is given, ask what the concept is (one question).
2. **Verify claims before they go on a slide.** Distinguish what the *thing being launched* does
   vs. what the underlying protocol/platform/dependency does — don't credit the wrapper for the
   platform's feature. Be precise on security/custody wording. Soften and flag anything you can't
   verify; park the "what's true / what to verify" caveats in speaker notes. Accuracy over punch.
3. **Read the reference:** `reference/design-and-arc.md` — voice, design system, the arc
   (benefit-first *promise → proof* pairs, explainer slides, grouping), motion, components,
   alignment discipline, brand fonts. It is the source of truth for *what* goes on each slide.
   Then skim the worked example `examples/solana-intelligent-summit/index.html` (a full public
   conference talk built with this skill) for pacing, explainer slides, motion, and speaker notes.
4. **Copy the template:** `assets/template.html` into the user's target path (ask where, or default
   to cwd as `<concept>-deck.html`). It's pre-wired with Reveal.js, the design-system CSS, the
   battle-tested components (cards, before/after code that never clips, explainer slides, flow,
   metric), the alignment hooks, brand-font embedding guidance, and worked examples per beat.
5. **Fill it in.** Replace every `__PLACEHOLDER__`. Distill hard — one idea per slide. Deck length
   is flexible (a thorough capability walkthrough can run 12–15) *if every slide earns its place*
   and speaker notes carry a cut-order. Keep the CSS and `Reveal.initialize` intact (tune `--accent`,
   fonts, `dark` class, timing). No em dashes in on-screen copy.
6. **Brand fonts (for a brand deck).** Embed the brand's real WOFF2 as base64 `@font-face` (verify
   authenticity first) and point `--font`/`--mono` at them. Load only 400/500/700 and only write
   those weights in CSS — in-between weights over-bold pills/steps.
7. **Preserve the signature morph.** The product **name shrinks from the "turn" headline into the
   next slide's kicker** (same `data-id`, identical text, same accent on both).
8. **Produce a companion talking script** (`<concept>-script.md`) — per-slide narration + timing,
   analogy cheat sheet, delivery/cut-order notes, source-accuracy caveats. Keep it in sync on reorders.
9. **Render and verify — don't ship unseen.** Open the file in a headless browser (gstack browse /
   playwright), screenshot each slide, and confirm: no code clipping, same-type slides align (measure
   kicker/headline `top`), fonts applied, morph works. Then run the checklist in the reference.

## Defaults (state, don't ask)

- **Accent:** Base blue `#0052ff` unless the user has a brand color. One hue only; accent the product name.
- **Fonts:** system by default; **brand fonts embedded for a brand launch** (verify + weight-discipline).
- **Theme:** light (`#fbfbfd`). Switch to dark with `class="dark"` on `<body>` if asked.
- **Canvas:** 1280×720 (set in the template) so code panes have room. Delivery keyboard/click; notes `S`, overview `Esc`.
- **Self-contained.** Fonts embedded; Reveal.js from CDN. For fully offline, vendor `reveal.js@5/dist` + notes plugin locally.
- **Companion script** produced alongside for DevRel/video use.

## When NOT to use this

- **Minimal static keynote, no motion** → the plain `concept-slideshow-guide.md` brief.
- **A rendered video / MP4** (auto-paced, narrated) → `hyperframes` workflows.
- **Captions on existing footage** → `embedded-captions`.
