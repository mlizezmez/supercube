# Square Quest

A tiny NES-style platformer in **one HTML file** — no build step, no dependencies, no assets.
Title screen → scrolling world map → levels → score tally, with a 16-colour palette, auto-tiled
terrain, SMB1-style wall edge-lock, secret exits and on-screen touch controls for phones.

| Title | World map | Level |
|---|---|---|
| ![Title](docs/title.png) | ![Map](docs/map.png) | ![Level](docs/level.png) |

| Sky theme | Mobile |
|---|---|
| ![Sky](docs/sky-level.png) | ![Mobile](docs/mobile.png) |

## Play

Open `index.html` in any modern browser. That's it.

Or host it for free with **GitHub Pages**: *Settings → Pages → Deploy from a branch → `main` / root*.
Your game will be live at `https://<your-username>.github.io/<repo-name>/`.

## Controls

| Action | Keyboard | Touch |
|---|---|---|
| Move | Arrow keys (or WASD) | D-pad |
| Jump (hold = higher) | Space / Z / Up (W) | **A** |
| Run | X / Shift | **B** |
| Drop through thin platforms | Down + Jump | D-pad down + **A** |
| Confirm / play level | Space / Z / Enter | **A** |
| Back to map / title | Esc | **BACK** |
| Start (title) | Enter (Space / Z also work) | **START** |
| Mute | M | **MUTE** |
| Colour / face (title) | C / F | **COLOR** / **FACE** |
| Swap Arrows ↔ WASD (title) | T | — |
| Reset save (title) | R | — |
| Debug overlay | D (F3 or ` in WASD mode) | — |

Touch controls appear automatically on phones and tablets and are multi-touch (hold right + B to run).
The D-pad is a single control, so you can slide your thumb between directions.

## Rules

- Collect **40 %** of a level's coins to unlock the exit.
- Silver stars at **60 / 80 / 90 %**, a gold star at **100 %**.
- `%` tiles are **secret exits**; they can reveal hidden levels on the map.
- Progress is saved in your browser's `localStorage` (key `squareQuestSave`). Press **R** on the title screen to wipe it.

## Making levels and worlds

Everything lives in `index.html`; the code is commented for beginners. Search for the `=====` banners:

1. CONSTANTS · 2. ASSET / TILE RENDERER · 3. INPUT HANDLER (3b: touch) · 4. GAME STATES · 5. PHYSICS & COLLISION · 6. MAIN LOOP

Levels are plain text, one character per tile (15 rows; shorter levels are padded at the top):

| Char | Meaning | Char | Meaning |
|---|---|---|---|
| `.` | empty | `o` | coin |
| `#` | solid ground (auto-tiled) | `e` | enemy |
| `B` | brick | `S` / `E` | start / exit |
| `-` | one-way thin platform | `%` | secret exit |
| `^` | floor spikes | `v` | ceiling spikes (need `#`/`B` above) |

Themes: `day`, `cave`, `castle`, `sky`, `pine` (unknown names fall back to `day` with a console warning).

World-map nodes (`start`, `level`, `warp`, `goal`) are connected with `links`. Optional settings include
`after` (unlock when any listed node is beaten; `'2-A@100'` requires 100 % coins), `secret` / `secretExit`
(reveal a hidden node), `linkGates` (paths that only appear on a condition) and `warpTo`.
See the large comment above `WORLDS` in `index.html` for worked examples.

## Project layout

```
index.html   the whole game
docs/        screenshots used in this README
```

## Tips

- Press **D** in-game for the debug overlay (position, velocity, ground, wall-lock state, coin count).
- Open the browser console: level-data mistakes are reported as warnings with the offending level id.

## License

No licence has been chosen yet. Add a `LICENSE` file (e.g. MIT) before sharing the code publicly if you want others to reuse it.
