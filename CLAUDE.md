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

## Repo scope

- `token-global-color.yaml` — canonical PointSav palette (dark terminal brand)
- `token-global-telemetry.yaml` — product telemetry tokens
- `theme-pointsav-terminal.yaml` — semantic theme mappings
- `css/theme-pointsav.css` — CSS custom properties (--ps-* prefix)
- `logos/` — SVG/PNG brand marks
- `tokens/linguistic/` — corporate language protocols
