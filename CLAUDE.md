# Project: MK Soap Co site

A redesigned showcase site for MK Soap Co, a small handmade-soap business (Michael Kennedy, the same owner as the `mikewkennedy` portfolio site). MK Soap is not currently selling: the site is a photography-forward retrospective/archive of past batches and branding, not a storefront. Static site, no build step, no framework, modeled loosely on Brian Jones' minimal, photo-led portfolio style (brianjonesdesign.net) before a later bold-color pass (see Design system).

## Stack

Plain HTML/CSS. No JS, no React, no bundler, no dependencies. Fonts loaded via a Google Fonts CDN link in `index.html`'s `<head>`.

## File structure

```
index.html     single-page site (header, hero, highlights photo grid, about/story, footer)
styles.css     the whole site's stylesheet
images/        all photography and branding assets, flat (no subfolders) — drop new photos here,
               reference as images/filename.jpg. images/README.md documents this convention.
```

## Content status — what's real vs. placeholder

Everything on the site is real. There is no placeholder copy or stock photography.

* Copy is sourced from the original live bigcartel site (mksoap.com) where possible: the "Our story" paragraph is the real About-page text almost verbatim (founded 2018, farmer's market origins, upstate NY / Arboretum vision). The hero subhead ("on hiatus, back in a future season from our new home upstate in New York") reflects what the site owner told the builder directly — MK Soap is not permanently closed, it's relaunching from a new upstate NY location in a future season, not before.
* The live bigcartel site itself had no soap product photography left (only a founder headshot and two unrelated current-store items, tote bag and stickers) — all 12+ photos in the highlights grid were supplied directly by the site owner (iPhone photos and Live Photos, some originally HEIC/MP4, converted to JPG; a couple of sideways uploads were corrected with `PIL.ImageOps.exif_transpose`, and one — `IMG_8372`, an intentionally tilted/angled product shot — was left out of the site rather than fought into alignment).
* `images/founder.png` is a real low-res founder headshot pulled from the old bigcartel account image, used in the About section.
* `images/packaging-flatlay.jpg` had a personal Venmo handle visible on a business card in one corner of the original photo — covered with a sampled wood-tone patch (not cropped, since cropping would have cut off real soap boxes elsewhere in the same shot) before publishing. Don't swap in the unredacted original.
* Brand fonts (Chewy display wordmark, Signika body) and the black/white/off-white base palette were pulled directly from the live bigcartel site's theme CSS, not invented — see Design system below for what was deliberately kept vs. changed.
* The real MK Soap logo mark (a circular "M" + lightning-bolt "K" peace-sign icon) only exists baked into photographed packaging/the felt pennant — there's no isolated vector/PNG of it, so the site doesn't use it as a standalone graphic anywhere; it's part of the photography.

## Design system

* Structure is deliberately a single page (hero + highlights + about + footer) — no separate nav pages, no shop/cart. This was an explicit site-owner choice when the structure options were presented, and matches the "retrospective, not storefront" framing.
* Original minimal pass: black `#000000` / white `#ffffff` / off-white `#f5f5f5` background, pulled straight from the live bigcartel theme CSS (`--primary-background-color`/`--secondary-background-color` there). Chewy (display/wordmark/headings) + Signika (body) were kept as-is from the live site even though they read more playful/farmer's-market than a strict Brian-Jones minimal aesthetic — the site owner explicitly chose "keep Chewy/Signika as-is" over swapping to a cleaner sans when that tension was raised.
* **Bold color refresh** (later pass, explicit site-owner request: "a deep emerald green with light mossy accents," plus "get rid of the white top banner" and "a big vibrant shape of content overlaying the main graphic"): added `--emerald-deep` (`#0E4A30`) and `--emerald` (`#1F7A4D`) as the new accent pair, plus `--moss` (`#A8C39F`) as a lighter secondary — not arbitrary picks, `--emerald-deep` is close to the real color of the felt pennant visible in `images/brand-pennant-display.jpg`, sampled directly from the photo. Links (`a`) now use `--emerald-deep` instead of the original `--accent-blue` (`#1a3c96`, still defined in `:root` but no longer the active link color — kept in case it's wanted again).
* The "white top banner" was the site header: it had no background of its own, so it inherited the light `--paper` body background and read as a plain white bar. Fixed by making `.site-header` `position: absolute` and transparent, floating directly over the hero photo instead of occupying its own strip — brand/nav text switched to white with a soft text-shadow for legibility against the photo. The header is not sticky/fixed; it scrolls away with the rest of the page past the hero, matching the original site's lack of a scroll-pinned nav.
* The "big vibrant shape" is `.hero-shape`: a large organic blob (`border-radius` percentages, bottom-left anchored, bleeding past the hero's left edge) filled with an `--emerald` → `--emerald-deep` gradient, sitting behind `.hero-caption` (the title/subhead) and in front of the hero photo. `.hero` has `overflow: hidden` so the shape's bleed doesn't cause horizontal scroll — check this with a real viewport-width test (not just a visual screenshot) if the shape's size/position changes, since percentage-based bleed can silently reintroduce horizontal overflow at in-between breakpoints. No animation on the shape or header — static only, consistent with the rest of the site.
* Highlights grid (`.photo-grid`): 3 columns desktop, 2 columns ≤672px, fixed 4:5 aspect-ratio tiles, `object-fit: cover`. No lightbox/zoom. Currently holds all 12 real photos the site owner has supplied — if more arrive, add more `<figure><img></figure>` entries in image order; there's no placeholder-tile pattern anymore (an earlier skeleton version used flat diagonal-striped placeholder divs for unfilled slots, removed once real photos replaced them all).

## Deployment

Not yet deployed anywhere (no GitHub Pages / Vercel / custom domain configured as of this writing). Ask the site owner before setting that up.

## Conventions

* No em dashes in copy
* Keep prose concise and direct
* Relative links only (`images/...`) so the site works from any host path
