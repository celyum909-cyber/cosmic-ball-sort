# Cosmic Ball Sort

A single-file, space-themed ball-sorting puzzle. Pour balls between tubes until each tube holds a single color. Completed tubes detonate and leave the board, chaining clears together builds a combo multiplier, and your score runs across every level with a persistent all-time high.

Everything — markup, styles, game logic, sound, and visual effects — lives in one self-contained `cosmic-ball-sort.html`. No build step, no dependencies, no network calls. Open the file in any modern browser and play.

## How to play

- Tap a tube to pick up the top group of matching balls, then tap another tube to pour them.
- A ball can move onto an empty tube, or onto a tube whose top ball is the same color.
- Fill a tube completely with one color to clear it.
- Clear every color to win the level.
- In **Mystery mode**, only the top ball of each tube glows; the colors beneath are hidden until you uncover them, so you have to dig and remember.

## Controls

| Control | What it does |
| --- | --- |
| Tap tube | Select / pour balls |
| Undo | Step back a move (limited uses per level; refunds score) |
| Add tube | Drop in one extra empty tube (limited uses per level) |
| Restart | Rebuild the current level from its starting layout |
| Home (menu) | Pause, view scores, start a new game |

## Scoring & combos

Clearing a tube is worth points, and clearing tubes in quick succession chains them into a combo.

- **Combo window** — after a clear, you have **5 seconds** to clear another tube and extend the streak. A live meter under the stats bar shows the multiplier (`×2`, `×3`, …) and a bar that drains as the window runs out, turning red in the final stretch.
- **Exponential payoff** — each chained clear doubles the previous one: `+100`, `+200`, `+400`, `+800`, `+1600`, and so on. Breaking the chain resets you to `×1`, so setting up several completions to fire back-to-back is where the big scores come from.
- **Escalating feedback** — higher streaks make the detonation bigger and brighter, pitch the boom up a step, add a rising combo ding, kick in a stronger screen shake, and float a `×N COMBO` callout off the tube.

### Score readouts

- **Score** (gold) — points earned on the current level. Resets each level.
- **Total** (cyan) — the running total across every level in the current run. Carries forward as you advance.
- **High score** — your best-ever run total, shown on the menu. Saved between sessions.

Undo refunds both the level score and the running total. Restarting or replaying a level removes that level's points from the total first, so re-clearing it never double-counts. The saved high score only ever ratchets upward — undo and restart can't lower it.

## Runs & the New Game button

A **run** is a continuous playthrough that begins at level 1 and accumulates a single growing total as you clear levels via **Next level**.

- Your all-time **high score** persists across runs and browser sessions.
- **New game** (in the menu) starts a fresh run from level 1 with the total reset to zero, while keeping your saved high score. It uses a two-tap confirm — the button turns red and asks you to tap again — so you can't wipe a good run by accident.

## Winning a level

The win screen shows the level score, run total, moves, and time, plus a 1–3 star rating based on how efficiently (in moves) you solved it. If the run beat your saved record, a **★ New High Score!** badge appears.

## Visual & audio effects

- **Tube detonation** — a completed tube charges up, then bursts in a color-matched supernova (core flash, expanding shockwave ring, flung ball fragments, cosmic sparks) and is removed from the board. Because clears remove tubes, the board reflows and the remaining tubes grow as it empties.
- **Combo crescendo** — the blast, sound, and shake all scale with the streak.
- **Starfield & planets** — an animated cosmic backdrop, plus win confetti.
- All effects honor the system **reduced-motion** setting, dialing down or simplifying animation when requested.

## Technical notes

- **One file, zero dependencies.** Pure HTML/CSS/JS in a single document.
- **Rendering.** The board is plain DOM; particle effects (detonations, confetti) and the starfield draw to their own `<canvas>` layers.
- **Sound.** Generated live with the Web Audio API — no audio files. Audio unlocks on first interaction and can be toggled off in the menu.
- **High-score persistence.** Stored in the browser via `localStorage`, wrapped in a safe fallback: if storage is blocked (for example inside a sandboxed preview frame), the game keeps the score in memory for the session instead of erroring, so it never breaks. True cross-session persistence works when you open the downloaded file in a normal browser.
- **Level generation.** Levels are generated to be solvable, with difficulty scaling by level number.

## File

- `cosmic-ball-sort.html` — the complete game. Double-click to play.
