# Pulse · AI Daily

A personal daily AI briefing, rebuilt every night at **2 AM Toronto time** by a scheduled Claude task and published with GitHub Pages.

**Health & regulation sections** (3 picks each, with a plain-language summary):
- AI in Cardiac Surgery, Robotics & AI Models
- AI in Healthcare Management
- Pharmaceutical Regulation
- Medical Devices

**AI News:** AI agents · new models · fun AI news

## How it works
1. The scheduled task follows `DIGEST_INSTRUCTIONS.md` — it searches the web, picks items and writes summaries.
2. It saves the issue as JSON in `docs/data/` (`latest.json` plus a dated copy in `archive/`) and pushes to `main`.
3. GitHub Pages republishes `docs/` automatically.

To change topics, sources or style, edit `DIGEST_INSTRUCTIONS.md` — the next night's run uses the new version.

Inspired by [ell-hosse/AI-Daily](https://github.com/ell-hosse/AI-Daily); site and theme written from scratch.
