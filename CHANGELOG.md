## Verification changelog

| ID | Severity | Status | Change |
|---|---|---|---|
| D1 | medium | fixed | Lr mass corrected from [262] to [266] (Lr-266 is the longest-lived isotope). |
| D8 | medium | fixed | Hg, Zn and Br now have `w:['earth_only']`. Their trace or single detections moved into `wn` and are marked "not a resource", so the Where lens no longer shows them as Moon or Mars sources. |
| D9 | medium | fixed | Orion silver claim removed. The mission example is now the ISS Zvezda module (2000) silver-ion potable water, and the use line reads "Mir, ISS Russian segment". |
| F1 | medium | fixed | Desktop (>=1100px) uses a compact masthead and legend, cells at 1/0.96 aspect and a 2px gap. At 1440x900 the table top is 296px and the last row ends at 880px, so all 10 rows fit. |
| F2 | medium | fixed | Below 600px each mission table row is a stacked grid card (element + in-situ pill, then Role/How/Maturity with data-label captions). No overflow at 375px. |
| A11Y-01 | high | fixed | Cell aria-label starts with the symbol ("Fe, Iron, 26, ..."). |
| A11Y-02 | high | fixed | Help dialog has a "Single-key shortcuts" checkbox, stored in localStorage with try/catch. When it is off, / 1-5 m t ? are ignored. Documented in the dialog. |
| A11Y-03 | medium | fixed | Controls, legend, table and drawer are wrapped in `<main id="main" tabindex="-1">`, with a "Skip to table" link as the first focusable element. |
| A11Y-04 | medium | fixed | Light `--dot-3` changed to oklch(0.5 0.14 135), about 5.4:1 on --bg. |
| A11Y-05 | medium | fixed | Faint/dim now uses a `.in::after` surface scrim between the fill and the text. Text stays at full opacity and z-index 2. |
| A11Y-06 | medium | fixed | `.table-wrap` padding changed to 8px 8px 12px, so the focus ring and the hover scale are no longer clipped. |
| A11Y-07 | medium | fixed | `body.panel-open` reserves 420px on the right at >=1100px (the table drops secondary text through a container query). On mobile, `revealCell()` scrolls the focused cell above the 85vh sheet, and 86vh of bottom padding is added. Verified: the focused cell sits clear of the panel at 1440, 1280 and 375. |
| A11Y-08 | medium | fixed | aria-live removed from #legend and #drawer. A single `#lensStatus` (role=status) announces "Lens: X" and the mission summary or clear. |
| A11Y-09 | medium | fixed | box-shadow, border-color and background/color transitions removed (the state changes are instant). The lpulse filter step is dropped. Legend and drawer animate their children, not the blurred container. The panel uses an opaque surface with no backdrop-filter while it slides. |
| R1 | low | fixed | Search match count moved left of the native clear (×) button and the input reserves right padding, so the count is no longer overlapped on desktop. |

Earlier verification rounds also reported 27 low-severity findings that were not sent to the refiner, because the workflow only forwards low findings when there are fewer than 40 findings in total.

## Shader background

| Change | Detail |
|---|---|
| WebGPU nebula | In the dark theme, on browsers with WebGPU, the background is now a volumetric nebula with drifting star dust, a vignette and light film grain, built with the [Shaders](https://shaders.com) library (v4.0.4, MIT). It is vendored in `vendor/shaders/` so the page makes no third-party requests, and telemetry is disabled. |
| Fallback | The light theme, browsers without WebGPU, Save-Data mode and any GPU error all keep the original 2D canvas starfield. The 2D loop is paused while the nebula is showing. |
| Motion | The nebula pauses when the tab is hidden, and shows a single still frame when reduced motion is requested. |
| Search | The placeholder is shortened to "Search ( / )", and room for the match count is reserved only while a count is shown, so the placeholder is no longer clipped. |
| Favicon | An inline atom icon replaces the missing `/favicon.ico` request. |

## Background without dots

| Change | Detail |
|---|---|
| No star dots | The 2D starfield no longer draws stars or the shooting star. It keeps only the soft colour washes. |
| Generator-based shader | Following the official Shaders agent skill ("build backgrounds from generators"), the dark-theme WebGPU sky is now a slow FlowingGradient with a faint Aurora (screen blend, 35% opacity) and a Vignette. The Nebula, FloatingParticles and FilmGrain layers, which all drew dots or grain, are removed. This is also cheaper to render. |

## Professional redesign (v2)

The page was redesigned as a calm, publication-quality reference tool, following `PROMPT.md`. It now has a sticky top bar with the wordmark, a segmented view switcher, search, and theme and help controls. Tiles are quieter, with tinted fills, 1px borders and tabular numerals, and there is one accent hue. Colour scales are ordered for colour-blind readers. The detail drawer has a structured header and the sections In space, Where to find it, Origin, Properties and Electron shells. The mission preset panel has per-element in-situ verdicts. New About & methodology and Sources sections and a real footer were added. A data-preservation diff (`RAW`, `ABUND`, `ORIGIN_*`, `LOCATIONS`, `SPACE`, `RISK_*`, `SCENARIOS` and the derived `ELEMENTS`) is byte-identical to the previous version, across all 118 elements. The refinement round below changed only copy, layout and behaviour.

| ID | Severity | Status | Change |
|---|---|---|---|
| F1 | medium | fixed | Choosing a mission preset (from the select or the `m` shortcut) now scrolls the mission panel into view below the sticky bar. The scroll is smooth, or instant with reduced motion, and focus stays on the select. The offset accounts for the html `scroll-padding-top`, so the panel lands right under the bar at 1440 and 375. |
| F2 | medium | fixed | The help checkbox row now reads "Single-key shortcuts" on one line. The key list moved to the `.fine` note below. A light scrim (darker in dark mode) sits behind the `aria-modal` help dialog, and clicking the scrim closes the dialog. |
| F3 | medium | fixed | `html`, `body` and `.table-wrap` use `overflow-x: clip` (with `overflow-clip-margin: 8px` on the table so focus rings survive). The maximum scrollWidth overflow during the origin replay is now 0 at every width tested. |
| D1 | medium | fixed | The supply-risk copy now lists exactly which elements are not assessed: Tc, Pm, At, Rn, Fr, Ra, Ac, Pa and Z ≥ 96, which matches `RISK_NA` plus the Z ≥ 96 rule. The legend sub-label also changed. Data unchanged. |
| D2 | medium | fixed | The origin copy now says hatched tiles (Po–Ac, Pa, Np, Pu) occur naturally only in trace amounts, from U/Th decay, neutron capture on uranium or primordial Pu-244. It notes that Tc and Pm are also traces but are not hatched. The legend label is now "Natural traces only". |
| D3 | medium | fixed | The abundance hatch now reads "no reliable tabulated solar-system abundance (synthetic elements and short-lived natural traces)". The "always means does not apply" sentence became "hatching marks elements outside the scale for that view". The tooltip and the detail panel had the same false "not naturally present" (for example Tc and Pu), so they now say "no tabulated solar-system abundance". This is copy only; the `ABUND` values are untouched. |
| D4 | medium | fixed | The footer now reads "Static site, no analytics or cookies" because Google Fonts is a third-party request. |
| A11Y-01 | medium | fixed | Previous and Next in the detail panel use `aria-disabled` instead of `disabled`, so focus stays on the button at H and Og. `stepPanel` already guards the range and now also guards a closed panel. |
| F4 | low | fixed | With the drawer open at 1024px and wider, `main` keeps its left gutter (`margin-left: max(0, (100% - --wrap-max)/2)`). The content edge stays aligned with the wordmark (76px at 1440). Only the right side gives way to the drawer. |
| F5 | low | fixed | The search field flexes (min 150px). Between 1024 and 1279px the placeholder is "Search", so it is no longer clipped. |
| F6 | low | partly fixed | The mission preset now sits in a bordered field card that shares the legend card's top edge. The legend height still varies by view; a fixed min-height would add a large empty band to shorter legends, so this was left. |
| F7 | low | skipped | The mobile sticky header behaviour (hide on scroll) is not a quick, safe change. Left for a later round. |
| F8 | low | fixed | On mobile the mission h2 is `--step-1`, the summary is `--step--1`, and Clear stays inline with the heading. |
| F9 | low | partly fixed | Sources is a 2-column list at 1024px and wider. The prose measure stays at 68ch, and no side nav was added. |
| D0 | low | no change needed | Data diff is clean. Re-run after this round: still identical. |
| D5 | low | fixed | Added a CNSA source (Chang'e). "Last reviewed" became "Page last updated", because no fact review took place. "Mission records" became "mission pages". |
| D6 | low | fixed | Restored the status definitions: Flown = demonstrated in space; Ground test = demonstrated only on Earth; Planned or in development = funded or designed but not flown. |
| D7 | low | fixed | Page copy now uses US spelling throughout ("colored", "colors", "labeled"). The IUPAC names Aluminium and Caesium are kept. |

## Light-mode background

| Change | Detail |
|---|---|
| Visible light background | The light theme now has soft sky-blue, lavender and warm-peach washes (theme tokens `--wash-1..3`), and the WebGPU light scene uses a pastel FlowingGradient instead of near-white colors. Still no dots. |
| Gradient fix | The 2D washes faded to `transparent`, which canvas treats as transparent black, so they passed through grey. They now fade to the same hue at zero alpha. |
| Footer | Now reads "No analytics or cookies. Fonts load from Google Fonts." (R-D4). |

Before and after screenshots are in `docs/screenshots/`.
