# savicdev.com

Single-page B2B landing site for **savicdev.com** — Marko Savić, AI & Software Automation Engineer.

- One static file: `index.html` (HTML5 + Tailwind CSS CDN + vanilla JS). No build step.
- Bilingual: Serbian (default) / English. Preference is stored in `localStorage`; `?lang=en` forces English — send `https://savicdev.com/?lang=en` to foreign prospects.
- `CNAME` contains `savicdev.com` for GitHub Pages.

Preview locally: open `index.html` in a browser, or run `npx serve .`.

## Link previews and SEO

- `og-image.png` (1200×630) is the preview card for Viber, WhatsApp, LinkedIn, Facebook, Slack and X. Its source is `tools/og-image.html`: change the text there, open it in a browser at 1200×630 and save a screenshot over `og-image.png`. Preview crawlers don't run JavaScript, so the `og:*` / `twitter:*` tags in `<head>` stay Serbian-first.
- `icon-192.png`, `icon-512.png` and `apple-touch-icon.png` are PNG renders of `favicon.svg` (messengers and iOS ignore SVG icons).
- `<head>` holds JSON-LD (`ProfessionalService`, `Person`, `WebSite`); the FAQ section holds a `FAQPage` block built from the Serbian answers. Keep it in sync when FAQ copy changes.
- `robots.txt` and `sitemap.xml` sit in the root. Bump `<lastmod>` in the sitemap after larger content changes.
- After deploying, re-scrape the preview at <https://www.linkedin.com/post-inspector/> and <https://developers.facebook.com/tools/debug/> (WhatsApp uses Facebook's cache).

## Savings calculator

The `#calc` section computes hours and money from the visitor's own inputs only (items per day × minutes × working days × share automated × hourly cost). Constants at the top of the calculator script: `EUR_RSD` (shown in the note), `PILOT` (keep in sync with the pricing section). "Send this estimate" pastes a summary into the contact form message.

## Contact form (Web3Forms)

1. Go to <https://web3forms.com>, enter `marko@savicdev.com`, and copy the free access key from the email.
2. In `index.html`, find `YOUR_WEB3FORMS_ACCESS_KEY` and replace it with the key.
3. Commit and push. Submissions arrive at that inbox. Until the key is set, the form shows an error pointing visitors to the email address.

## Editing copy

All text lives in the `I18N` object near the bottom of `index.html` (`sr` and `en` blocks, same keys). If a key is missing from one language, the browser console shows `I18N: sr/en key mismatch`.

**Adding a case study:** copy a `<!-- PROJECT CARD START: cs.N -->` … `<!-- PROJECT CARD END -->` block, rename its `cs.N.*` keys (e.g. `cs.4.t`, `cs.4.p`, …), and add those keys to both `sr` and `en`.

The logo is an inline SVG in the navbar and footer; `favicon.svg` is the same mark on a dark tile.

## Deploy to savicdev.com (GitHub Pages)

1. **Enable Pages:** repo → *Settings → Pages* → Source: *Deploy from a branch*, Branch: `main` / `(root)` → Save. The custom domain `savicdev.com` is picked up from `CNAME`.
2. **DNS at your registrar** (or Cloudflare, with proxy *off* until HTTPS is issued):
   - `A` records for `@`: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - `CNAME` for `www` → `markosavicle.github.io`
3. **HTTPS:** after DNS propagates (minutes to a few hours), go back to *Settings → Pages* and tick **Enforce HTTPS**.

**Cloudflare Pages alternative:** *Workers & Pages → Create → Pages → Connect to Git* → pick `savicdev-site`, framework preset *None*, build command empty, output directory `/` → then *Custom domains → savicdev.com*.
