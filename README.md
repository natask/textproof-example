# textproof-example

Live demo of [textproof](https://github.com/natask/textproof) — automated text layout verification across viewports.

**Live:** [textproof-example.pages.dev](https://textproof-example.pages.dev)

## What's here

### Example page (`/`)

A responsive site with **intentional text bugs** that textproof catches:

| Bug | CSS cause | What textproof reports |
|-----|-----------|----------------------|
| Heading overflow on mobile | `white-space: nowrap` on a long string | **FAIL** — text bleeds past container at 375px–430px |
| Fixed font clips in container | `font-size: 42px` with no `clamp()` | **FAIL** — text exceeds container width on mobile |
| Line-wrap drift | `font-size: 1.25rem` paragraph in narrow card | **WARN** — +3 lines vs desktop baseline on iPhone SE |
| Hero title (correct) | `clamp(2.5rem, 10vw, 5rem)` | **PASS** — fits all 9 breakpoints |

### Screenproof viewer (`/screenproof.html`)

Interactive report showing textproof results for this page:

- **Left panel** — list of all text checks, sorted by severity (fail → warn → pass)
- **Center viewport** — live preview of the page at the selected breakpoint
- **Click a check** → viewport scrolls to that element and highlights it with a pink outline
- **Device bar** — switch between 9 breakpoints (375px–1920px) with status dots
- **Left/right arrows** — navigate breakpoints from the viewport, or use `←` `→` keys
- **Filter tabs** — show only fails, warns, or passes
- **Search** — find checks by text content

### Accuracy report (`/why-not-pretext.html`)

Data-driven infographic showing why textproof uses real DOM measurement instead of mathematical text approximation (pretext). Based on 360 measurements across a production site:

- 77% agreement between pretext math and real DOM
- 16% false alarms from pretext (overestimates text width)
- 7% missed issues (ancestor clipping, negative margins)

## Run locally

```bash
pnpm install

# Start the example site
pnpm dev

# Run textproof against it
pnpm textproof

# Open the interactive report
pnpm textproof:view
```

## Deploy

Hosted on Cloudflare Pages. Static files in `public/` — no build step.

```bash
# Deploy via CLI
npx wrangler pages deploy public

# Or connect this repo to Cloudflare Pages:
# Build command: (empty)
# Build output directory: public
```

## Files

```
public/
├── index.html              # Example page with intentional text bugs
├── screenproof.html        # Interactive textproof results viewer
├── results.json            # Textproof results data (30 checks × 9 breakpoints)
├── why-not-pretext.html    # Pretext vs real DOM accuracy report
└── results.html            # Simple summary view
```

## Regenerate results

After changing `index.html`, re-run textproof to update the results:

```bash
textproof verify --app=https://textproof-example.pages.dev --pages=/ --channel=chrome
```

Then transform and deploy:

```bash
node transform-results.js > public/results.json
npx wrangler pages deploy public
```
