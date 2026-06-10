# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Project Is

A battle-record tracker for three players: 牛 (Cow), 马 (Horse), and 太后 (Empress Dowager). It's a **single-file static SPA** with no build step — all logic lives in `index.html`, all data lives in `data.json`.

Deployed to GitHub Pages: https://liverpool1026.github.io/TheBattleOfCowHorse/

## Development

**No build tool.** Open `index.html` directly in a browser, or serve locally for live `data.json` updates:

```bash
python -m http.server 8000
# Visit http://localhost:8000
```

**Lint / Test / Build:** None. The only automated check is a GitHub Actions workflow (`.github/workflows/validate-data.yml`) that validates `data.json` on every PR.

**Validate data.json locally:**

```bash
python3 -c "
import json, sys
with open('data.json', encoding='utf-8') as f:
    data = json.load(f)
PLAYERS = {'牛', '马', '太后'}
errors = []
for i, row in enumerate(data):
    if not isinstance(row, list) or len(row) != 5:
        errors.append(f'Row {i+1}: expected 5 elements'); continue
    num, date, p1, p2, winner = row
    if p1 not in PLAYERS or p2 not in PLAYERS or winner not in (p1, p2) or p1 == p2:
        errors.append(f'Row {i+1} (game #{num}): invalid')
print(f'❌ {len(errors)} errors' if errors else f'✅ Valid — {len(data)} records')
[print(e) for e in errors]
sys.exit(len(errors) > 0)
"
```

## Architecture

### Data Format

`data.json` is a JSON array of 5-element arrays:

```json
[gameNumber, "DD/MM/YYYY", "Player1", "Player2", "Winner"]
```

Valid players: `"牛"`, `"马"`, `"太后"`. Winner must be Player1 or Player2.

### index.html Structure

All application logic is in `index.html` (~1300 lines). Key sections:

- **`DEFAULT_DATA`** — 162+ hardcoded games embedded as a JS array; used as offline fallback when `data.json` can't be fetched
- **`DATA`** — the live in-memory array; all mutations go here first
- **`rebuildAll()`** — master recalculate-and-render function; call after any data change
- **`calcStats()`** — computes per-player win/loss records, streaks, H2H records
- **`renderStats()` / `renderH2H()` / `renderCharts()` / `renderTable()`** — pure render functions
- **`setDirty(bool)`** — tracks unsaved state; shows/hides the "unsaved changes" banner
- **`createGamePR()`** — GitHub API integration: creates a branch, commits the new record, opens a PR
- **`loadedJSON`** — string snapshot of last fetched data; compared against `JSON.stringify(DATA)` to detect dirty state

### GitHub Constants (hardcoded)

```javascript
const GH_OWNER = 'liverpool1026';
const GH_REPO  = 'TheBattleOfCowHorse';
const GH_BASE  = 'master';
```

### CI Validation Rules

The workflow enforces exactly these constraints on every PR touching `data.json`:
1. Array length increases by exactly +1
2. Each row is `[number, "DD/MM/YYYY", player, player, winner]`
3. Players are from the valid set; players differ; winner is one of the two players

## Key Constraints

- **Do not add new players** without updating both the `PLAYERS`/`P` config in `index.html` and the validation in `validate-data.yml`.
- **CDN dependencies** (Chart.js 4.4.0, SheetJS 0.18.5) are loaded at runtime — no package manager.
- **GitHub token** for PR creation is stored in `localStorage` only; never write it to files or logs.
- The offline fallback (`DEFAULT_DATA`) should be kept in sync with `data.json` when doing significant updates, but is not required to be updated on every game add.
