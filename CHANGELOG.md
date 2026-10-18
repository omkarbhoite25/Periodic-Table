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
