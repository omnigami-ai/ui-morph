# Remake spec: @twoclipping's UI morph → Fennick (a fictional company)

Reference: https://x.com/twoclipping/status/2103273003555402193 (local copy
`reference/motion/twoclipping-ui-morph.mp4`, not committed). Made in code by
Opus 5.5 from the creator's published prompt. Measured with
`tools/study/container.py` (container box per frame at 60 fps) and on
full-resolution stills of every state.

## Format
1440 × 1440, 60 fps, 14.0 s (840 frames), loops (last frame = first).
120 BPM: a beat every 0.5 s, something changes on every beat.
Canvas `rgb(233,235,230)`, a faint lighter centre. Black and white UI, Geist.
One container, never cut, morphing size, radius and colour on springs with a
tiny overshoot; content swaps with a short blur; a cursor drives every change.

## States (on-screen box at 1440 px; t = when the morph into it starts)

| t (s) | Reference | Box w × h, radius | Fennick |
|---|---|---|---|
| 0.00 | Generate button | 641 × 205, pill, black | Build your box |
| 0.55 | loader (click at 0.50) | 221 circle | loader |
| 0.93 | check draws | 230 circle | check |
| 1.27 | dynamic island: art + waveform | 863 × 219, pill | the Yuzu & Fennel can on its colour + rising bubbles |
| 1.80 | player (click at 1.73) | 996 × 633, r 67 | box card: Yuzu & Fennel, Box #10482, its delivery week |
| 2.33, 2.70 | pause → play → pause | | pause / resume the box |
| 2.80–3.57 | scrub the progress bar | | scrub from Packed through Shipped to Delivered |
| 3.72 | volume slider | 1075 × 185, pill | fizz level (bubbles appear as it rises) |
| 4.13–4.77 | drag down, then up past max | stretches to 1166 wide, left edge fixed | same |
| 5.10 | release, springs back | | |
| 5.27 | toggle (on) | 490 × 274, pill | toggle |
| 5.55 / 5.85 / 6.10 | flips off / on / off | off = grey track | same |
| 6.27 | tabs, knob becomes indicator | 1191 × 169, white pill | Day / Week / Month |
| 6.80, 7.07 | Week, Month (edges on different springs) | | same |
| 7.27 | chart opens | 1099 × 843, r 44, white | cans shipped, 1,284 |
| 7.47–8.00 | count up, line draws | | |
| 7.87–8.80 | tooltip scrub | | |
| 9.17 | click Week: counts down, curve reshapes | | 312 |
| 9.73 | search pill | 871 × 210, r 59, white | "Find a flavour" |
| 10.07 | command palette | 1039 × 813, r 35 | Add Yuzu & Fennel, Download receipt, Skip a box, Track order #10482, Build your box |
| 10.53–10.90 | type "frame", list filters | 1243 × 571, r 41 | type "box" |
| 11.30–11.53 | hover, select (row turns black), enter | | Build your box |
| 11.77 | toast with check | 965 × 180, pill, black | Tea, but it fizzes. |
| 12.57 | back to the button | 641 × 205 | Build your box |
| 14.00 | loop | | |

## Keep / change
Keep: every box, radius, colour, time, spring, cursor path, blur swap.
Change: words, icons, the art tile (Fennick's can on its yuzu colour), the ink and paper (Fennick's), data.
