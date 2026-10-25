# UI morph: style

Style inspired by [@twoclipping's UI-morph video](https://x.com/twoclipping/status/2103273003555402193): one container
that never cuts, on springs, driven by a cursor at 120 BPM. This skill tells that grammar as one real job in the
product. Every number below is measured from `reference/index.html` (Fennick, 1440 × 1440, 60 fps, 16 s).

## The grammar

- **One job, one shape.** One real task in the product, done once, in its own order, ending on its real result. The
  container is every piece of it in turn: a button, the card that button opens, the control on that card, the product
  working, done, its result. No cuts, no second shape, nothing changes that the cursor didn't cause (except the loader,
  the check and the result arriving).
- **Each morph is what the click before it opens.** The button you press becomes the card it opens; the card's button
  becomes the control it opens; the choice becomes the saving. A piece never appears that the last click wouldn't have
  shown in the product.
- **The product's own pieces,** drawn from captures of each state (`reference/capture/`): its words, icons, colours,
  radii, weights and order. The container's two ends are the product's ink and paper; its brand colour is the one
  accent, where the product uses it (Fennick: yuzu, on the result's check).
- **A caption per step,** above the container, in the product's headline face: what the product does for the viewer
  at this step ("Skip the next box.", "Pick a new date."), never the sample data. The sample data lives inside the
  pieces (the card's date, the chooser's dates, the toast).
- **Breathing room.** Each caption lands and is read before the cursor sets off; the cursor rests on its target before
  it presses; the result holds long enough to read twice; the brand holds to the loop.
- **Loops pixel for pixel.** The last frame is the first: the brand, the button, the cursor in its corner.

## The beat grid (120 BPM: a beat 0.5 s, a bar 2 s; 16 s = 8 bars)

| t (s) | Beat | What | Hold |
|---|---|---|---|
| 0.00 | brand | wordmark above the button; cursor in its corner | 1 s |
| 1.00 | question | caption 1 (the viewer's need: "Plans changed?") | read 1 s, then the cursor sets off (2.0), arrives (2.5), rests 0.5 s |
| 3.00 | click 1 | the button opens the product's card | |
| 3.08 | step 1 | caption 2 with the card | read ~2 s (3.6–5.5); sets off 5.5, arrives 6.0, rests 0.5 s |
| 6.50 | click 2 | the card's button opens its control | |
| 6.58 | step 2 | caption 3 with the control | read ~1 s (7.1–8.0); sets off 8.0, arrives 8.5, rests 0.5 s |
| 9.00 | click 3 | the choice is made in the control | the choice shows 0.6 s; the cursor leaves for its corner (9.25–10.15) |
| 9.62 | working | the control collapses into the loader; the caption leaves | none (the product's own working is never held) |
| 10.00 | done | the check draws; **the song lands its hit here** (`--land 10`) | |
| 10.40 | result | the product's own result message (the toast) | 3.1 s |
| 11.50 | promise | caption 4: the product's promise in its own words | 2 s |
| 13.50 | brand | the toast becomes the button again; the wordmark | 2.5 s to the loop |

A morph starts 0.08 s (`LAG`) after the click that opens it. Clicks and landings sit on beats (3.0, 6.5, 9.0, 10.0);
the product's working (9.62) and its result (10.4) follow the product, not the grid. A job with more or fewer steps
adds or removes whole bars (2 s) and keeps the holds; the song still lands on the check.

## The container (at 1440 px)

| Row | State | Box | Radius | Fill (lum: 0 ink … 1 paper) | Spring |
|---|---|---|---|---|---|
| 0 | button | 540 × 205 | pill | ink (0.03) | 280/19 |
| 1 | card | 1040 × 560 | 64 | ink | 280/19 |
| 2 | control (the date chooser) | 1191 × 169 | pill | paper (1) | 280/19 |
| 3 | loader | 221 circle | pill | ink | 280/27 (a big collapse: firmer, stays a circle) |
| 4 | check | 230 circle | pill | ink | 280/19 |
| 5 | toast | its words' width × 180 | pill | ink | 280/25 (a big growth: about 5% over) |
| 6 | button | as row 0 | pill | ink | 280/19 |

- **Springs:** `kit.spring`, stiffness 280, damping 19 (an overshoot of about a tenth of the change, settled in about
  0.4 s). Width and height ride it **in log space** (`logTrack`): a change overshoots by a share of itself, so a wide
  pill collapsing to a circle never passes through a tall pill on the way. Radius, centre and fill ride it linearly;
  the fill (lum) on 800/57, which doesn't overshoot. A row can set its own spring (rows 3 and 5).
- **The toast's width** comes from its words: `max(720, 155 + text width + 86)` at DM Sans 500 45 px.
- **Layout:** the caption, a 104 px gap and the container are centred as a group (`GROUP` 712, caption height 53), so
  the container keeps one centre (y 791) and each caption sits 104 px above its own state's top edge.
- **Shadow:** black at 0.10 (paper) to 0.24 (ink), blur 70, 26 px down.
- **Ground:** the product's paper a shade deeper (Fennick `#EFE7DA`), a little lighter in the middle (white at 0.35
  fading over 1000 px, centred 72 px above the middle).

## Hand-offs

- **Content:** the outgoing piece blurs and fades out over 0.08 s as the morph starts; the incoming comes in from a
  14 px blur over 0.14 s, from 0.05 s after (the toast's words wait 0.13 s, until the pill is nearly wide enough, so
  they never come into focus clipped). Content is clipped to the live container.
- **Captions:** each word rises 22 px and comes into focus from a 10 px blur over 0.36 s, from 0.14 s after its step,
  0.05 s after the word before it (ease out). A caption leaves all at once over 0.14 s (up 10 px, blurring 8 px) as the
  next arrives, keeping its gap above the container's live top edge, so a growing card pushes it up instead of
  running over it. At 80 px, -2% tracking, shrunk to fit 1240 px wide. The wordmark (420 px wide, its letters' middle
  on the caption line) is the first and last caption.

## Presses and hovers

- **Every click has a press,** on one curve (`env`): down over 0.05 s from 0.03 s before the click, held, back over
  0.16 s from 0.07 s after. What's pressed sinks 4%. The container button lightens (+0.06 lum); a ghost button on the
  card fills (paper at 0.10); a segment of the control washes darker (ink at 0.06).
- **The cursor presses too,** on the same curve: it shrinks to 0.86 and comes back, never in one frame.
- **Hover:** what the cursor rests on answers over 0.15 s from 0.05 s before it arrives: the button lightens (+0.025
  lum), the ghost button washes (paper at 0.08), the segment washes (ink at 0.05). It clears as the click's morph
  begins.

## The cursor

- An arrow 34 × 53 px at 1440: ink, a 5 px paper outline, a soft shadow (black 0.3, blur 10, 4 px down).
- It rests in a corner of the frame (1268, 1150) when it isn't working, glides to each target in 0.5 s
  (`1 - (1 - p)^3.2`: starts straight off, lands soft), rests 0.5 s, presses, and leaves for its corner after the last
  click. Its tip sits on the target's lower part, beside the words, never over them.
- Each point names the box row it works on (`CUR`), so it lands on the piece wherever that piece is.

## The pieces (Fennick's, as an example of the measure)

- **Card:** a 250 px sand tile (radius 48, 60 px in) with the product's photo at 82% of its height; a text column
  48 px right of it: eyebrow DM Sans 500 38 (dim), title 600 64 (paper), detail 400 38 (dim), centred on lines 48, 124
  and 200 px below the tile's top. Two buttons along the bottom (112 tall, 60 px in, 24 apart): the ghost one outlined
  3 px in paper, the filled one paper with ink words; labels 600 38 with the product's 40 px icons (stroke 1.75 on 24),
  18 px apart.
- **Control (segmented):** inset 13 px, three equal segments, labels 600 47. The ink indicator moves on two springs:
  the leading edge stiff (440/24), the trailing soft (170/16), so it stretches as it travels and settles (for a move
  to the left, swap them). The skipped date is struck through (5 px grey line over 0.2 s from 0.1 s after the click,
  revealed as the indicator leaves it) and greys as the product greys a struck date.
- **Loader:** an arc at 0.2 of the circle's size, 0.05 thick, turning 9.5 rad/s, its span breathing (π × 1.15–1.5).
- **Check:** two strokes (0.075 of the circle thick) drawing over 0.2 s (expo out) from 0.04 s.
- **Toast:** the brand colour's disc (radius 29, 90 px in) with an ink tick drawing over 0.22 s from 0.18 s; the
  result's words in DM Sans 500 45, 36 px after the disc.

## Type

The product's UI face for its pieces (the reference: DM Sans); its headline face for the captions (the reference:
Bricolage Grotesque 800 at 84% width, as the shop sets its headlines). Centre every label on its capitals
(`kit.centreText`), never `textBaseline = 'middle'`.

| Where | Size | Weight |
|---|---|---|
| caption | 80 (shrinks to fit 1240 px) | the headline face, 800 |
| button label | 55 | 600 |
| card eyebrow / title / detail | 38 / 64 / 38 | 500 / 600 / 400 |
| card buttons | 38 | 600 |
| control labels | 47 | 600 |
| toast | 45 | 500 |

Nothing under 28 px at 1440 (about the limit on a phone); the reference's smallest is 38. Cut words before shrinking
anything.

## Shape

Square only: 1440 × 1440 (`SHAPES` has one entry, `1:1`). The reference lays out no wide or tall frame.

## Sound

- **Effects** on each visual onset: a `tap` on every press (gain 0.65), one quiet `swish` as the card opens (the one
  big growth, 0.32), a soft `pop` as each other state lands (0.4). No riser, no accent. Effects from the kit
  (`scripts/sounds/kit.json` says what each is for); retiming a beat retimes its cue.
- **The song** (`music/song.mp3`, glossy, bouncy synth-pop at 120 BPM, made for this skill): `song.mjs` starts it on a
  bar line, lands one hit on the check (`--land 10`), where the drums stop (from its stems) and the rest closes and
  fades. Once it lands, the result's pops are left out. Effects sit 6 dB under it; mastered around −14 LUFS.
- **`--music`** gives a synthesised 120 BPM bed instead (`music.style`: `'organic'` for plants, food and drink,
  `'synth'` for software and tools, `'felt'` for a quiet film).

## Banned

Cuts; a second shape; a piece the product doesn't have; sample data as a caption; a caption that names a feature
instead of what it does for the viewer; a click with no press; a cursor that snaps; anything that appears or vanishes
in one frame; text over text in a swap; bouncy easing on text; glows; gradients on UI chrome; particles; icons with
mismatched strokes; holds on the product's own working; dead time that isn't a read or a result.

## Engine rules

- `seek(t, values)` paints from its arguments only: no `Date`, `performance.now()`, unseeded `Math.random`, timers or
  network.
- CPU-backed canvases (`getContext('2d', { willReadFrequently: true })`), helper canvases too; `ctx.reset()` at the
  start of every frame.
- Every file the film loads is inside its folder; fonts and images load in `prepare()`.
