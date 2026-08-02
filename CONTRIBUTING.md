# Contributing

## What belongs here

- **Binary brand assets** — logos, favicons, wordmarks (SVG/PNG) for PointSav Digital
  Systems, in `logos/`.
- **Non-token brand governance content** — corporate language protocols, trademark and
  legal disclaimer text, in `governance/`. This is prose, not a design token, even
  though it once lived under a folder literally named `tokens/` (renamed 2026-07-27).
- **Telemetry endpoint config** — `token-global-telemetry.yaml`. Despite the filename,
  this is an operational endpoint URL, not a design token; it's out of scope for the
  token/asset split below and stays here.

## What doesn't belong here — and where it actually goes

**Anything DTCG/CSS-custom-property-shaped — color values, theme mappings, spacing,
typography, radius, motion — never lands in this repo.** That includes PointSav's own
brand palette: PointSav is the *vendor* building `pointsav-design-system`, not an
adopting tenant of it, so PointSav's own reference theme lives directly in
`pointsav-design-system/dtcg-vault/themes/pointsav-brand.json` — the same way IBM Carbon
ships its own neutral themes inside its own repo, not in a separate "IBM brand assets"
repo.

This wasn't always the rule here, and the history is worth knowing so it doesn't
recreate itself. This repo used to hold a `token-global-color.yaml` (a hand-maintained
brand palette) and, before that, a generated `css/theme-pointsav.css`. Both drifted from
`pointsav-design-system`'s own copies of the same values — the CSS was found with 6 of 8
comparable values mismatched (the canonical brand blue `#234ed8` wasn't even in it) and
was deleted 2026-07-10; the YAML was found to be a stale, incomplete duplicate of
`dtcg-vault`'s own values and was retired 2026-07-29. **The root cause both times was the
same: two consumption surfaces for the same values.** Every design-token file removed
from this repo removes one more place that drift can start.

If you're about to add a color, theme mapping, or any other DTCG-shaped value here —
don't. It belongs in `pointsav-design-system`. If you're not sure whether something is a
design token or governance prose, the test is simple: does it define a value a
stylesheet would consume (`$value`, a hex code, a CSS custom property)? That's a token.
Does it define legal/brand-voice text a human reads? That's governance content, and it
belongs in `governance/` here.

## How to propose a change

Open an issue on [GitHub](https://github.com/pointsav/pointsav-media-assets) or route a
`DESIGN-ASSET`/`ASSET` draft through the normal cross-cluster design-draft pipeline (see
`pointsav-design-system`'s own `dtcg-vault/designing/contributing.md` for how that
pipeline works end to end — the mechanics are shared across both repos; only the content
scope differs, as described above).
