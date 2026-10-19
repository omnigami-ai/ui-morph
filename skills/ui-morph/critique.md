# Critique

Be a harsh motion director who didn't build this. Default: reject. Look at the
pictures; don't score from the code.

## What to look at

- Read `film/STATES.md` and its source evidence. Is this the requested journey?
- The film's own key-frame sheet (`--times key --sheet`) and phone-size sheet.
- Compare retained scenes with the reference (`scripts/compare.mjs`). For
  replaced scenes, use the reference to judge craft, not content or timestamps.
- Strips around the adapted film's actual transitions and actions.
- The first and last frames side by side (`--times 0,13.99`): they must match, cursor included.

## Score each 1–10

1. **Timing:** actions and transitions follow the planned rhythm; results hold long enough to understand. Reference timestamps apply only to retained, unretimed scenes.
2. **Springs:** morphs overshoot a little and settle; nothing slides linearly or stops dead.
3. **Fit:** every word fits its container with room to spare, in every state and every shape; nothing is clipped by the rounded corners, and no box crowds or leaves its frame.
4. **Readability:** on the `--phone` sheet (360 px wide) every intended word is readable; equivalent content keeps the reference hierarchy and no text falls below 28 px at 1440 px.
5. **Truth and story:** every state shows an evidenced product action or result, in its own words with sample data. The sequence explains the requested feature; no chart, setting or control exists just to fill a reference slot.
6. **Craft:** icons share one stroke weight; spacing is even; the art tile uses the product's own mark and colours; the brand colour is the one accent, used where the product uses it.
7. **Loop:** the last frame equals the first.

## Hunt for

- **Breathing room** (a failure here caps the film at 7): an action the viewer can't follow on one viewing: a click within half a second of the camera or cursor arriving, a result gone in under a second, a caption or headline replaced before it can be read. Lengthen the film rather than compress the holds.
- **Type centred in its container** (pills, buttons, chips, badges, a word beside a mark): the capitals sit on the container's centre line, measured, not by eye. Words that ride high are the usual fault (textBaseline 'middle' and CSS line boxes both centre the font's em box, not the letters); draw with `kit.centreText`, and in HTML use `text-box: trim-both cap alphabetic` with equal padding. The quick test fails canvas text set with 'middle'; captured screens and HTML are checked on the stills.
- **The film's own shapes, finished:** every click has a press state on its visual onset (what's pressed sinks a few percent and lights or darkens, then comes back), and a held control shows it's held; apertures and reveals are clean circles or the product's own shapes, never blades or drawn lines; a shape that becomes another does it in one continuous move, not a chain of in-between shapes; a pulse is one thin ring that thins as it grows; nothing (a check, a label, an icon) vanishes or appears in a single frame at a hand-off: it moves, shrinks or is covered. Check each on a strip of consecutive frames from the MP4.
- text overlapping text during a swap;
- the cursor covering what it's pointing at (it sits beside or below its target, as in the reference);
- frantic activity that prevents understanding a result, or an unmotivated hold;
- geometry that crowds the frame or clips the real content, in any of the three shapes; shorten copy and adjust the layout;
- a shape that only looks like the square one cropped or shrunk, or a box lost in the wide or tall frame;
- tiny controls or labels, an inconsistent type hierarchy, or overloaded scenes;
- controls that mean nothing for the product (play / pause on a product that plays nothing);
- colour that isn't the product's, more than one accent, or the accent on surfaces the product keeps neutral;
- a click with no visible response, a cursor following a removed chart, slider stretch on an unrelated scene, or sound for a removed action;
- outdated scene names, fields or review times after a replacement;
- user word edits lost during a revision.

For every issue write: state and time, what's wrong, and the exact fix
("toggle knob lands 3 frames late: move its TOGGLE time from 5.85 to 5.80").
Fix the five that matter most, compare again, score again. Nothing ships
below 8.

With each fix, write what it must keep (the timing, sizes and moves already
right) and the times to look at again; look at them, and at the cuts either
side, before scoring again. If the same problem survives two fixes, stop
fixing it and report it with what you tried. Never loosen a check, a size
floor or the bar to get a pass. After three rounds, report what remains
instead of claiming it is finished.
