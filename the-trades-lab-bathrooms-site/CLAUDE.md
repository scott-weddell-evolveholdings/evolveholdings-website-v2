# The Trades Lab — Bathroom WOW Demo Site (project brief for Claude)

You are working on a **"WOW" demo website** for The Trades Lab: a cinematic before/after site
we build to show a prospect what their new site could look like. This example is **Lumina
Bathrooms** (a fictional Manchester bathroom fitter used as the demo). Live example: a Netlify
static site.

## What this project is
A **single, self-contained `output/index.html`** (hand-written HTML/CSS/JS — no framework, no
build step). It is one of many **per-niche templates**; this one is the bathrooms niche.
- `output/index.html` — the whole site.
- `output/assets/frames/` — **193 JPG frames** (`f_001.jpg`…`f_193.jpg`) that drive the hero.
- `output/assets/team/` — real team photos used in the site.
- `output/cookie-policy.html`, `output/privacy-policy.html`, `output/terms-and-conditions.html`
  — legal pages.
- `source-media/*.mp4` — the raw bathroom transformation video the frames were extracted from
  (source material; not loaded by the page, not deployed — lives outside `output/` on purpose).

**`output/` is exactly what gets deployed and is safe to hand to a prospect as-is** (it's already
the live public site). Everything else in this project (`docs/`, `source-media/`, this file) is
internal working material and must never be bundled into a client- or lead-facing download —
see "Packaging a lead-magnet download" below.

## Repo layout
Note the repo root is one level **above** this folder (`evolveholdings-website/`), and
`netlify.toml` lives there — not inside `the-trades-lab-bathrooms-site/` — because its
`publish` path (`the-trades-lab-bathrooms-site/output`) is relative to the repo root. Don't move
it into this folder or the live Netlify build will 404.

## The business (why this exists)
The Trades Lab sells these cinematic sites to UK trades, **from £1,500** (client owns it). This
demo is the "here's yours" artefact. See `docs/OFFER-AND-POSITIONING.md`.

## How the hero works (the WOW — don't break it)
The hero is a **scroll-scrub**: a `<canvas>` paints frames `f_001…f_193` as the user scrolls,
so the bathroom transforms dated→immaculate ("Before" → "After"). It is NOT a `<video>`.
- Desktop and mobile each have their own scrub block (see the two IIFEs near the bottom of
  `index.html`, `#hero` / `#heroM`).
- All 193 frames must ship, or the hero shows a blank navy background.

## Run / preview
No build. Open `output/index.html` in a browser, or serve the `output/` folder statically.
Deploy = drop the **whole `output/` folder** (index.html + assets + frames) onto a static host
(Netlify). **All paths are relative** — keep them that way. If deploying by drag-and-drop, zip
the folder first so the frames folder doesn't get dropped (a past bug: frames 404'd because the
folder didn't upload).

## Customising for a real client (this is the job)
Swap content only, keep the structure/hero engine:
- Business name, town, phone, services, reviews, FAQ, SEO meta — all in `index.html`.
- The before/after gallery + process video currently use external (CDN) image/video URLs —
  replace with the client's own.
- To change the hero transformation, extract new frames from a client's before/after video into
  `assets/frames/` as `f_001.jpg…` (see the funnel repo's `extract_frames.sh` for the pattern)
  and update the frame count `N` in the two hero scripts.

## Packaging a lead-magnet download
When this demo is offered as a downloadable lead magnet, package **only `output/`** (zip that
folder as-is). Never include `docs/`, `source-media/`, `CLAUDE.md`, or anything from the repo
root — those contain internal sales positioning, brand strategy, and build notes that aren't for
a prospect. `downloads/*.zip` (git-ignored, generated locally) is where that packaged zip lives;
regenerate it after any `output/` change rather than trusting a stale copy.

## Verify before "done"
The team's standard is to check every change in a **real headless browser** (screenshot desktop
+ mobile) before calling it finished — don't trust the code, look at the render.

## Brand
See `docs/BRAND-GUIDELINES.md`. Navy #0E1B2A, brass #C9A227, teal #0F766E, chalk #F7F4EF;
Space Grotesk (display) + Inter (body); plumb-bob mark.

## Notes on the other docs
`docs/design.md`, `docs/hero-concept.md`, `docs/hero-asset.md`, `docs/intake.md`,
`docs/TRACKER.md` are the original build notes/spec for this niche template — useful background,
internal-only (see "Packaging a lead-magnet download" above).
