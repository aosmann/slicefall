# Slicefall

Educational fruit slicer for the EduGames portal. A question sits at the top; its three answers fly up from the bottom as fruit. Swipe through the right one. The wrong ones are bombs in disguise.

- Right slice: +1 (×2 from 3 in a row, ×3 from 5 in a row), juicy split, next question
- Wrong slice: the fruit turns into a bomb and you lose a life
- Right fruit falls back down unsliced: you lose a life
- 3 lives; the run ends when they run out or the timer ends
- Every 8 questions a frenzy wave: two questions at once, colour-coded A / B
- Harder levels: shorter air time, higher arcs, wider spread, paths that cross
- Record kept per topic, difficulty and time limit

Plain canvas 2D, no build step, works offline after the first visit, installs to the home screen. Portrait first, works on laptops with mouse drag.

## Files
- `index.html`: the game (canvas board, fruit, swipe input, menus, audio, scoring, PORTAL EMBED block)
- `questions.js`: the shared EduQ question bank, byte-identical to Lanefall and Stackfall. Do not edit here.
- `game.json`: portal metadata and teacher settings (level, time)
- `sw.js`, `manifest.webmanifest`, `icon-*.png`: offline support and install

## Portal
Follows the EduGames game contract v1: `?topic=<id>&level=1-3&time=60|90|120&lock=1` starts a run at once; posts `edu-ready`, `edu-progress` after every answer and `edu-result` at the end (also kept in `localStorage['edu-results']`). The result adds `livesLeft`, `timeUsed`, `duration`, `cause` (`time` / `lives` / `quit`) and `frenzies`; `missed[].picked` is the sliced answer or `"missed"` for a dropped fruit.

`?debug=1` exposes a read-only `window.SF` hook used by the automated tests.
