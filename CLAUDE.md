# Aligned Global Network — static site rebuild

## What this is
A static HTML snapshot of alignedglobalnetwork.com, scraped from the original Laravel site (baseline commit `5430122`, captured Aug 2026). The goal is to republish it as a working static site that has no dependency on the old server. Work happens on the `fix-current-site` branch.

## Layout (as scraped)
- `site/<page>/index.html`: one folder per scraped page (homepage, about-us, leadership-team, our-services, our-impact-advisors, contact-us, donate).
- `site/<page>/assets/<host>/...`: each page's own copy of CSS, JS, and images, mirrored by host (alignedglobalnetwork.com, cdn.jsdelivr.net, cdnjs.cloudflare.com, img1.wsimg.com). The copies are byte-identical across pages.
- The HTML does **not** use these local assets. Every reference is still an absolute `https://alignedglobalnetwork.com/...` URL.
- `contact-us/index.html` is identical to `homepage/index.html`, and `leadership-team/index.html` is identical to `about-us/index.html`. On the live site, "contact" is the `/#contact` section of the homepage and "leadership team" is `/about#team`.
- Live URLs: `/`, `/service`, `/advisor`, `/about`, `/donate`.

## Target
- Homepage at the root `index.html`.
- One shared assets folder, `site/assets/`.
- All paths relative, never root-relative (`assets/...` from the homepage, `../assets/...` and `../service/` from pages one level down), so the site works both at tamera-debug.github.io/agn-current-site/ and at the root of a domain. Don't reintroduce `/`-prefixed paths.
- Clean URLs that match the live site (folder `service/index.html` serves `/service`, and so on).
- Deployed to GitHub Pages by `.github/workflows/deploy-pages.yml` on push to main.
- No references to alignedglobalnetwork.com for assets, no Laravel/server-side leftovers, and no GoDaddy tracking script.
- Donate page and every link to it removed.
- Contact form replaced by an embedded Google Form. The form URL is a marked placeholder (`GOOGLE_FORM_EMBED_URL`) until the owner provides it.

## Rules
- **Keep the design and copy unchanged unless the owner approves.** This covers text, layout, styling, images, and nav order. Fixing broken paths and removing the items listed above is in scope. Rewording, restyling, or "improving" anything is not. If a fix would change what a visitor sees, ask first.
- **Commit after each category of fix**, one commit per category, with a message naming the category.
- Don't edit the baseline commit or rewrite history.
