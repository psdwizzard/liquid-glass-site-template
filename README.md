# Share-site template

A house style for share sites: bake-offs, comparisons, reports, demo
galleries. **Monochrome liquid glass** — Apple-style frosted translucent
panels, no hue anywhere; hierarchy comes from opacity, weight, and glass
depth.

## What's in here

- `index.html` — the template itself (fully self-contained, animated
  glitch-dust background included inline).
- `CLAUDE.md` — **the design guide / agent instructions.** Auto-loads for any
  Claude session working inside (a copy of) this folder. If you're an agent
  building a site: read it first — rule zero is copy `index.html`, never
  recreate it.
- `media/` — where a project's videos/images go.

## Use

1. Copy this whole folder and rename it for the project.
2. Edit `index.html` — every spot needing project content is marked `✏️`.
   Swap the placeholder logo mark and wordmark in the header for your own.
   Each `── SECTION: … ──` block is independent: delete the ones you don't
   need, duplicate cards inside the ones you do.
3. Drop videos/images into `media/` and point the cards at them by
   **relative path**.
4. Verify by double-clicking `index.html` — it must work from `file://`.
5. Zip the folder to send it out.

## Hard rules (why the template looks the way it does)

- **Self-contained.** No web server, no build step, no npm, no CDN, no
  `fetch()` of local files. All CSS/JS inline; data inlined as a JS object if
  a page ever needs it.
- **Relative media paths only** — the zipped folder must work anywhere.
- **Dark mode is the default**; the light/dark toggle stays.
- **The lock-up stays in the header** (logo mark + wordmark + product name).
  A placeholder diamond mark ships in the template — replace it with yours.
- **Stay monochrome.** No color accents. The winner gets the FILLED white
  chip (`.chip.fill`) and the raised glass card (`.glass-raised`); everything
  else is outline glass at varying opacity (`.chip.strong` / `.chip` /
  `.chip.dim`).

## The glass recipe (liquid glass)

- Panel: translucent white fill (`rgba(255,255,255,.055)` dark /
  `rgba(255,255,255,.58)` light) + `backdrop-filter: blur(32px) saturate(170%)`.
- Edges: 1px hairline border + **specular top inner highlight** + faint
  bottom inner light + soft deep drop shadow.
- A diagonal sheen (`.glass::after`) like light catching the pane.
- Continuous rounded corners: 1.25rem panels, 1.6rem media cards, pills
  (999px) for every chip and control.
- One soft light source top-left in the page background — monochrome
  radial glows only.

## Glitch dust

A fixed `<canvas>` behind the content draws a sparse pixel-dust element,
monochromed. The rules (encoded in the inline script):

- Squares only, **all the same node size**, aligned to a pixel grid, never rotated.
- Mostly one primary color (low-alpha white/black) + **a few** brighter
  secondary nodes.
- Main cluster top-right, spreading down and out; sparse — it finishes off the
  composition, it never competes with content.
- It represents "rendering" / work-in-progress, hence the slow
  dissolve-and-respawn animation. Static under `prefers-reduced-motion`.
- Glass panels blur the dust behind them — that layering is intentional.

## Tokens

| token | dark value | note |
|---|---|---|
| background | `#08080a` | near-black |
| glass fill | `rgba(255,255,255,.055)` | + blur(32px) saturate(170%) |
| ink (the one accent) | `#ffffff` | filled chip = the winner |
| edge | `rgba(255,255,255,.12)` | hairline border |
| specular | `rgba(255,255,255,.22)` | top inner highlight |
| text muted / faint | 55% / 34% white | hierarchy via opacity |
| light bg | `#f5f5f7` | Apple-style light theme |
| type | Inter → system-ui | swap in a brand font if you have one |
| mono | ui-monospace → SF Mono | for meta/figures |

Components included: sticky glass header with lock-up + pill theme toggle,
hero with etched-glass gradient headline + glass eyebrow pill, stat tiles,
media comparison grid (raised card = winner), monochrome chips, scorecard
table, prose panel, footer.
