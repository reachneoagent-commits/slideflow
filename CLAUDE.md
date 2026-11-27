<!-- Slideflow (rebrand/apply.py) -->
# Slideflow

This repository is **Slideflow**, a fork of DeckCraft. Read `docs/UPSTREAM.md` first. In short:

- Never hand-edit a file that came from upstream to change branding, ids, links or icons: add the
  change to `rebrand/brand.json` (or a patch in `rebrand/patches/`) and run `python3 rebrand/apply.py`,
  so it survives the next upstream merge.
- Slideflow's own files are `rebrand/`, `brand/`, `docs/UPSTREAM.md`, `README.md`,
  `assets/header-*.png` and `.github/workflows/release.yml` / `windows-release.yml`.
- Crate, binary and environment-variable names stay `deckcraft*` / `DECKCRAFT_*`.

@AGENTS.md
