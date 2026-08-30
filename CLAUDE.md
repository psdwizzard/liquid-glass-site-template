# Share-site design guide — instructions for the agent building the site

You are building a **share site** (bake-off, comparison, report, demo gallery).
This folder is the house template. These instructions exist because agents keep
writing their own generic dark page from scratch and shipping something
off-style. Do not be that agent.

## Rule zero: COPY, never recreate

**Never write share-site HTML from a blank file.** Start every site by copying
`index.html` from this folder and editing it. All of the identity — the liquid
glass, the glitch dust, the lock-up, the tokens — is already in that one file.
Writing "something similar" from memory is how the identity gets lost.

If the page you need looks nothing like the example sections, still copy the
file: keep the `<head>` styles, the header, the dust canvas, the theme script,
and the footer, then replace only the `<main>` sections.

## Why this matters (read once, believe it)

These sites are often the only artifact someone keeps from a project. Every one
of them should look like it came from the same designer, the same care. A
one-off page that "looks fine" but has square corners, colored buttons, and no
lock-up quietly reads as sloppy.

## The identity — every page must have ALL of these

1. **The lock-up** in a sticky glass header: logo mark SVG + wordmark +
   product name. A placeholder mark is in `index.html` — swap in your own
   logo, never plain text alone.
2. **Monochrome. No hue anywhere.** No blue links, no green success chips, no
   red errors, no colored buttons. Hierarchy comes from opacity, weight, and
   glass depth. The single "accent" is the filled ink chip (`.chip.fill`,
   white-on-dark) — reserved for THE winner/highlight, used at most once or
   twice per page.
3. **Liquid glass surfaces.** Panels are translucent (`var(--glass)`) with
   `backdrop-filter: blur(32px) saturate(170%)`, a specular top inner
   highlight, a hairline border, and a soft deep shadow. Never a flat opaque
   `#1a1a1a` card.
4. **Glitch dust** — the animated `<canvas id="dust">` background. Keep it;
   the glass panels blurring it is the depth effect.
5. **Continuous rounded corners and pills.** Panels 1.25rem, media cards
   1.6rem, every button/chip/control a 999px pill. Nothing square.
6. **Dark by default + the light/dark toggle** (glass pill, top right).
7. **Type**: `'Inter', system-ui` for UI; `ui-monospace` for metadata,
   prompts, and figures (class `meta`).

## Building components the template doesn't have

You will constantly need things the example sections don't show (two-up
comparisons, prompt panels, filmstrips, players). Build them **from the
existing tokens and primitives** — never invent new colors or surfaces:

- Any container → `class="glass"` (winner/emphasis → `glass glass-raised`).
- Any label/status → `.chip` (`.strong` / default / `.dim` for good → bad;
  `.fill` only for the single winner).
- Source-vs-output two-up → two `.glass card` blocks in a 2-col grid, or one
  card with two `.media` panes side by side; label each pane with a small
  uppercase `.meta` caption like `SOURCE STILL` / `OUTPUT VIDEO`.
- Long prompt / code / log text → `<pre class="meta">` inside a `.glass`
  panel, `font-size: 12.5px`, `color: var(--text-muted)`,
  `white-space: pre-wrap`, generous padding. Never a bare black box.
- Buttons ("Play all", "Export") → style like `.theme-toggle`: glass pill,
  hairline border, specular inset; the ONE primary action may be an ink-filled
  pill (`background: var(--ink); color: var(--ink-contrast)`).
- Videos/images → inside `.media` with relative `media/…` paths, rounded by
  the card, `object-fit: cover`.
- New tokens are forbidden. If a value isn't derivable from the existing
  `--glass/--edge/--specular/--text*/--ink*` variables, you don't need it.

## Hard constraints (unchanged from the README)

- Single self-contained folder, opens by double-click (`file://`): no server,
  no build, no CDN, no `fetch()` of local files. Inline everything; big data
  becomes an inline JS object.
- Media by **relative path** inside the folder so the zip travels.
- Verify by actually opening the file (`open path/index.html`) before calling
  it done.

## Self-check before you deliver (all must be yes)

- [ ] Did I start from a copy of this `index.html` (not from scratch)?
- [ ] Logo mark + wordmark in a sticky glass header?
- [ ] Glitch dust canvas alive in the background?
- [ ] Zero hue on the page (grayscale-only screenshot test)?
- [ ] Every surface translucent glass with blur — no flat opaque cards?
- [ ] Every control a pill; corners ≥ 1.25rem everywhere?
- [ ] Exactly one `.chip.fill` class of emphasis, on the actual winner?
- [ ] Mono (`.meta`) used for prompts/metadata/figures?
- [ ] Works from `file://`, media paths relative, folder zippable?
