# Prompt: Periodic Table for Space (v2, professional redesign)

## 1. Goal
Redesign the existing single-file site `index.html` into a **professional, publication-quality reference tool**. Mission planners, engineers, students and science journalists should be able to trust it, cite it and use it daily.

"Professional" means, concretely:
- **Calm and confident.** One accent hue, restrained colour, generous whitespace, nothing that competes with the data. The page should feel closer to a NASA technical reference or a well-made data journalism piece (FT, The Pudding, Our World in Data) than a game UI.
- **Clear hierarchy.** The reader knows within 3 seconds what the page is, what the active view shows, and how to change it.
- **Credible.** Every claim has a source. Methodology and limitations are stated openly, and speculative content is visibly marked.
- **Finished.** Real header and footer, consistent spacing, aligned edges, no clipped text, no visual bugs, polished empty and loading states.

## 2. Audience and jobs to be done
1. *"Which elements can we source on the Moon, Mars or asteroids?"* Use the **Where to find it** view and the mission presets.
2. *"Why does this element matter in space, and what has actually flown?"* Use the element detail panel, with flown, tested, planned and speculative labels.
3. *"Where did this element come from in the universe?"* Use the **Origin** view.
4. *"Which elements are supply risks for space hardware?"* Use the **Supply risk** view.

## 3. Hard constraints (do not break)
- Keep **all verified data and claims** exactly as they are: masses, configurations, origins, where-found tags, roles, mission examples and their status labels. This is a design and UX redesign, not a data rewrite. Fix data only where a verifier proves an error.
- Keep **all existing features**: 5 lenses, mission presets, detail panel with the electron-shell animation, search, keyboard navigation, theme toggle, shortcuts dialog, replay of the origin story.
- Keep it a **single static `index.html`**, plus the vendored `vendor/shaders/shaders-4.0.4.js` (MIT). No build step and no new third-party runtime requests except Google Fonts.
- Keep the **background free of dots, stars and particles**. Background motion may only come from the Shaders generators (FlowingGradient, Aurora, MeshGradient), per the official Shaders skill. It must sit far behind the content, and the page must read perfectly with the shader off.
- Must work at **375 px** wide with no horizontal page scroll, in **light and dark**, and with **reduced motion**.

## 4. Design direction
- **Layout:** a sticky top bar with the wordmark, the view switcher (segmented control) and search, and the theme and help controls. Below it, a short intro (one sentence and a "How to read this" link), the active view's legend, the table, then **About & methodology**, **Sources**, and a footer.
- **Table:** tiles are quieter by default. Use tinted fills at lower saturation, crisp 1 px borders, and consistent internal alignment (atomic number top-left, symbol, name, mass in tabular numerals). The active lens drives colour. Hover and focus get a clear, non-bouncy highlight. Keep the gap between the f-block and the main table.
- **Colour:** neutral surfaces with a slight cool hue bias, one accent, and lens scales that are perceptually ordered (sequential for abundance and risk, categorical for origin and role). Every scale must be colour-blind safe and pass WCAG AA for tile text in both themes.
- **Typography:** the type tokens stay in one `:root` block (`--font-body`, `--font-ui`, `--font-mono`, `--step-*`) so they can be swapped to match the reference site https://www.sophielwang.com/blog/paper-writing once it is reachable. Use the serif for headings and prose, a neutral sans for UI, and mono with tabular numerals for data. Build on a modular scale and keep prose to about 68 characters per line.
- **Motion:** only purposeful motion. Ease-out at 150–250 ms for UI changes, a cross-fade when the lens changes, and one orchestrated entrance (the origin-ordered reveal), replayable. No idle wiggles or pulsing badges.
- **Detail panel:** a right-hand drawer on desktop and a bottom sheet on mobile. Show a structured header (symbol, name, Z, mass, category), then sections in this order: *In space* (uses with status chips), *Where to find it*, *Origin*, *Properties*, *Electron shells*. Previous and next buttons, and Esc to close.
- **Mission presets:** a clear panel listing the required elements, an in-situ verdict per element, and an honest summary sentence.

## 5. Credibility content (new)
- **About & methodology:** what each lens encodes and how scores are derived, including the supply-risk formula, and that M-type compositions are inferred from meteorites.
- **Sources:** IUPAC standard atomic weights; Lodders (2003/2021) solar-system abundances; Johnson (2019) nucleosynthesis periodic table; NASA and ESA mission pages for flown examples. Give each a plain link.
- **Last reviewed** date, and a note that speculative items are labelled.

## 6. Accessibility and quality bar
- Semantic landmarks, a skip link, a grid with roving tabindex and arrow-key navigation, visible focus rings, ARIA live status for view changes, and dialogs that trap and restore focus.
- WCAG AA contrast for all text, including text on tiles, in both themes.
- Zero console errors. Lighthouse-level hygiene: meta description, Open Graph tags, favicon, `lang` attribute, a sensible `<title>`.
- Performance: the inline script stays readable. The shader runs only when the tab is visible and WebGPU is available, and the 2D fallback is cheap.

## 7. Process (multi-agent, model per role)
| Stage | Model | Output |
|---|---|---|
| Critique and redesign spec | **Fable**, thinking only, writes no code | Reviews current screenshots, writes a prioritised critique and a precise redesign spec against sections 1–6 |
| Implement | **Opus 5.5** | Edits `index.html` in place to meet the spec and every hard constraint |
| Verify | **Sonnet 5.5** (browser QA and visual review), **Haiku 5.5** (static and accessibility audit), **Sonnet 5.5** (data-preservation diff against the previous version) | Numbered findings with severity and fix |
| Refine | **Opus 5.5** | Fixes all high and medium findings and logs them in `CHANGELOG.md` |
| Re-verify | **Sonnet 5.5** | Confirms the fixes and reports anything remaining |

## 8. Deliverables
`index.html` pushed to `main` (GitHub Pages deploys it to https://omkarbhoite25.github.io/Periodic-Table/), an updated `CHANGELOG.md`, and before/after screenshots.
