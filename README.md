# nickmaffei.me

Static personal site. Single `index.html`, embedded CSS, no build step. Light/dark mode auto via `prefers-color-scheme`.

## Local preview

```sh
open index.html
# or for hot reload:
npx serve .
```

## Deploy — Cloudflare Pages (free, fast, push-to-deploy)

### One-time setup (~10 min)

1. **Push to GitHub**
   ```sh
   gh repo create nickmaffei-me --public --source=. --remote=origin --push
   ```
   (Or create the repo via web and push manually.)

2. **Cloudflare Pages → Connect to Git**
   - https://dash.cloudflare.com → Workers & Pages → Create → Pages → Connect to Git
   - Pick `nickmaffei1/nickmaffei-me`
   - Build command: *(leave empty)*
   - Build output directory: `/`
   - Save & Deploy

3. **Custom domain → nickmaffei.me**
   - Cloudflare Pages → your project → Custom domains → Set up custom domain → `nickmaffei.me`
   - Cloudflare will tell you the exact CNAME / A records needed.

4. **Point GoDaddy DNS at Cloudflare**

   You have two paths. Path A is simpler; Path B gives you the full Cloudflare proxy benefit.

   **Path A — keep DNS at GoDaddy, point CNAME at Cloudflare Pages:**
   - GoDaddy → DNS → `nickmaffei.me`
   - Add: `CNAME` record, name `@` (or `www`), value `<your-project>.pages.dev`
   - Save. Propagation: 5–30 min.

   **Path B — move DNS to Cloudflare (recommended for redirects + speed):**
   - Cloudflare → Add a Site → `nickmaffei.me` → Free plan
   - Cloudflare gives you 2 nameservers (e.g. `tom.ns.cloudflare.com` + `lia.ns.cloudflare.com`)
   - GoDaddy → DNS → Nameservers → "I'll use my own nameservers" → paste both Cloudflare ones
   - Propagation: 1–24 hr typically; site stays up the whole time.

5. **301 redirect `nickmaffei.net` and `nickmaffei.org` → `nickmaffei.me`** (if you want)
   - Easiest with Path B above. In Cloudflare add both domains → Redirect Rules → catch-all 301 to `https://nickmaffei.me$1`.
   - Owns the search results, prevents duplicates.

### Subsequent updates

```sh
git add . && git commit -m "Tweak copy" && git push
```
Cloudflare auto-deploys on push. Build takes ~10s.

## Content TODOs

None open. The earlier TODO markers (title, role one-liner) are filled in. Still worth a one-time check: the Strava URL (`/athletes/nickmaffei`).

## Adding a blog later

Easiest path when the time comes: drop in **Astro** (`npm create astro@latest`) and migrate `index.html` to a layout. Astro builds to static HTML, deploys the same way to Cloudflare Pages, and gives you `/blog/post-slug` routes plus markdown authoring.

Don't bother until you actually have a post written. Adding the blog is a 1-hour migration when you're ready.

## Files

```
nickmaffei-me/
├── index.html         # Single-page site, all CSS embedded
├── README.md          # This file
└── .gitignore
```
