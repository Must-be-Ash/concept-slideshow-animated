# Design system, voice & slide arc

The richer, animated evolution of the minimal `concept-slideshow-guide`. Same DNA — plain
language, one idea per slide, correct roles — but **less austere**: designed component cards,
brand fonts, subtle depth, and real slide-to-slide motion. Discipline is what keeps "richer"
from becoming "cringe startup deck."

> These rules are tuned from real DevRel launch decks. The defaults below are what a well-made
> deck converged to *after* many rounds of feedback — start here to skip those rounds.

---

## 1. Voice (non-negotiable)

The narrator explains out loud; slides are visual punctuation, not the explanation.

- **Calibrate to the audience. Skip the primer.** If the audience already knows the space (a
  launch to devs who know the protocol), **drop the title card and any "what is X" explainer** —
  cold-open on the problem. They hear the product name from the narrator. Only teach fundamentals
  for a genuinely new/lay audience.
- **Lead with the problem — but respect the primitive.** Name the friction without trashing the
  thing you build on. "X is a great building block. But you lay every brick yourself." beats
  "X was painful." You're elevating, not dunking.
- **Benefit-first.** For each capability, state the one-line **promise** first, then show the
  code/proof. Payoff slide → demo slide, not the reverse.
- **Plain prose, real nouns.** Statement/payoff slides ≤ ~10 words. But **explainer slides carry a
  real sentence or two** — when a benefit doesn't demo well (see arc), spell out *why it matters*
  in words. Not every slide is a headline.
- **Be concrete.** Real function names, real config, a real one-line diff beat abstract phrasing.
  `createX402Server({ routes: { "GET /report": { price: "$0.01" } } })` lands harder than
  "auto-configures your route."
- **Accuracy over punch (this is a hard rule).** Every capability claim gets verified against the
  source docs/PR before it goes on a slide. Distinguish **what the SDK does vs what the underlying
  protocol/platform/facilitator does** — don't credit the wrapper for the platform's feature.
  Be precise on security/custody wording (e.g. "you own and control the wallet; the key is secured
  by CDP" — never imply the vendor custodies funds if it's non-custodial). Put "what's actually
  true / what to verify / SDK-vs-platform" caveats in the **speaker notes** so the presenter is
  covered in Q&A. When you can't verify a claim (e.g. whether something is indexed downstream),
  soften it and flag it — don't assert it.
- **No em dashes in on-screen copy.** Use periods or commas. (Speaker notes can use them.)
- **Real-world analogies** (barcode, toll booth, valet, receipt) — one per idea, don't stack them.

---

## 2. Design system (richer, still disciplined)

Defined as CSS variables in the template. Change **one** thing to rebrand: `--accent`.

| Thing        | Rule |
|--------------|------|
| Background   | Off-white `#fbfbfd` (light) or near-black `#0a0a0f` (add `class="dark"`) |
| Text         | `--ink` / muted `--muted` / hairlines `--line` |
| Accent       | **Exactly one hue.** `--accent` + `--accent-2` is only a lighter tint of the SAME hue for the one gradient. Default Base blue `#0052ff`. Put the accent on the **product name** and the one word that matters. |
| Depth        | Soft shadows + rounded corners — allowed on cards / code / nodes only |
| Font         | System sans by default. **For a brand launch, use the brand's real fonts** (see below). Mono for code. |
| Type         | Big, tight-tracked headlines (`letter-spacing: -0.025em`) |

**Brand fonts (do this for a brand deck).** Embed the brand's real WOFF2 as base64 `@font-face`
so the file stays self-contained; point `--font` / `--mono` at them. **Verify authenticity** (WOFF2
magic bytes `wOF2` + official file naming; cross-check how the brand's own app wires them) — don't
trust a random file claiming to be the brand font. **Weight discipline:** only load the weights you
use (typically 400/500/700) and only ever write *those* weights in CSS. In-between values like
550/650/750 silently snap to the nearest loaded face (usually 700) and over-bold pills, steps, and
captions.

**Icons: SVG, not unicode glyphs.** Unicode symbols center unevenly and vary by font. Use inline
Feather-style line icons (white stroke) inside a **solid-accent circle**, centered via flex. Pick
semantically true icons (key = wallet/keys, ≤ = cap/limit, pen = sign, magnifier = discovery).

**Alignment discipline (this matters a lot).** When several slides share a layout (a title→turn
pair, a set of "section" explainer slides, a run of before/after code slides), their kicker and
title **must land at the same Y**. Under Reveal's vertical centering, different content heights
push them around. Fix it by **reserving equal heights**: `min-height` on `.headline.hl-anchor`
(equal headline box), an equal `min-height` on `.sub.wide` across an explainer series (measure the
tallest, in px), and the fixed `min-height` on `.cmp` for code slides. Then verify by measuring
kicker/headline `top` across the set — they should be identical.

**Code must never clip.** Side-by-side code uses `.cmp`/`.pane` with `min-width: 0` on the flex
child + `white-space: pre-wrap` + a fixed small mono size (14px) on a 1280×720 canvas. Wrap long
import lines by hand too. Before pane = dimmed (`--dim`); after pane = full ink with the **accent
on only the changed lines**. Default to showing **both panes together** (no per-pane fragment);
reserve a fragment reveal for a single deliberate "big reveal."

**Still banned:** logos, clip-art icons, emoji, multiple accent hues, rainbow gradients (incl.
multicolor code-highlight themes — they break the one-hue rule), dense paragraphs on statement
slides, drop-shadows on text. If it feels like a pitch deck, delete it.

---

## 3. Slide arc

Not a fixed count. Distill hard, but a thorough capability walkthrough can run 12–15 slides **if
every slide earns its place** and the speaker notes carry a **cut-order** for time-constrained
delivery. The shape that works:

1. **Problem** — cold-open on the pain (respect the primitive). A statement + a broken-flow row.
2. **The turn** — the fix in a short line; the product **name in accent** (this is the morph seed).
3. **The parts** — 2–4 component cards previewing the capabilities. Kicker docks the name (morph).
4. **Per capability, a PAIR: promise → proof.**
   - a one-line **promise** slide (the benefit), then
   - a **before/after code** slide (dim before, accent after) *or* an **explainer** slide
     (headline + a real sentence or two + a minimal `.snippet`) for benefits that don't demo well
     (discovery, gas, custody, pricing config).
   - **Group by persona/surface** (e.g. all buyer/client capabilities, then seller/server), and
     lead with the most differentiated / most on-theme for the audience.
   - Minor bonuses that aren't worth a dedicated pair → collapse into **one shared card slide**.
5. **Metric** — one big number (the deck's single gradient moment). Claim-then-proof or
   proof-then-payoff depending on placement.
6. **CTA** — the one line + the install/import.

Order is a lever you'll tune; the invariant is *promise before proof*, *group related capabilities*,
*one idea per slide*.

---

## 4. Motion vocabulary (Reveal.js)

Two mechanisms — deliberate, not everywhere. Restraint reads as "designed."

### a) Auto-animate — the slide-to-slide **morph**
`data-auto-animate` on two consecutive `<section>`s; matching `data-id` elements FLIP-tween.

- **THE signature move (keep it):** the product **name shrinks from the "turn" headline into the
  next slide's kicker**. Give the shared `<span data-id="hero-word">` the **identical text** and the
  **same accent color** on both slides so it docks cleanly (color + size + position tween, no
  content cross-fade jump).
- **Adjacency:** give unrelated adjacent auto-animate pairs distinct `data-auto-animate-id`s so they
  don't try to morph into each other. A plain (non-auto-animate) slide between two morph pairs is fine.
- **Tuning:** `data-auto-animate-duration/-easing/-delay`.

### b) Fragments — step-in reveals within a slide
`class="fragment"` (`fade-up`, `fade-left`, …). Use sparingly: cards flying in one at a time, or a
single punchline landing. **Before/after code panes default to appearing together, no fragment.**

### c) Deck defaults
`transition: 'fade'`; gentle overshoot easing; `autoAnimateDuration: 0.7`; `width: 1280, height: 720`.

---

## 5. Component library (classes in the template)

- **`.kicker` / `.title` / `.headline` / `.sub` / `.accent` / `.grad`** — type scale + emphasis.
  `.headline.hl-anchor` = equal-height headline for alignment.
- **`.cards` › `.card`** (`.glyph` solid-accent circle w/ inline SVG, `.c-title`, `.c-role`) — "the parts." Reveal each `.fragment fade-up`.
- **`.flow` › `.node` (+ `.node.cap`) + `.sep`** — actors/relationship pills; the accent pill is the mechanism in a payoff flow. Pills are regular weight.
- **`.cmp` › `.pane.before` / `.pane.after`** (`.lab`, `.hl`, `.cmt`) **+ `.cmp-cap`** — before/after code that never clips.
- **`.sub.wide` + `.snippet`** (`.k`, `.hl`, `.cap`) — the explainer slide (real sentence + minimal code).
- **`.steps` › `.step` (.num)** — numbered flow. **`.metric`** — big-number payoff.

---

## 6. Companion talking script (produce it alongside)

For DevRel video decks, always also produce a timed narration script (`*-script.md`):
per-slide narration + rough timing, an **analogy cheat sheet**, **delivery notes** (which slides are
the money, what to cut for time, live-demo cutaway points), and a **source-accuracy caveat** section.
Keep it in lockstep with the deck when slides move or reorder.

---

## 7. Delivery & export

- **Navigate:** ← / → / Space, click controls, `Esc` overview. **Speaker notes:** `S`.
- **PDF:** `?print-pdf` → Print → Save as PDF, landscape, background graphics on.
- **Offline:** vendor `reveal.js@5/dist/*` + the notes plugin locally; brand fonts are already embedded.

---

## 8. Checklist before handing back

- [ ] **Rendered and screenshotted every slide** in a headless browser to verify — don't ship unseen.
- [ ] Audience-calibrated: no title/primer for an expert audience; cold-open on the problem.
- [ ] Each capability is a **promise → proof** pair; related capabilities grouped; one idea per slide.
- [ ] Exactly **one** accent hue; the one gradient (if any) on one number/word; accent on the product name.
- [ ] **Brand fonts** embedded + verified (if a brand deck); only loaded weights used in CSS.
- [ ] **Same-type slides align** — kicker + title at the same Y across the set (measured, not eyeballed).
- [ ] Code **never clips** (pre-wrap + min-width:0); before dim, after accent-highlighted.
- [ ] SVG icons, centered, semantically true. No em dashes on-screen. No emoji/logos/rainbow.
- [ ] The signature **name-into-kicker morph** works (identical text + accent on both).
- [ ] Every claim **verified against source**; SDK-vs-platform correct; custody wording precise;
      unverifiable claims softened; caveats in speaker notes.
- [ ] Companion talking script produced and in sync; cut-order noted for time.
- [ ] Nav, notes (`S`), overview (`Esc`) all work. A smart outsider gets the gist in 30 seconds.
