# UI morph, one task: Fennick, skip the next box

Fennick is a fictional sparkling-tea shop made for omnigami's examples. One shape walks through one real job in its
shop: skipping the next box. Every morph is what the click before it opens. Square (1:1), 16 s, loops.

- **Film:** `index.html` (self-contained: `kit.js`, DM Sans and Bricolage Grotesque (both SIL Open Font License, in
  `assets/fonts/`), the shop's box render and its wordmark in `assets/art/`).
- **Evidence:** `capture/plan.json` captures the shop's own pieces in each state of the job (`capture/screens/`):
  the plan card with its two buttons, the date chooser, the skipped notice, the top bar's promise. Every piece the
  container becomes is drawn from these: words, icons, sizes by proportion, colours.
- **Length:** 16 s, 8 bars at 120 BPM; loops (the last frame is the first, pixel for pixel).
- **The grammar:** one container that never cuts, on a spring (280/19) with blur hand-offs; the cursor drives every
  change, with a press on every click and a hover on what it rests on; a caption per step in the shop's headline face
  (Bricolage Grotesque 800 at 84% width, as the shop sets its headlines); the size springs run in log space, so the
  wide chooser collapses into a round loader without passing through a tall pill; the loader and check; the two-edge
  indicator spring; the toast; the song.

## Steps

| Start (s) | Step | Caption | Container | Cursor and action |
|---|---|---|---|---|
| 0.00 | Brand | FENNICK wordmark | "Your box" button, ink pill 540 × 205 | rests in the corner |
| 1.00 | The question | **Plans changed?** | button | sets off 2.0, arrives 2.5, rests (button lightens) |
| 3.00 | Click "Your box" | | button sinks 4% and lightens | tap |
| 3.08 | The next box | **Skip the next box.** | card 1040 × 560: box photo, "Next box ships / Thu 12 Nov / 12 cans · every 4 weeks", [Skip a box] [Change flavours] | swish; read 3.6–5.5; sets off 5.5, arrives 6.0, rests (button washes) |
| 6.50 | Click "Skip a box" | | the ghost button sinks and fills | tap |
| 6.58 | Pick a date | **Pick a new date.** | paper pill 1191 × 169: 12 Nov (chosen) · 10 Dec · 7 Jan | pop; read 7.1–8.0; sets off 8.0, arrives 8.5, rests (segment washes) |
| 9.00 | Click "10 Dec" | | the ink indicator stretches across to 10 Dec; 12 Nov is struck through (9.1–9.3, revealed as the indicator leaves it) | tap; the cursor leaves for the corner (9.25–10.15) |
| 9.62 | Saving | (caption leaves) | ink circle 221, spinner (firmer spring, so it collapses without passing through a tall pill) | pop |
| 10.00 | Done | | check draws | pop; the song lands its hit here |
| 10.40 | The result | | toast, firmer spring (about 5% over): yuzu check, **Skipped. Next box ships 10 Dec.** (words from 10.53, once the pill fits them) | (holds 3.1 s) |
| 11.50 | The promise | **Skip, swap or pause any time.** | toast | |
| 13.50 | Brand | FENNICK wordmark | back to the "Your box" button | (holds 2.5 s to the loop) |

Holds: each caption lands and is read before the cursor moves; the cursor rests 0.5 s before each press; the
date choice shows 0.6 s before saving (the product working, so not held); the toast holds 3.1 s; the brand 2.5 s.

## Words and data

The captions say what the shop does for the viewer ("Skip the next box.", "Pick a new date.", "Skip, swap or pause
any time."); the sample data stays inside the shop's own pieces (the card, the dates, the toast).

All from the shop: order #10482, 12 cans every 4 weeks, next box ships Thu 12 Nov; skipping it moves the next one to
Thu 10 Dec. "Skip a box" and "Change flavours" are the order page's own buttons, with its icons. "Pick a new date" is
the chooser's own heading; 10 Dec skips one box and the shop says "Skipped. Next box ships 10 Dec.", the film's toast
word for word. "Skip, swap or pause any time" is the shop's own line (its top bar). "Your box" is the shop footer's
heading for these actions. Dates are written the shop's way ("12 Nov", not "Nov 12").

## Decided (the founder, 2026-10-25)

- **Story approved** ("UI morph looks good … story is approved").
- **The date chooser is in the shop** (order page): "Skip a box" opens "Pick a new date" with the next three ship
  dates; the film draws only what the shop has.
- **Length:** 16 s. **Shape:** square only.

## Render

From the skill's folder (or a project with `scripts/` and `music/` beside the film):

```bash
node scripts/render.mjs reference --size 1:1 --times key --sheet
node scripts/render.mjs reference --size 1:1 --review
node scripts/render.mjs reference --size 1:1 --check
node scripts/render.mjs reference --size 1:1 --stress
node scripts/render.mjs reference --size 1:1 --video --blur 4 --sound \
  --audio music/song.mp3 --bpm 120 --land 10 --poster 4.4
```

The song's stems (`music/song-stems/`) are found beside it; `--land 10` lands its hit on the check.
