# Whole Yield site

The one-page site for **wholeyield.com**. Static HTML, no build system, no
dependencies, and no analytics. `index.html` and `privacy.html` are the site.

One typeface ships with the repo in `fonts/`: Inter, under the SIL Open Font
License. It is SELF-HOSTED on purpose. Do not swap it for a Google Fonts or
other CDN link. `privacy.html` states in writing that the site "makes no
requests to third-party servers" and that the typeface "is served from this
same site rather than from a font provider", so a CDN link would make the
published privacy policy false.

To preview it, open `index.html` in a browser. That is the entire dev loop.

## How it publishes

GitHub Pages serves this repo from the `main` branch, root folder. Pushing to
`main` republishes. `CNAME` holds the apex domain and must stay at the repo
root, or Pages drops the custom domain on the next deploy.

The repo is **public** on purpose. Pages sites published from a private repo
require a GitHub login to view, which would make the site unreachable to Google
(both the Play Console ownership check and Search Console) and to the public.

## Why the copy says what it says

Two claims were deliberately kept off this page. Do not add them back without
checking first:

1. **No legal entity is named.** There is no "LLC" or "Inc." anywhere, because
   no entity has been filed yet (the Lucentcast Stripe activation is blocked on
   exactly that). Naming one here would be a false claim on the page Google
   verifies against.
2. **Perfumed Decay is not claimed as a Whole Yield property.** It is co-hosted
   by three equal partners. The card says so explicitly and scopes Whole Yield's
   involvement to Daniel's production work.

Also: no em dashes in the copy, per Daniel's standing rule.

## DNS

DNS is not managed here. See `DNS-RUNBOOK.md` for the records to add and the
warning about not disturbing the Google Workspace MX records.
