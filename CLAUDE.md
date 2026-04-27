# Escher

> Read `INTENT.md` before acting. It governs all work in this repo.

**Runtime:** Python 3.12+
**Package manager:** uv
**Status:** active

## Overview
Generates Escher-like tilings of the Poincare disk model of hyperbolic geometry. Given a triangle satisfying `1/p + 1/q + 1/r < 1`, fills the disk with reflected copies of user-supplied images using Moebius transformations.

## How to run
```bash
uv run python escher.py              # generate default tiling
uv run python escher.py --help       # see all options
```

## Key files
- `escher.py` — complete implementation: hyperbolic triangle construction, Moebius transformations, pixel reflection, image generation

## How it connects
- Output published to jthorvaldur.github.io
- Uses mathematical symmetry groups (connects to D.72 coherence geometry)

## Origin
Original author: Balazs Strenner, UW-Madison Mathematics (C++ 2006, Python rewrite 2014). Forked by Joel Thorarinson. GPL licensed.

## Agent rules
- This is a fork — preserve attribution and license
- The math is correct and well-tested — do not simplify hyperbolic geometry computations without verification
- Module includes doctests: run with `python escher.py`
- Do not commit .env or secret files
