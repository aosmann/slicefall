# Slicefall

Educational fruit slicer for the EduGames portal. A question sits at the top; its three answers fly up from the bottom as fruit. Swipe through the right one. The wrong ones are bombs in disguise.

- Right slice: +1 (×2 from 3 in a row, ×3 from 5 in a row), juicy split, next question
- Wrong slice: the fruit turns into a bomb and you lose a life
- Right fruit falls back down unsliced: you lose a life
- 3 lives; the run ends when they run out or the clock hits zero
- Chess clock, picked on the topic screen. Everyone starts with 10 s:

  | Clock | Start | Right | Wrong / dropped |
  |---|---|---|---|
  | Quick | 10 s | +1 s | −1 s |
  | Normal (default) | 10 s | +2 s | −2 s |
  | Relaxed | 10 s | +3 s | −2 s |

  The clock only runs while fruit are in the air, so the slice and splat animations don't eat anyone's time. It can't hold more than 15 s, and the bonus shrinks by 0.5 s for every 8 right answers (never below 0.5 s), so strong players get long runs that still end. Under 5 s it shows tenths and ticks; every +/− flashes under the timer.
- The fruit fly 2% faster with every question, up to 1.5×
- Every 8 questions a frenzy wave: two questions at once, colour-coded A / B
- Harder levels: shorter air time, higher arcs, wider spread, paths that cross
- No question repeats in a run. If a player answers every question a topic has, the run ends as "Topic cleared"
- Record kept per topic, difficulty and clock

Plain canvas 2D, no build step, works offline after the first visit, installs to the home screen. Portrait first, works on laptops with mouse drag.

## Files
- `index.html`: the game (canvas board, fruit, swipe input, menus, audio, scoring, PORTAL EMBED block)
- `questions.js`: the shared EduQ question bank (v2), byte-identical to Lanefall and Stackfall. Do not edit here.
- `game.json`: portal metadata and teacher settings (level, time)
- `sw.js`, `manifest.webmanifest`, `icon-*.png`: offline support and install

## Portal
Follows the EduGames game contract v1: `?topic=<id>&level=1-3&clock=quick|normal|relaxed&lock=1` starts a run at once; posts `edu-ready`, `edu-progress` after every answer and `edu-result` at the end (also kept in `localStorage['edu-results']`). The result adds `clock`, `livesLeft`, `timeUsed` and `duration` (seconds the clock actually ran), `cause` (`time` / `lives` / `done` / `quit`) and `frenzies`; `missed[].picked` is the sliced answer or `"missed"` for a dropped fruit.

`?debug=1` exposes a read-only `window.SF` hook used by the automated tests.
