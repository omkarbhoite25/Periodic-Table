# Improved Prompt: Periodic Table for Space Exploration

## Role and goal
Build **one self-contained, interactive web page** that reimagines the periodic table for people planning space missions. The page should help mission planners, students and engineers answer the question: *"Which elements matter off-Earth, where do we find them, and what do we use them for?"*

## Orchestration (multi-agent, model per role)
| Stage | Model | Job |
|---|---|---|
| 1. Think | **Fable** (deep reasoning only, writes no code) | Design spec: information architecture, space-data model, animation concept, interaction design |
| 2. Build | **Opus 5.5** | Implement the spec as one `index.html` file (HTML, CSS and vanilla JS, no build step) |
| 3. Verify | **Sonnet 5.5** (data accuracy, browser QA) + **Haiku 5.5** (static lint and accessibility checklist) | Check the page against the spec and against known reference values; report numbered findings with severity |
| 4. Refine | **Opus 5.5** | Fix every confirmed finding |
| 5. Re-verify | **Sonnet 5.5** | Run the browser checks again and confirm each fix; stop when no high-severity issues remain |

## Functional requirements
1. **All 118 elements** with symbol, name, atomic number, standard atomic mass, category, period, group and block. Lanthanides and actinides go in the standard f-block rows.
2. **Space lenses.** Each lens recolors the table as a heatmap, and the user switches between them:
   - *Cosmic abundance*: log scale of solar-system abundance
   - *Where to find it*: Moon (regolith, polar ice), Mars, asteroids (C-type, S-type, M-type), Earth-only
   - *Mission role*: propellant, life support, radiation shielding, structure, electronics/power, nuclear power (RTG/fission), ISRU feedstock
   - *Origin*: Big Bang, cosmic-ray spallation, small stars, exploding massive stars, merging neutron stars, white dwarfs, human-made (the classic nucleosynthesis chart)
   - *Supply risk*: Earth criticality plus off-world availability
3. **Element detail panel** with properties, origin, where it is found in the solar system, current and future space uses, and one real mission example where one exists (for example Pu-238 in the Perseverance MMRTG, or xenon in Hall-effect thrusters). Only cite real missions.
4. **Mission builder.** The user picks a scenario (Lunar base, Mars sample return, Asteroid mining, Deep-space probe). The table highlights the elements that scenario needs and shows a short "can we source it in situ?" summary.
5. **Search and filter** by name, symbol or number, with keyboard navigation (arrow keys move around the grid, Enter opens the detail panel, Esc closes it).

## Animation and visual
- A subtle animated starfield or nebula background on canvas, which pauses when the tab is hidden.
- A staggered entrance where the elements "condense" into place in order of their nucleosynthesis origin.
- Smooth, GPU-friendly transitions when the lens changes (transform and opacity only).
- An orbital or electron-shell animation in the detail panel, drawn from the element's real electron configuration.
- Respect `prefers-reduced-motion`.

## Typography
Match the font family, size scale, line height and measure of the reference page https://www.sophielwang.com/blog/paper-writing. Define all type in CSS custom properties (`--font-body`, `--font-ui`, `--font-mono`, `--step-*`) so the type can be swapped in one place.

## Quality bar
- One file, under about 400 KB, no external requests except Google Fonts and pinned CDN versions.
- Light and dark themes with an explicit `body` background, and no horizontal scroll at 375 px width.
- WCAG AA contrast, semantic markup, ARIA labels on cells, and a visible focus ring.
- Data accuracy: atomic masses within IUPAC conventions, and space claims that are defensible and conservative. Write "speculative" when they are not established.

## Deliverable
`periodic-table/index.html`, published as an artifact, plus a short changelog of the verification findings and how each was fixed.
