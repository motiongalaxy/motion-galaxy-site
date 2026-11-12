# Motion Galaxy site — instructions for Claude

Static website for **Motion Galaxy** (motion-galaxy.com): customizable templates for Final Cut Pro, sold on FxFactory. Owner: Tiago Pacianotto (Creative Director). The owner writes in Portuguese — answer in Portuguese.

Full history of how this site was made, decisions and pending items: `docs/HISTORICO-DO-PROJETO.md`. Read it before a large change.

## Structure

- `index.html` — the whole site (HTML + inline CSS + inline JS). No build step, no framework.
- `img/` — `logo.png` (white, inverted by CSS in light theme) and one 1280×720 WebP per product, named by product id (thumbnail of its YouTube demo).
- `.htaccess` — hides `docs/`, `.claude/`, `.git/` and the `.md` files from the public website.
- `.claude/skills/motion-galaxy-web-design/` — design & motion skill (14 guides by Emil Kowalski + Apple design). Use it for any visual/animation change.
- `.claude/skills/web-design-guidelines/` — Vercel's Web Interface Guidelines review skill (rules pinned locally in `guidelines.md`). Use it to audit changes before committing. Its rule "Title Case for headings/buttons" does not apply: this site uses Apple-style sentence case.
- `.claude/settings.json` — enables two plugins from `anthropics/claude-plugins-official`: `modern-web-guidance` (Google Chrome team; consult it before writing new HTML/CSS/JS so the code uses current web platform features) and `frontend-design` (Anthropic; UI/visual design quality). When a plugin's generic advice conflicts with this file or the motion-galaxy-web-design skill, this project's direction wins.
- `docs/` — project history and a snapshot of the old WordPress homepage. Not part of the site.

## Where things live in `index.html`

- Design tokens: `:root` at the top of `<style>` (dark-first; light theme in the two `prefers-color-scheme` / `[data-theme]` blocks — keep all three in sync).
- Products: `const PRODUCTS = [...]` — `id` (also image name), `name`, `yt` (YouTube video id), `fx` (FxFactory slug → `https://fxfactory.com/info/<fx>/`), `feature` (full-width tile), and `pt`/`en` copy `{h: headline, d: description}`.
- Product copy for es/fr/de/it/ja: `const PX = {...}` as `[headline, description]`.
- UI strings: `const T = { pt, en, es, fr, de, it, ja }`. Static HTML text uses `data-i18n="key"` and is written in English (the default).
- Languages list: `const LANGS = [...]`. Default language: `let lang = 'en';` (the visitor's choice is remembered in `localStorage` key `mg-lang`).

## Rules for changes

- Every new text must be added to **all 7 languages** (`T` and, for products, `pt`/`en` + `PX`). Keep English as default.
- Adding a product: add to `PRODUCTS`, add its copy to `PX` for es/fr/de/it/ja, add `img/<id>.webp` (1280×720, quality ~72). Keep the grid filled: featured tiles span the full row, others go in pairs.
- Links: buy → FxFactory product page; video → YouTube watch URL; channel → https://www.youtube.com/@motion-galaxy; e-mail → motiongalaxy.templates@gmail.com.
- Keep the Apple-style direction (see the skill): system font, tight tracking on big type, translucent sticky nav, restrained motion (only the hero entrance animates), respect `prefers-reduced-motion`, `prefers-reduced-transparency`, `prefers-contrast`.
- Don't use Apple logos or claim Apple endorsement; the footer trademark line stays.
- Before committing: syntax-check the inline script and test at 390px and 1280px wide (no horizontal scroll, no console errors).

## Deploy

Push to `main` → Hostinger Git auto-deployment publishes the repo root to `public_html` (once the owner has connected it in hPanel → Sites → Advanced → Git, with the webhook in GitHub). Commit messages in English.
