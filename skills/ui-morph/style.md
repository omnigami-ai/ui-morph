# UI morph: style

Style after [@twoclipping's UI-morph video](https://x.com/twoclipping/status/2103273003555402193),
made in code with Claude Opus 5.5 from a prompt he published openly. The
reference film here is our own, built and measured against it (`spec.md`).

## The grammar

- **One shape, never cut.** Every state is the same container changing size, radius and colour. There are no cuts and no second object.
- **A cursor drives every change,** with real clicks and drags. Nothing changes by itself except loaders, counters and the typing.
- **Beat-led rhythm:** 120 BPM, a beat every 0.5 s, 28 beats, 7 bars, 14 s. Place actions and transition accents on the rhythm; allow readable result holds. The film loops: the last frame is the first.
- **Light canvas** a shade deeper than the product's paper (the reference: Fennick's `#EFE7DA`), a little lighter in the middle. UI in the product's ink and paper (Fennick: `#1D1A16`, `#FBF6EE`), with the product's brand colour as its one accent, where the product itself uses it: the primary button, the active tab or selection, a chart line, a check. One UI face (Geist, or the product's own when licensed).
- **Content swaps behind a short blur:** the outgoing content blurs out over 0.08 s as the morph starts; the incoming blurs in over 0.14 s from 0.05 s after.

## Choose scenes for the product

Keep the motion grammar above. Choose actual product actions and visible
results first. The following table documents the reference, not required
states. Reuse its measured transitions where they fit; replace irrelevant
controls or scenes while preserving continuous motion, readable holds and
120 BPM rhythm. A held scene can have small responsive motion without
adding another feature or repeatedly toggling a meaningless setting.

## Reference states (at 1440 px; t = when the morph starts)

| t (s) | State | Box | What it can become for another product |
|---|---|---|---|
| 0.00 | button | 641 × 205 pill, black | the main call to action |
| 0.55 / 0.93 | loader, then a check | 221–230 circle | the action working, then done |
| 1.27 | island | 863 × 219 pill | the product's tile and something live |
| 1.80 | card | 996 × 633, r 67 | the core object (a track, a doc, a watch, an order), with a bar to scrub and three controls (below) |
| 3.72 | slider | 1075 × 185 pill | one continuous setting; dragged down, then past the end so the pill stretches |
| 5.27 | toggle | 490 × 274 pill | one on/off setting, flipped three times on the beat |
| 6.27 | tabs | 1191 × 169 pill, white | three periods or views |
| 7.27 | chart | 1099 × 843, r 44, white | a number that counts up, a line that draws, a tooltip scrubbed along it; the second tab reshapes it |
| 9.73 | search | 871 × 210, r 59 | the product's search or ask box, with ⌘K |
| 10.07 | palette | 1039 × 813, r 35 | five real commands |
| 10.60 | filtered | 1243 × 571, r 41 | three typed letters filter to two; the second is chosen |
| 11.77 | toast | 965 × 180 pill, black | the closing line, with a check |
| 12.57 | button | as the first | back to the start: the loop |

## Adapting scenes and their interactions

For each replacement, update these together:

- container keys (`BOX`) and drawing functions (`CONTENT`), with their local times;
- cursor targets, easing/drag intervals (`CUR`, `LINEAR`, `DRAGS`) and clicks;
- scene-specific hooks: `cursorAt` follows `chartLineY` at 7.85–8.8 s;
  `box` applies slider stretch at 4.0–5.27 s; `lumKeys` includes `TOGGLE`;
- tabs, typing, counters and other content schedules;
- sound cues and music accents, so removed actions leave no ghost clicks;
- editable fields and defaults, the saved words in `values.json`, scene names
  (`STATES`) and review times (`keyTimes`);
- each shape's layout (`SHAPES`): a new or resized box that crowds the wide or
  tall frame gets its own `[w, h]` there, and every new `CUR` point names the
  `BOX` row it works on.

Use the reference's spring constants and blur hand-offs as the starting
point. Container geometry can change for a different real screen. Keep
breathing room and the type hierarchy; do not shrink words to fit. Check
fast transitions at their new times. Keep the loop's first and last frame
matching, including cursor and any saved words.

For example, a large panel can expand into a real search result instead of
a chart if that is what the product does. Rebuild its action, cursor and
sound from the evidenced interface; changing the chart label is not enough.

## When the product has the reference card's controls

The reference has three controls under a scrub bar; its middle control is
clicked twice (2.33 and 2.7 s). Retain this only when those interactions
exist in the product. Otherwise replace the layout and cursor action.
For retained controls:

- **The middle one** is a two-state action: pause / resume, follow / unfollow, lock / unlock, live / paused, star / unstar.
- **The side ones** are its neighbours (previous / next item) or two related actions (refresh, share, export).
- **Media controls** (previous, play / pause, next) only when the product plays something or has a live feed to pause, as the reference's box delivery does (pause and resume the box).
- When the middle pair isn't pause and play, swap its two icons on each click with a quick spring (the old one shrinks out, the new one grows in), never a crossfade.

## Type

The product's UI font throughout (the reference: DM Sans), with tabular figures for small numbers. Sizes in px at 1440, measured against the original. Use the same hierarchy for equivalent content; cut words before shrinking anything. New scenes use comparable sizes and the floor below.

| Where | Size | Weight |
|---|---|---|
| button label | 55 | 600 |
| card title / subtitle | 44 / 32 | 600 / 400 |
| card figures under the bar | 28 (mono) | 400 |
| tabs | 47 | 600 |
| chart number / tabs / caption / tooltip | 105 / 29 / 29 / 29 | 700 / 600 / 400 / 600 |
| search / ⌘K | 42 / 32 | 400 / 500 |
| palette input / rows / shortcuts | 38–46 / 36–44 / 28–30 | 400–500 / 500 / 500 |
| toast | 45 | 500 |

Nothing under 28 px: that is the original's smallest text, and about the limit on a phone.

## Motion

- **Container:** closed-form springs, stiffness 280, damping 19 (a visible overshoot of a few percent on every morph). Size, radius, position and colour all ride it.
- **Cursor:** arrives on the beat; every move eases out fast and lands soft, except drags, which move steadily. Pressed, it shrinks to 0.86.
- **Two-edge motion:** the toggle knob and the tab indicator have a stiff leading edge (560/26, 440/24) and a soft trailing edge (190/17, 170/16), so they stretch as they travel and settle.
- **Stretch:** dragged past its end, the slider grows by 0.62 of the overshoot, left edge fixed; on release it springs back (320/14).
- **Counters** ease out over 0.5 s; the chart line draws left to right over 0.5 s.
- **Motion blur:** 4 sub-frames across half a frame (`--blur 4`).

## Sound

Retiming or replacing a scene must retime or replace its sounds too.
A `tap` on every press, a `pop` as each state lands, a `tick` per typed key, a
`whoosh` on the big openings (card, chart, palette), and a light 120 BPM bed.
The effects come from omnigami's own kit; `scripts/sounds/kit.json` says what
each one is for. Name them in `cues()` and use them as they are. Mastered around −14 LUFS.

The score's sound is `music.style`: here `'organic'` (plucked strings, a marimba, a shaker), as the reference's plants or botanicals brand has it. For the user's product, pick by what it is: `'organic'` for plants, food and drink, and other natural or handmade things; `'synth'` (oscillators, the default) for software and tools; `'felt'` (a sparse felt piano over a sub bass and a light kit) for a quiet, minimal film. In a break (`music.breaks`) the drums, bass and lead stop and the chords play on; the film's name seeds the key (always major), the progressions and the patterns.

## Banned

Cuts; a second shape; bouncy easing on text; glows; gradients on UI chrome;
particle bursts; icons with mismatched strokes; unmotivated dead time; text
overlapping text during a swap; anything that looks like a
template; invented features.

## Engine rules

- `seek(t)` paints from `t` only: no `Date`, `performance.now()`, unseeded `Math.random`, timers or network.
- A CPU-backed canvas (`getContext('2d', { willReadFrequently: true })`), and helper canvases created the same way.
- `ctx.reset()` at the start of every frame, so no canvas state carries over.
- Every file the film loads is inside its folder; fonts load in `prepare()`.
