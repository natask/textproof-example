# textproof-example

Live demo of [textproof](https://github.com/natask/textproof) catching text layout issues.

**Live:** https://textproof-example.pages.dev

## What it shows

A responsive HTML page with intentional text issues:
- **Card headings** use `white-space: nowrap` → overflow on mobile
- **Hero title** uses `clamp()` for fluid sizing
- **Paragraph text** tests line-wrap drift across breakpoints

Run textproof against this page to see what it catches at each breakpoint (375px–1920px).

---

## Local setup

```bash
pnpm install
```

## Local run

```bash
# start the example site on http://localhost:3000
pnpm dev

# in another terminal — verify text layout
pnpm textproof

# view the report in your browser
pnpm textproof:view
```

---

## Deploy to Cloudflare Pages

1. **Push to GitHub**
   ```bash
   git push origin master
   ```

2. **Connect to Cloudflare Pages:**
   - Go to [dash.cloudflare.com](https://dash.cloudflare.com) → Pages
   - Click "Create project" → "Connect to Git"
   - Select this repo: `natask/textproof-example`
   - Build settings:
     - **Build command:** (leave empty)
     - **Build output directory:** `public`
   - Click "Save and deploy"

3. **Done!** Your site is live at `https://textproof-example.pages.dev`

Now people can visit the live site and run textproof against it:
```bash
textproof verify --app=https://textproof-example.pages.dev --pages=/
```
