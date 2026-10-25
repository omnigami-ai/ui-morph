# Reference spec: Fennick, skip the next box

The reference film's tables as its code holds them (`reference/index.html`), so an adaptation can see what moves
together. The story in words is `reference/STORY.md`; the grammar and its numbers are `style.md`.

## Format

1440 × 1440, 60 fps, 16.0 s (960 frames), loops (the last frame is the first). 120 BPM, 8 bars. Square only.

## The times (`T`)

| Key | t (s) | What |
|---|---|---|
| `ask` | 1.00 | caption 1 |
| `open` | 3.00 | click 1: the button opens the card (morph at 3.08) |
| `skip` | 6.50 | click 2: the card's "Skip a box" opens the chooser (morph at 6.58) |
| `pick` | 9.00 | click 3: 10 Dec |
| `save` | 9.62 | the chooser collapses into the loader |
| `done` | 10.00 | the check (the song's landing) |
| `toast` | 10.40 | the result |
| `promise` | 11.50 | caption 4 |
| `close` | 13.50 | back to the button and the wordmark |

## The container (`BOX`: t, w, h, radius, lum, cx, cy, [spring])

| Row | t | w × h | Radius | Lum | Spring |
|---|---|---|---|---|---|
| 0 button | 0 | 540 × 205 | pill | 0.03 | 280/19 |
| 1 card | 3.08 | 1040 × 560 | 64 | 0.03 | 280/19 |
| 2 chooser | 6.58 | 1191 × 169 | pill | 1 | 280/19 |
| 3 loader | 9.62 | 221 × 221 | pill | 0.03 | 280/27 |
| 4 check | 10.00 | 230 × 230 | pill | 0.03 | 280/19 |
| 5 toast | 10.40 | from its words × 180 | pill | 0.03 | 280/25 |
| 6 button | 13.50 | 540 × 205 | pill | 0.03 | 280/19 |

All centred at (720, 791). Content (`CONTENT`): button, card, chooser, loader, check, toast (its words wait 0.13 s),
button, each from its row's time.

## Captions (`CAPTIONS`: start, field, the height of its state)

| Start | Words | Sits above |
|---|---|---|
| 0 | the wordmark | button (205) |
| 1.00 | `ask`: "Plans changed?" | button (205) |
| 3.08 | `step1`: "Skip the next box." | card (560) |
| 6.58 | `step2`: "Pick a new date." | chooser (169) |
| 9.62 | none (the caption leaves as the loader comes) | |
| 11.50 | `promise`: "Skip, swap or pause any time." | toast (180) |
| 13.50 | the wordmark | button (205) |

## The cursor (`CUR`: arrival, x, y, the row it works on) and its clicks

| Arrives | Point | On | Then |
|---|---|---|---|
| 0, 2.0 | 1268, 1150 | its corner | sets off at 2.0 |
| 2.5 | 838, 824 | button | rests; the button lightens (hover from 2.5); click at 3.0 |
| 5.5 | (held) | | sets off at 5.5 |
| 6.0 | 613, 986 | card ("Skip a box") | rests; the ghost button washes (hover from 6.0); click at 6.5 |
| 8.0 | (held) | | sets off at 8.0 |
| 8.5 | 790, 822 | chooser (10 Dec) | rests; the segment washes (hover from 8.5); click at 9.0 |
| 9.25 → 10.15 | 1268, 1150 | its corner | stays to the loop |

`CLICKS` = 3.0, 6.5, 9.0: each a press of the pressed piece and of the cursor (`env`). The hover times (2.5, 6.0,
8.5) are written in `box()`, `C.card` and `C.chooser`: they are the cursor's arrivals and move with them.

## Words (`DEFAULTS` and `FIELDS`, editable in the preview)

| Field | Default | Max |
|---|---|---|
| `button` | Your box | 12 |
| `ask` | Plans changed? | 22 |
| `step1` | Skip the next box. | 22 |
| `step2` | Pick a new date. | 22 |
| `toast` | Skipped. Next box ships 10 Dec. | 34 |
| `promise` | Skip, swap or pause any time. | 30 |

The card's words and the dates (`CARD`, `DATES`) are sample data from the shop, not fields.

## Sound (`cues()`)

| t | Sound | Gain |
|---|---|---|
| 3.00, 6.50, 9.00 | tap | 0.65 |
| 3.08 | swish (the card opening) | 0.32 |
| 6.58, 9.62, 10.00, 10.40, 13.50 | pop | 0.40 (after the song lands at 10, left out) |

Render: `--audio music/song.mp3 --bpm 120 --land 10 --sound --blur 4`; poster at 4.4 s (the card and its caption).

## Review times (`keyTimes`)

0.5, 1.3, 1.9, 2.6, 3.0, 3.25, 4.4, 6.1, 6.5, 6.75, 7.6, 8.7, 9.05, 9.4, 9.75, 10.15, 10.55, 11.2, 11.75, 12.8, 13.65,
14.6, 15.9: inside every state and around every event.
