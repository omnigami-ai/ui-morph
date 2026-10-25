# Critique

Be a harsh motion director who didn't build this. Default: reject. Judge the pictures and the MP4's frames, not the
code.

## What to look at

- `film/STORY.md` and the captures in `film/capture/screens/`: is this one real job, in the product's order?
- The key-frame sheet (`--times key --sheet`) and the phone sheet (`--phone`).
- The review strips (`--review`: every other frame, 0.8 s, around every cut and key time) and a 12-frame `--strip`
  just before every click (`<click> - 0.05`), at every morph, at the collapse into the loader, at the result's words
  and at the close.
- The MP4 itself, frame by frame across each click and morph (ffmpeg, e.g.
  `ffmpeg -ss 2.9 -i out/1x1.mp4 -frames:v 12 -vf "scale=480:-1,tile=6x2" out/press1.png`), and
  `node scripts/motion.mjs out/1x1.mp4 <from> <to>` over each morph (a dip at each click is the press, by design).
- The loop: `--times 0,15.99` side by side, and the MP4's first and last frames.

## Score each 1–10 (nothing ships below 8)

1. **Story:** one real job, done once in the product's order, ending on its real result. Each morph is what the click
   before it opens. Every piece the container becomes exists in the product and matches its capture: words, icons,
   order, colours.
2. **Timing:** clicks and landings on the beat; every caption read before the cursor moves; the result held; the song
   lands on the check.
3. **Springs and hand-offs:** each morph overshoots a little and settles in one move; content blurs out and in under
   it; nothing slides linearly or stops dead.
4. **Presses and the cursor:** every click visibly pressed, on its onset, by the piece and the cursor; a hover on what
   the cursor rests on; the cursor glides, rests, presses, and never covers what it points at.
5. **Type and fit:** labels centred on their capitals; every word fits its piece with room, in every state; on the
   phone sheet (360 px wide) every word reads; nothing under 28 px at 1440.
6. **Craft:** the product's ink, paper and one accent where the product uses it; icons in the product's stroke;
   spacing even; nothing cheap, borrowed or invented.
7. **Loop:** the last frame is the first, pixel for pixel, the cursor included.

## The founder's rules (check each; a failure is a fix, not a note)

- **One job, one shape (Direction A, 2026-10-25).** One task, not a tour of features. No piece is there to fill a slot:
  no chart, slider or toggle the job doesn't use. Check every state against its capture; a piece the product doesn't
  have fails the film (change the story, never draw the feature).
- **Captions say what the product does for the viewer, never the sample data.** "Pick a new date." passes; "10 Dec"
  or "Under $220 a night" as a caption fails. Sample data belongs inside the product's pieces. Each caption is short
  enough to read in about a second (two to five words).
- **Breathing room** (a failure caps the film at 7): the caption lands and holds about a second before the cursor sets
  off; the cursor rests 0.4–0.5 s on its target before it presses (not a full second); the result holds at least 1 s
  (the reference: 3.1 s); the brand holds to the loop. No hold on the product's own working (the loader). Nothing acts
  the instant it arrives. Read it at each click on the strips: caption landed → cursor sets off → rests → press.
- **A press on every click,** on the press's visual onset: the pressed piece sinks a few percent and lightens (dark)
  or darkens (light), then comes back. The cursor's press eases too: count frames on the MP4 strip before each click;
  the cursor reaching 0.86 in one frame, or coming back in one, fails (it takes about 3 frames down, 10 back).
- **Hover on what the cursor rests on:** the button lightens, a ghost button washes, a segment washes. A press with no
  hover before it fails.
- **One-step morphs:** a shape becomes the next in one continuous move. The wide control collapsing to the round
  loader must never pass through a tall pill (strip at the collapse: every frame is wider than tall or round); sizes
  ride their springs in log space.
- **No one-frame pops at hand-offs:** a leaving caption never runs into the growing container (it keeps its gap
  above the live top edge); the result's words never come into focus clipped by a pill still opening; a struck label
  is revealed as the indicator leaves it, not drawn over it; nothing (a check, a label, an icon) vanishes or appears
  in a single frame.
- **Labels centred on their capitals** in every pill, button and segment (`kit.centreText`; `--stress` fails canvas
  text set with `'middle'`). Measure on a full-size still, not by eye. Segments and chips are fully rounded pills.
- **The visual vocabulary is the product's:** its own pieces, icons and words; no devices borrowed from other fields
  (no bounding boxes, no annotation arrows, no device frames).
- **Sound:** a tap on every press and a sound on each landing, on its visual onset, with no riser or accent and
  nothing crunchy; the song's hit lands on the check.
- **A story that holds:** time only runs forward; no screen repeats; the end is the product's real result, then the
  brand.

## Hunt for

- the cursor parked over the words it points at, or snapping instead of gliding;
- a click with no visible response, or a response before the click;
- text over text during a swap, or a caption over the container;
- a box that crowds the frame (keep at least 100 px clear at 1440) or clips its own content at the corners;
- muddy, mixed-up states that read as neither piece for more than a few frames;
- colour that isn't the product's, more than one accent, or the accent where the product keeps neutral;
- a hold with nothing to read, or a result gone before it's read;
- outdated fields, scene names (`STATES`), review times (`keyTimes`) or sound cues after a change;
- the user's saved words (`film/values.json`) lost in a revision;
- a claim of wide or tall: the skill makes square only.

For every issue write the state and time, what's wrong, and the exact fix ("the cursor arrives at 2.5 and presses at
2.7: move the click to 3.0, a beat later, and its cue with it"). Fix the five that matter most, look again at those
times and the cuts either side, and score again. With each fix, write what it must keep. If the same problem survives
two fixes, stop and report it with what you tried. Never loosen a check, a size floor or the bar to pass. After three
rounds, report what remains instead of calling it finished.
