# concept-slideshow-animated

A [Claude Code](https://docs.claude.com/en/docs/claude-code) **skill** that turns any feature,
protocol, or product launch into an **animated, presentable keynote deck** — a single
self-contained `.html` file built on [Reveal.js](https://revealjs.com/) with slide-to-slide morph
transitions (auto-animate), step-in fragment reveals, designed component cards, before/after code
panes that never clip, brand-font embedding, and speaker notes.

It encodes a disciplined DevRel voice and slide arc (benefit-first *promise → proof* pairs,
explainer slides, capability grouping) so a launch deck starts close to done instead of after ten
rounds of feedback.

## What it produces

- One **self-contained HTML deck** you click through live (keyboard / click; `S` for speaker
  notes, `Esc` for overview, `?print-pdf` to export).
- A companion **timed talking script** (`*-script.md`) — per-slide narration, analogy cheat
  sheet, delivery/cut-order notes, and source-accuracy caveats.
- Optional **brand fonts** embedded as base64 `@font-face` so the file stays portable.

## Install

Skills live in `~/.claude/skills/`. Clone this repo into that directory under the same name:

```bash
git clone https://github.com/Must-be-Ash/concept-slideshow-animated \
  ~/.claude/skills/concept-slideshow-animated
```

Restart Claude Code (or start a new session) and it will be available as the
`concept-slideshow-animated` skill.

## Use

Paste the thing you're launching (a changelog, doc page, PR, or a few sentences) **plus the source
docs**, and ask for a concept slideshow. The skill will:

1. Read the source of truth and **verify every capability claim** before it goes on a slide.
2. Copy `assets/template.html` to your target path and fill it in (one idea per slide).
3. Preserve the signature morph (the product name shrinks from the "turn" headline into the next
   slide's kicker).
4. Produce the companion talking script.
5. **Render and screenshot every slide** in a headless browser to verify (no clipping, aligned
   same-type slides, fonts applied, morph works) before handing back.

See [`SKILL.md`](./SKILL.md) for the workflow and [`reference/design-and-arc.md`](./reference/design-and-arc.md)
for the full voice, design system, slide arc, motion vocabulary, and checklist.

## What's inside

| File | Purpose |
|------|---------|
| `SKILL.md` | Skill definition + step-by-step workflow |
| `assets/template.html` | Pre-wired Reveal.js deck (design-system CSS, components, worked examples per beat) |
| `reference/design-and-arc.md` | Voice, design system, slide arc, motion, alignment discipline, brand fonts, checklist |
| `examples/solana-intelligent-summit/` | Worked example: the full "Agentic Finance" talk from the Solana Intelligent Summit, with assets and speaker notes |
| `concept-slideshow-guide.md` | The **minimal static** fallback: a no-animation, no-dependency deck template + the same voice/design principles |

There are two build paths: the **animated** skill (default for launches) and the **minimal
static** template in `concept-slideshow-guide.md` for a no-animation, no-dependency deck.

## Related skills

This skill produces a deck you present or click through. It does **not** depend on anything else.

If you instead want a **rendered, auto-paced, narrated MP4 video**, that's a different tool:
[**hyperframes**](https://github.com/heygen-com/hyperframes) (install with `npx hyperframes init`).
The two are complementary — use this skill for a live keynote deck, hyperframes for a rendered
video.

## License

No license file is included yet. Add one (e.g. MIT) if you want to permit reuse.
