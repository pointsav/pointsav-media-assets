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

None, for design tokens. **Corrected 2026-07-29** (Carbon-style consumption
model review — see `pointsav-design-system/.agent/rules/design-tokens.md`):
PointSav is the *vendor* building `pointsav-design-system`, not an adopting
tenant of it, so PointSav's own brand values live directly in that repo
(`dtcg-vault/themes/pointsav-brand.json`) as its default/reference theme —
the same way IBM Carbon ships its own neutral themes inside its own repo.
There is no separate "PointSav consumer layer" the way there is for an
adopting customer like Woodfine.

**This repo now holds binary assets and non-token governance content only**
— no DTCG tokens, no brand-color YAML, no theme CSS. This is a step further
than the 2026-07-10/2026-07-17 "upstream-only" restructure: those kept one
raw brand-values YAML file here as PointSav's "source of truth" feeding
`pointsav-design-system`'s build; that YAML turned out to be a stale,
incomplete duplicate of what `dtcg-vault` already carries (verified
2026-07-29 — every value already present, some more complete). Retired
outright rather than reconciled, per the same reasoning `css/theme-pointsav.css`
was already retired for on 2026-07-10: two consumption surfaces for the same
values is how that drift happened the first time.

## Repo scope

- `logos/` — SVG/PNG brand marks
- `governance/` — corporate language protocols, trademark/legal disclaimer text (renamed
  2026-07-27 from `tokens/linguistic/` — this is prose governance content, not a DTCG
  token; the old path name implied otherwise)

**Removed 2026-07-29:** `token-global-color.yaml`, `theme-pointsav-terminal.yaml`
— PointSav's own palette + dark-terminal theme mapper, fully superseded by
`pointsav-design-system/dtcg-vault/themes/pointsav-brand.json`'s `.dark.*`
semantic tokens (confirmed live and current — no other reference to the
"Brutalist Dark"/terminal aesthetic exists anywhere in the live app).
`token-global-telemetry.yaml` (a telemetry endpoint URL, not a design token)
remains, out of scope for this reclassification.

**Removed 2026-07-10:** `css/theme-pointsav.css` — a hand-maintained CSS
duplicate of `token-global-color.yaml`'s values that had drifted from its
own sibling YAML (6 of 8 comparable values mismatched; the canonical brand
blue `#234ed8` didn't even appear in it, using a generic `#3B82F6` instead)
and was superseded by `pointsav-design-system`'s own compiled `tokens.css`.
Deleted outright rather than reconciled — two consumption surfaces for the
same values is exactly how that drift happened. If a real need for a
generated CSS artifact resurfaces, it should be a scripted build step
reading `token-global-color.yaml`, not a second hand-authored file.
