# textproof-example

Minimal example showing [textproof](https://github.com/natask/textproof) in action.

## Setup

```bash
pnpm install
```

## Run

```bash
# start the example site
pnpm dev

# in another terminal — verify text layout
pnpm textproof

# view the report
pnpm textproof:view
```

## What it does

Runs textproof against a static HTML page with responsive text. The report shows overflow, line-wrap drift, and font-size issues across 9 breakpoints (375px–1920px).
