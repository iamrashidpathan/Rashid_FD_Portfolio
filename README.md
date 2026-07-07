# Rashid Reyaz Khan — Portfolio (Frontend / Mujin-tailored)

**Live site:** [iamrashidpathan.github.io/Rashid_FD_Portfolio](https://iamrashidpathan.github.io/Rashid_FD_Portfolio/)

A single-file, zero-build portfolio aimed at real-time-UI frontend roles (built with Mujin's Senior Frontend Engineer JD in mind). Theme: **Operator Console / MujinController HUD** — a dark robotics-console look with an animated *digital-twin* hero (isometric grid + a pick-and-place motion arc), telemetry readouts, and section headers styled as console modules.

Why this theme: Mujin's minimum requirements call out **CSS/SVG visual effects and animation** and **web-performance work**. The hero is a hand-written `<canvas>` animation (dpr-capped, paused when the tab is hidden, with a static fallback) — so the page itself demonstrates the skill, not just claims it.

Everything is in `index.html` — all CSS/JS inline, **no external runtime dependency** (only Google Fonts via `<link>`), vanilla JS only.

## Run locally
```
python3 -m http.server 8000   # http://localhost:8000
# or just open index.html
```

## Deploy
- **GitHub Pages:** push `index.html` (+ `og-image.png`) → Settings → Pages → deploy from `main` / root.
- **Netlify:** drag the folder in, or `netlify deploy`.
- **Vercel:** run `vercel`, accept the static defaults.

After deploy, update `og:url` / `og:image` / `twitter:image` in `<head>` to your real domain.

## Customize — where things live
- **Colors & fonts:** CSS custom properties under `:root` (dark) and `[data-theme="light"]` (light), at the top of `<style>`. Two accents by design: `--signal` (cyan = perception/vision) and `--motion` (amber = actuation) — a real HUD separates sensing from motion.
- **Content:** plain HTML in `<main>` — hero, Profile readout (`.readout`), Trajectory (`.job` articles), Systems (`.skill`), Payload (`.card`), contact links. Skill tags with class `tag req` are highlighted as role-critical — edit that list to match whatever role you're targeting.
- **Config constants** (top of the `<script>` IIFE):
  - `CALENDLY_URL` — empty = email-only booking; set your scheduler link and an **"Open scheduler"** button appears (never a dead link).
  - `EMAIL` — used by booking, command palette, and contact.
- **Assistant knowledge:** the `KB` array — `{k:[keywords], a:"answer"}`. Runs 100% client-side (no backend, no key), so it works on static hosting. It has a Mujin-fit answer built in.

### Upgrade the assistant to a real LLM (optional)
Keep the key server-side. Swap `answer()` for a `fetch()` to your own serverless proxy:
```js
async function answer(q){
  const r = await fetch("/api/chat", {
    method:"POST", headers:{"Content-Type":"application/json"},
    body: JSON.stringify({ message:q })
  });
  return (await r.json()).reply;
}
```
Never put an API key in `index.html`.

## Features
Boot/calibration sequence with % counter · animated canvas digital-twin hero · HUD side rail with scroll progress · reveal-on-scroll (IntersectionObserver) · light/dark toggle (in-memory) · command palette (Ctrl/Cmd-K) · client-side assistant · mailto booking with optional Calendly · responsive (1200 / 860 / 480 px) · keyboard-navigable, visible focus · `prefers-reduced-motion` respected · canvas wrapped in try/catch with graceful hide · dpr capped at 2 · rendering paused when tab hidden.

## Social preview
`og-image.svg` (1200×630) is the source. Export to PNG for best sharing support:
```
rsvg-convert -w 1200 -h 630 og-image.svg -o og-image.png
#   or: npx svgexport og-image.svg og-image.png 1200:630
#   or open the SVG in a browser and screenshot at 1200×630
```

## Honesty note
All content comes from the provided (Mujin-tailored) resume — no invented employers, titles, or metrics. Payload/work links are marked as placeholders (`aria-disabled`) since no public demo URLs were supplied; wire them up when ready. Note: this resume lists Oracle IRT2 as reaching 50,000+ users and EXL Vantage as healthcare/medical — the earlier general resume phrased these differently, so double-check which numbers you want public before sending.
