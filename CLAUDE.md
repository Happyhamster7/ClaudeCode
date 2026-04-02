# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Single-file browser game (`gomoku.html`). No build system, no dependencies, no package manager. Open the file directly in a browser to run it.

## Architecture

Everything lives in `gomoku.html` — HTML, CSS, and JavaScript in one file.

**Game state** (global variables): `board` (15×15 2D array, 0=empty/1=black/2=white), `turn`, `gameOver`, `history` (move stack for undo), `mode` (`'2p'`, `'ai-easy'`, `'ai-hard'`).

**Rendering**: Canvas-based. `draw()` redraws the full board from scratch on every update. `drawStone()` handles individual stones with radial gradients and marks the last move.

**Win detection**: `checkWin(r, c, player)` checks all 4 directions from the last placed stone, returns the winning 5-cell array or null.

**AI** (`aiMove`, `evalCell`, `scoreDir`): Greedy one-ply heuristic. Scores candidate cells near existing stones by counting consecutive pieces in each direction, balancing attack vs defense with a weighted sum. Hard mode uses less randomness (±5) than Easy (±30).

## Git & GitHub workflow

Every project (including this one) must be version-controlled on GitHub. Follow this for all work:

**For this repo:** `Happyhamster7/ClaudeCode` on `origin/master`

**For every new project:**
1. Create a new folder on the Desktop for the project
2. `git init` inside it
3. Create a `.gitignore` (OS files, editor files, `.claude/settings.local.json`)
4. Make an initial commit with all starting files
5. `gh repo create <ProjectName> --public --source . --remote origin --push` to create and push to a new GitHub repo under `Happyhamster7`

**After every significant change:**
1. Stage the changed files by name (not `git add -A`)
2. Commit with a clean, descriptive message explaining what changed and why
3. Push to GitHub immediately — `git push`

The goal is always having a saved version on GitHub so any change can be reverted.
