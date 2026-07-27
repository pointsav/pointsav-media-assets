# CLAUDE.md — pointsav-media-assets

Brand primitives and media assets for PointSav Digital Systems. Contains
global color tokens, CSS theme variables, and brand assets (logos,
favicons, wordmarks).

This file is repo-specific and inherits the workspace rules in
`~/Foundry/CLAUDE.md`. Read that first for corporate topology, identity
map, commit flow, and rules of engagement.

## Tier

**Admin-only repo.** Direct commits from `ps-administrator` identity.
No staging-tier (jwoodfine/pwoodfine) flow. No cluster clone.

## Remotes

| Name | URL | Role |
|---|---|---|
| `origin` | `git@github.com-pointsav-administrator:pointsav/pointsav-media-assets.git` | Canonical — push directly after commit |

## Commit procedure

Follow `~/Foundry/CLAUDE.md §8` admin-tier procedure for `pointsav/*` repos:

```bash
GIT_AUTHOR_NAME="ps-administrator" \
GIT_AUTHOR_EMAIL="ps-administrator@users.noreply.github.com" \
GIT_COMMITTER_NAME="ps-administrator" \
GIT_COMMITTER_EMAIL="ps-administrator@users.noreply.github.com" \
git -c user.signingkey="$HOME/Foundry/identity/pointsav-administrator/id_pointsav-administrator.pub" \
    -c commit.gpgsign=true \
    -c gpg.format=ssh \
    -c gpg.ssh.allowedSignersFile="$HOME/Foundry/identity/allowed_signers" \
    commit -m "<message>"
```

## Downstream consumer

`github.com/pointsav/pointsav-design-system` consumes brand primitives
from this repo. When token values change here, the design system's
DTCG tokens should be updated accordingly.

**This repo is upstream-only** (2026-07-10 restructure, per a cross-repo
token audit + Fable review): it holds raw brand primitives — logo/favicon
files, legal/linguistic protocol content, and one raw brand-values YAML —
that feed `pointsav-design-system`'s build. It is not a distribution
channel a creative-team member should ever need to visit directly;
design.pointsav.com's own token/asset exports are meant to serve that
audience. All derived formats (compiled CSS, per-theme bundles, JSON
exports) are generated downstream in `pointsav-design-system`, not
hand-maintained here — `css/theme-pointsav.css` was removed for exactly
this reason (see below).

## Repo scope

- `token-global-color.yaml` — canonical PointSav palette (dark terminal brand);
  the single raw source of truth in this repo
- `token-global-telemetry.yaml` — product telemetry tokens
- `theme-pointsav-terminal.yaml` — semantic theme mappings
- `logos/` — SVG/PNG brand marks
- `governance/` — corporate language protocols, trademark/legal disclaimer text (renamed
  2026-07-27 from `tokens/linguistic/` — this is prose governance content, not a DTCG
  token; the old path name implied otherwise)

**Removed 2026-07-10:** `css/theme-pointsav.css` — a hand-maintained CSS
duplicate of `token-global-color.yaml`'s values that had drifted from its
own sibling YAML (6 of 8 comparable values mismatched; the canonical brand
blue `#234ed8` didn't even appear in it, using a generic `#3B82F6` instead)
and was superseded by `pointsav-design-system`'s own compiled `tokens.css`.
Deleted outright rather than reconciled — two consumption surfaces for the
same values is exactly how that drift happened. If a real need for a
generated CSS artifact resurfaces, it should be a scripted build step
reading `token-global-color.yaml`, not a second hand-authored file.
