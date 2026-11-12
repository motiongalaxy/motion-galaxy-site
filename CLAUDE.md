# Motion Galaxy site — instructions for Claude

Static website for **Motion Galaxy** (motion-galaxy.com): customizable templates for Final Cut Pro, sold on FxFactory. Owner: Tiago Pacianotto (Creative Director). The owner writes in Portuguese — answer in Portuguese.

Full history of how this site was made, decisions and pending items: `docs/HISTORICO-DO-PROJETO.md`. Read it before a large change.

## Structure

- `index.html` — the whole site (HTML + inline CSS + inline JS). No build step, no framework.
- `video/` — one muted 1280×720 H.264 preview per product (`<id>.mp4`, ~15 s, CRF 30, no audio, faststart, 0.7–2.2 MB). Sources are the owner's `head-<Product>.mp4` files in Drive › Motion Galaxy - Backup › Demo Videos.
- `img/` — one 1280×720 WebP per product (also the poster shown before/without the preview), named by product id (thumbnail of its YouTube demo); `favicon.png`, `apple-touch-icon.png`.
- Logo: inline SVG `<symbol id="mg-logo">` at the top of `<body>`, from the vector `Motion Galaxy.ai` (fill `currentColor`, so it follows the theme). Reuse it with `<svg class="logo"><use href="#mg-logo"/></svg>`.
- Brand fonts (Nasalization, Ethnocentric, Typodermic desktop EULA) must NOT be embedded as web fonts: the EULA forbids distributing the font files. The logo already carries them as outlines.
- `.htaccess` — hides `docs/`, `.claude/`, `.git/` and the `.md` files from the public website.
- `.claude/skills/motion-galaxy-web-design/` — design & motion skill (14 guides by Emil Kowalski + Apple design). Use it for any visual/animation change.
- `.claude/skills/web-design-guidelines/` — Vercel's Web Interface Guidelines review skill (rules pinned locally in `guidelines.md`). Use it to audit changes before committing. Its rule "Title Case for headings/buttons" does not apply: this site uses Apple-style sentence case.
- `.claude/settings.json` — enables two plugins from `anthropics/claude-plugins-official`: `modern-web-guidance` (Google Chrome team; consult it before writing new HTML/CSS/JS so the code uses current web platform features) and `frontend-design` (Anthropic; UI/visual design quality). When a plugin's generic advice conflicts with this file or the motion-galaxy-web-design skill, this project's direction wins.
- `docs/` — project history and a snapshot of the old WordPress homepage. Not part of the site.

## Where things live in `index.html`

- Design tokens: `:root` at the top of `<style>`. Single dark theme on purpose (the page is a night sky); there is no light theme.
- Shadows: everything that sits on the galaxy gets one (owner's request, 12/11/2026). Tokens `--sh-text` (text directly on the background), `--sh-lg` (tiles, gallery cards), `--sh-md` (benefit cards), `--sh-sm` (buttons, chips, carousel and pause controls), applied in the "Shadows over the galaxy" block. New elements placed on the background should use them too.
- Background: `<canvas id="galaxy">`, `position:fixed`, drawn by the "Fixed galaxy" block at the end of the script (spiral of points in color buckets, orbit lines with moving dots, shooting stars, pre-rendered star layer). The page scrolls over it; scroll adds rotation, zoom and dimming. It pauses when the tab is hidden, has a pause button (`#bg-toggle`, choice saved in `localStorage` key `mg-bg`) and starts paused under `prefers-reduced-motion`. Keep the device-pixel-ratio cap and particle counts unless you re-measure frame rate.
- Scroll effects: native CSS scroll-driven animations only, inside `@media (prefers-reduced-motion: no-preference)` + `@supports ((animation-timeline: view()) and (animation-range: entry))` (the "Motion" block). Without support the page is static and fully visible; do not add a JS polyfill. Effects: nav surface on scroll, hero receding, statement lighting up word by word (`.stmt span` with `--p`), `.reveal` rise-in, tile media scale-in, gallery slide dimming.
- Highlights gallery (`.hwrap` > `#hprev`, `#hrail`, `#hnext`; `#dots`, `#gplay`): snap carousel with side arrow buttons (wrap around). Only the centered card plays its preview; the active dot's CSS `fill` animation lasts the preview length (`--dur`, from `p.vd` or 15 s; 5 s without video) and `animationend` advances. `gLock` stops scroll events from pulling the index back during an arrow-driven smooth scroll. Side space comes from `.hspacer` elements (first and last child of `#hrail`, sized with `cqw` against `.hwrap`, a size container), not from `padding-inline`: Safari drops inline-end padding in scroll containers, which left the last card unreachable. Scroll targets and the current index use `offsetLeft`/`offsetWidth` (`gTarget`, `gNearest`; `#hrail` is `position:relative` so it is the offsetParent), never `getBoundingClientRect`, because the slide scale effect would skew them. It only runs while in view, has a pause button, and never runs under reduced motion.
- Previews: `<video class="pv" muted loop playsinline preload="none" data-src>` over the poster image in gallery cards and tile media; `src` is set only when it first plays, and it fades in on `playing`. Tile previews play while ≥45% visible. All previews require `previewsOn()` (animations on, player closed, tab visible, no Save-Data). The corner button `#bg-toggle` pauses all animation: galaxy, gallery and previews.
- Video player: `<dialog id="player" closedby="any">` opened with `showModal()`. Any `a[data-yt]` (gallery cards, tile images, tile "Watch the video") opens it on a plain click and loads `https://www.youtube-nocookie.com/embed/<id>?autoplay=1` only then; Cmd/Ctrl/middle click still opens YouTube. Closing empties the frame (stops the video). The gallery timer and galaxy drawing pause while it is open. Safari gets a click-outside fallback because it lacks `closedby`. The Claude artifact preview blocks iframes, so the player only plays on the live site.
- Products: `const PRODUCTS = [...]` in the owner's order (12/11/2026): Soccer Tools, Wedding Tools, Whiteboard Universe, Essential Callouts, Universal Titles, Galactic Backdrops, Colorful Transitions, Cosmo Slice. Fields: `id` (also image/video name), `name`, `yt` (YouTube video id), `fx` (FxFactory slug → `https://fxfactory.com/info/<fx>/`), `feature` (full-width tile: Soccer Tools and Essential Callouts, so the grid reads big, pair, big, pair, pair), `vid` (has `video/<id>.mp4`), `vd` (preview seconds when not 15), and `pt`/`en` copy `{h: headline, d: description}`.
- Product copy for es/fr/de/it/ja: `const PX = {...}` as `[headline, description]`.
- UI strings: `const T = { pt, en, es, fr, de, it, ja }` (includes `stmt`, the statement sentence, and the pause/play labels). Static HTML text uses `data-i18n="key"` and is written in English (the default).
- Languages list: `const LANGS = [...]`. Default language: `let lang = 'en';` (the visitor's choice is remembered in `localStorage` key `mg-lang`).

## Rules for changes

- Every new text must be added to **all 7 languages** (`T` and, for products, `pt`/`en` + `PX`). Keep English as default.
- Adding a product: add to `PRODUCTS`, add its copy to `PX` for es/fr/de/it/ja, add `img/<id>.webp` (1280×720, quality ~72). Keep the grid filled: featured tiles span the full row, others go in pairs.
- Links: buy → FxFactory product page; video → YouTube watch URL; channel → https://www.youtube.com/@motion-galaxy; e-mail → motiongalaxy.templates@gmail.com.
- Keep the Apple-style direction (see the skill): system font, tight tracking on big type, translucent sticky nav, motion as described above (the owner asked for the animated galaxy and Apple-style scroll effects on 12/11/2026): animate only `transform`/`opacity`, keep content visible at rest, and give any motion longer than 5 s a pause control, respect `prefers-reduced-motion`, `prefers-reduced-transparency`, `prefers-contrast`.
- Don't use Apple logos or claim Apple endorsement; the footer trademark line stays.
- Before committing: syntax-check the inline script and test at 390px and 1280px wide (no horizontal scroll, no console errors).

## Deploy

Push to `main` → Hostinger Git auto-deployment publishes the repo root to `public_html` (once the owner has connected it in hPanel → Sites → Advanced → Git, with the webhook in GitHub). Commit messages in English.
