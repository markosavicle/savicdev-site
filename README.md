# savicdev.com

Single-page B2B landing site for **savicdev.com** — Marko Savić, AI & Software Automation Engineer.

- One static file: `index.html` (HTML5 + Tailwind CSS CDN + vanilla JS). No build step.
- Bilingual: Serbian (default) / English. Preference is stored in `localStorage`; `?lang=en` forces English — send `https://savicdev.com/?lang=en` to foreign prospects.
- `CNAME` contains `savicdev.com` for GitHub Pages.

Preview locally: open `index.html` in a browser, or run `npx serve .`.

## Contact form (Web3Forms)

1. Go to <https://web3forms.com>, enter `marko@savicdev.com`, and copy the free access key from the email.
2. In `index.html`, find `YOUR_WEB3FORMS_ACCESS_KEY` and replace it with the key.
3. Commit and push. Submissions arrive at that inbox. Until the key is set, the form shows an error pointing visitors to the email address.

## Editing copy

All text lives in the `I18N` object near the bottom of `index.html` (`sr` and `en` blocks, same keys). Integration logos/tags are in `INTEGRATIONS` right below it.

## Deploy to savicdev.com (GitHub Pages)

1. **Enable Pages:** repo → *Settings → Pages* → Source: *Deploy from a branch*, Branch: `main` / `(root)` → Save. The custom domain `savicdev.com` is picked up from `CNAME`.
2. **DNS at your registrar** (or Cloudflare, with proxy *off* until HTTPS is issued):
   - `A` records for `@`: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - `CNAME` for `www` → `markosavicle.github.io`
3. **HTTPS:** after DNS propagates (minutes to a few hours), go back to *Settings → Pages* and tick **Enforce HTTPS**.

**Cloudflare Pages alternative:** *Workers & Pages → Create → Pages → Connect to Git* → pick `savicdev-site`, framework preset *None*, build command empty, output directory `/` → then *Custom domains → savicdev.com*.
