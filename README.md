# Lesson Note Generator — standalone app

## What this is
A Node.js server (`server.js`) + one HTML page (`public/index.html`).
Every note is written by calling the Anthropic API with **your own key**,
so the AI cost is billed to you — which is what lets you charge users.

## Run it locally
1. Install Node.js 18+ (https://nodejs.org).
2. `npm install` (nothing to install yet, but keeps this step standard).
3. Copy `.env.example` to `.env` and fill in `ANTHROPIC_API_KEY` from
   https://console.anthropic.com (Settings → API Keys).
4. `node server.js` then open http://localhost:3000

## How the money side works
- Every device gets `FREE_NOTES` (default 5) free notes, tracked by a random
  ID stored in the visitor's browser — no login needed.
- After that, a visitor enters an **access code** in the "Access code" box.
  Codes you allow are set in `ACCESS_CODES` (comma-separated) and each is
  capped at `CODE_DAILY_CAP` notes per day.
- You decide how someone gets a code — e.g. they pay you via Mobile Money
  (Paystack/Flutterwave) and you message them a code, or you build a simple
  payment page later that generates one automatically. That payment page
  is the one piece this project doesn't include yet — flag it back to me
  when you're ready and I'll add it.
- Usage counters are stored in `usage.json` next to `server.js`. They reset
  by day automatically; delete the file to reset everything.

## Hosting (put it online)
Any Node host works. Two simple options:
- **Render.com** (free tier, easiest): create account → New → Web Service →
  connect this folder as a Git repo → Start command `node server.js` →
  add the `.env` values under Environment → Deploy. You get a public URL.
- **Railway.app**: similar flow, also has a free trial tier.

You'll need a GitHub account to push this folder as a repo — I can walk you
through that when you're ready, or a freelancer can do the whole hosting
setup in under an hour if you'd rather pay for that part.

## Files
- `server.js` — the whole backend: serves the page, calls the Anthropic API,
  tracks free/paid usage.
- `public/index.html` — the app itself (form + generator + saved notes).
- `public/manifest.webmanifest`, `public/icon-*.png` — let phones "Add to
  Home Screen" so it opens like a real app icon.

## Costs to expect
Check current Anthropic API pricing at https://www.anthropic.com/pricing
before setting your prices — each generated note uses a few thousand tokens.
