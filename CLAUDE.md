# Escher

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

## Data-First Protocol
When answering questions about data, facts, documents, conversations, or history:
1. **Query the vector DB first.** Use `devctl search "query"` or direct Qdrant search before answering from memory or general knowledge. The DB has 2M+ vectors across legal docs, chats, sessions, and facts.
2. **Know the search scopes.** `devctl search` defaults to ingested docs, court files, facts, and algorithms — AI-assistant chats are excluded (they carry questions and assertions, not ground truth). Use `--claude` for AI chat history (Claude Code, Claude.ai, ChatGPT), `--facts` for the fact registry / case facts, `--algos` for algorithms, `--all` to include everything.
3. **Cite the source.** Include collection name, confidence level, and date when referencing DB results.
4. **Distinguish confidence levels.** A bank statement (verified) is not the same as an email claim (asserted). Never present asserted facts as verified.
5. **Log new facts.** When you discover or confirm a fact during work, log it: `devctl log-fact --fact "..." --source-type X --confidence Y --domain Z`

## Agent rules
- This is a fork — preserve attribution and license
- The math is correct and well-tested — do not simplify hyperbolic geometry computations without verification
- Module includes doctests: run with `python escher.py`
- Do not commit .env or secret files
