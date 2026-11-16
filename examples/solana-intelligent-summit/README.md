# Example: Agentic Finance (Solana Intelligent Summit)

A real conference talk built with this skill and presented publicly. Use it as the reference for what a finished deck looks like.

Open it by serving the folder (Reveal.js loads files relative to `index.html`):

```sh
cd examples/solana-intelligent-summit && python3 -m http.server 8000
# then open http://localhost:8000 — press S for speaker notes, Esc for the overview
```

What to study:

- **Arc:** a one-idea-per-slide story that moves from the problem (browsers and ads as the front door) to the shift (agents call APIs and pay per request) and on to live examples.
- **Explainer slides:** side-by-side "you vs. your agent" comparisons, flows, and price-tag tiles instead of bullet lists.
- **Motion:** staggered reveals (`.stag`), fragments, and the logo wall that animates in.
- **Speaker notes:** every slide has an `<aside class="notes">` with the full narration.
- **Assets:** local `vendor/` (Reveal.js, Lucide and Tabler icons) and `assets/` (logos, screenshots, QR codes), so the deck works offline.

The original used the Coinbase Sans and Coinbase Mono brand fonts. They aren't included here, so the deck falls back to the system font stack in `--font` and `--mono`. To match the original, add the brand WOFF2 files as `@font-face` rules, as described in step 6 of `SKILL.md`.
