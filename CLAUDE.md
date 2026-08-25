<!-- drafted by wy-claudify using claude-haiku-4-5-20251001; review before trusting -->
# wholeyield-site

One-page static site for wholeyield.com. No build system, no dependencies, no analytics. GitHub Pages serves from main branch, root folder. Pushing to main republishes immediately.

## Running

Open `index.html` in a browser. That is the entire dev loop.

## Testing

No test files found in this repo.

## Layout

- `index.html`, `privacy.html`: main pages
- `manna/`: Manna page and support page
- `fonts/inter-latin.woff2`: self-hosted typeface (SIL Open Font License)
- Logo files and favicon in root

## Conventions

No em dashes in any copy (Daniel's standing rule). Never use external font CDN; `privacy.html` claims the typeface "is served from this same site rather than from a font provider", so a CDN link makes that statement false.

## Gotchas

- `CNAME` must stay at repo root or GitHub Pages drops the custom domain on next deploy.
- No legal entity is named (none filed yet). Do not add LLC, Inc., or entity names without checking first.
- Perfumed Decay is not a Whole Yield property; it is co-hosted equally. The card says so explicitly.
- DNS runbook is outside version control for security. Ask Daniel for it. Do not reintroduce it or summarize it in this public repo.
- The repo is public deliberately; private Pages sites require GitHub login, which blocks Google and the public.
