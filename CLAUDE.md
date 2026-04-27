# CLAUDE.md — Escher

**Runtime:** Python 3.12+
**Package manager:** uv
**Status:** active

## What this is
Generates Escher-like tilings — mathematical art from symmetry groups. Produces SVG tessellations with configurable symmetry, color, and transformation parameters.

## How to run
```bash
uv run python escher.py              # generate default tiling
uv run python escher.py --help       # see all options
```

## How it connects
- Output published to jthorvaldur.github.io
- Uses mathematical symmetry groups (connects to D.72 coherence geometry)

