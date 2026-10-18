# Periodic Table for Space

An interactive periodic table built for people planning space missions. It shows which elements matter off-Earth, where in the solar system they are found, and what missions use them for.

- **Lenses**: cosmic abundance, where to find it (Moon, Mars, asteroids), mission role, nucleosynthesis origin, supply risk
- **Mission builder**: pick Lunar base, Mars sample return, Asteroid mining or Deep-space probe to see which elements it needs and whether they can be sourced in situ
- **Animation**: a WebGPU nebula background in the dark theme (via [Shaders](https://shaders.com), MIT, vendored in `vendor/shaders/`) with a 2D starfield fallback, elements that condense into place in order of origin, electron-shell orbits in the detail panel (respects `prefers-reduced-motion`)

A single self-contained `index.html` with no build step. `.github/workflows/pages.yml` deploys it to GitHub Pages on every push to `main`.

See [`PROMPT.md`](PROMPT.md) for the full brief and the multi-agent build process.
