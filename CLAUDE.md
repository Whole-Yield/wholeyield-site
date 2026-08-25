<!-- drafted by wy-claudify using claude-haiku-4-5-20251001; review before trusting -->
# Whole Yield site

Static HTML site, no build system or dependencies. GitHub Pages serves from `main` at root.

## How to run

Open `index.html` in a browser. That is the entire dev loop. No build step.

## How to test

No test command found in this repo.

## Layout

- `index.html` and `privacy.html`: the site pages
- `manna/index.html`, `manna/support.html`: Manna subpages
- `fonts/inter-latin.woff2`: self-hosted Inter typeface (SIL OFL)
- Assets: logos, favicons, og-image.png

## Critical constraints

**Font is self-hosted on purpose.** `privacy.html` states "no requests to third-party servers" and "typeface served from this same site". Swapping to Google Fonts or a CDN makes the published privacy policy false. Do not change this.

**No third-party requests allowed.** The privacy policy is checked against actual behavior. Never add analytics, CDN links, or external script tags.

**CNAME must stay at repo root.** GitHub Pages drops the custom domain on the next deploy if it moves.

**Repo is public on purpose.** Private Pages repos require GitHub login, breaking Google verification and public access. Do not make private.

**No legal entity named.** No "LLC" or "Inc." anywhere. The entity has not been filed yet (Stripe activation blocked on this). Naming one would be false on a page Google verifies.

**Perfumed Decay is not a Whole Yield property.** It is co-hosted by three equal partners. The card scopes Whole Yield to Daniel's production work only.

## Conventions

- No em dashes in copy, per Daniel's standing rule.
- DNS runbook lives outside this repo (public repo with DNS details is a hijack/phishing gift). Ask Daniel.
- This repo affects only the web side. Leave mail records alone.
