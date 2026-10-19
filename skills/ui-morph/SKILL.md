---
name: ui-morph
description: Create or revise a 14-second UI-morph product film from real screens and actions, with one continuous shape, spring motion, a cursor and sound. Plan the story around the product, deliver an editable local preview and square, wide and tall MP4s, and reuse brand assets for the next film. Use for product launch clips, feature announcements and UI teasers.
---

# UI morph

Make a product film in one continuous morphing container, driven by a cursor,
with spring motion and sound at 120 BPM. Start from the finished Fennick film (a fictional sparkling-tea shop made for omnigami's examples)
in `reference/`. Its measurements (`spec.md`) teach the motion; its sequence
of controls is an example. Preserve the craft while choosing scenes that tell
the user's actual story. Never invent a feature to fill a reference scene.

Read `style.md` before building and `critique.md` before judging.

## Start or resume

- Check Node 20+, ffmpeg and a local Chrome-family browser (`scripts/chrome.mjs`
  finds it; `CHROME_PATH` overrides). Explain any missing dependency.
- Use the product URL and purpose already supplied. Inspect the site before
  asking for details it can answer. Ask once for essentials still missing:
  the product or assets you cannot access, the action to highlight, or an
  explicit restriction. Infer the CTA and closing words from verified copy
  when the user has no preference.
- Look for an existing `ui-morph-film/`, its `PRODUCT.md`, `film/STATES.md`
  and `film/values.json`. For a revision, work on that film instead of
  restarting. For another clip, create a new named project folder and reuse
  the previous brand assets and preferences; preserve the previous film.
  Confirm changed facts from the current product. Do not copy customer data.

For a first film, copy the reference and scripts into a new project:

```bash
mkdir ui-morph-film
cp -R "$SKILL_DIR/reference" ui-morph-film/reference
cp -R "$SKILL_DIR/reference" ui-morph-film/film
cp -R "$SKILL_DIR/scripts" ui-morph-film/scripts
cd ui-morph-film
npm init -y >/dev/null
npm i -D puppeteer-core
```

`SKILL_DIR` is this skill's directory. Choose another folder if this one
already exists and the request is for a new clip. Keep `reference/` untouched.

## Learn and propose the story

1. Capture the site: `node scripts/capture.mjs <url> capture`. Inspect the
   screenshots and `capture/brand.json`. Use supplied screens or accessible
   product source when available. If a marketing site does not reveal the
   interaction, request the missing evidence rather than invent its UI.
2. Choose a real action and its result. Prefer a coherent short journey over
   unrelated controls. Keep the film 14 seconds at 120 BPM, in all three shapes.
   Select enough scenes for that story; no required count or UI sequence.
   Keep a reference scene when it fits; replace it when it does not.
3. Write `film/STATES.md`: start/end time, scene, source screen or evidence,
   visible action and result, on-screen words, and transition. Note which
   reference scenes are reused or replaced and why. Pick readable holds and
   rhythmic accents; tiny loading states need not become separate scenes.
4. Show a short proposal in ordinary language: duration, a sequence of actions
   joined by arrows, and one sentence about replacements. Ask for one story
   review before building. Explicit instructions to proceed, avoid questions,
   or run unattended waive that review; follow existing authorization. Never
   treat silence as approval. Do not ask the user to choose springs or coordinates.

## Build from the reference

- Keep the continuous container, spring character, blur hand-offs, cursor
  easing, loop and readable type. The reference's scene count, order, exact
  timestamps, controls and geometry may change to fit the planned story.
- Adapt the existing content functions and add replacements as needed. Use
  the product's real screens or faithful reconstructions from evidence,
  branded with its words and licensed assets. A chart is appropriate only
  when the product actually shows that data; sample data illustrates the
  interface, never an invented claim about growth or results.
- Update the full scene together: `BOX`, `CONTENT`, local animation times,
  `CUR`, `LINEAR`, `CLICKS`, `DRAGS`, `STATES`, `keyTimes`, sound `cues()` and
  any music accents. Read `style.md`'s adaptation checklist. In particular,
  the reference's cursor follows `chartLineY`, its box stretches during the
  slider drag, and its luminance changes with `TOGGLE`: replace these hooks
  when replacing those interactions. No cursor clicks on removed controls.
- Lay out all three shapes: square (1:1), wide (16:9) and tall (9:16), each
  for its own frame, never cropped. `SHAPES` gives each its frame, a scale
  `k` for the whole design and, where a state's box doesn't suit the frame,
  a replacement `[w, h]` for that `BOX` row. Content draws relative to its
  box, so it follows. Give every `CUR` point the `BOX` row it works on (or
  `'frame'` for where it enters and leaves, `null` in passing) so it moves
  with that box. Keep a clear margin in every shape, including the slider's
  stretch, and replace a box in the shape that needs it rather than shrinking
  the whole design.
- Keep useful short words in `DEFAULTS` and `FIELDS`, with labels and limits
  appropriate to the new scenes. Remove obsolete fields; add replacement
  fields. Expose only words the user can meaningfully change; a clip with no
  user text can have no fields. Do not invent copy just to populate the editor.
  User edits in `film/values.json` override defaults during preview,
  checks and rendering. Read them before revising the film; preserve edits
  and migrate or remove fields only when their scene changes.
- Use the product's font when licensed files are available; otherwise use the
  bundled DM Sans (Fennick's UI font). Keep the type hierarchy and 28 px floor at 1440 px.
  Shorten words before shrinking type; allow geometry to fit a real scene.
- Save `PRODUCT.md` at the project root: URL, purpose, evidence paths, brand
  assets/fonts and licence, chosen words, preferences and verification date.
  Save only sample data. This is local reusable context, not account data.

## Review, render and deliver

1. Set the film's `keyTimes` inside its own scenes and after important actions.
   Make its own sheet and phone check:
   ```bash
   node scripts/render.mjs film --all --times key --sheet
   node scripts/render.mjs film --all --phone
   ```
   For unchanged scenes, `node scripts/compare.mjs reference film out/compare.png`
   compares at reference times (square). Look at every shape's sheet: a box
   that crowds or leaves its frame is a layout fix in `SHAPES`. For replaced
   or retimed scenes, inspect the
   reference's craft separately; matching its content is not a success criterion.
2. Inspect 12-frame strips at the film's actual transitions and clicks:
   `node scripts/render.mjs film --size 1:1 --strip <time>`, and in the shape
   whose box you replaced (`--size 9:16`, `--size 16:9`). Update the times
   after revisions. Inspect the loop with `--times 0,13.99`.
3. Score using `critique.md`; fix the worst problems and review again. Do not
   ship below 8 in any category. Before shipping, **get a fresh judgement**:
   if your agent can start a sub-agent without this session's memory, give it
   `critique.md` and the images (the sheet, the phone check and the strips),
   nothing else, and fix the worst problems it finds; otherwise reread
   `critique.md` and score from the images alone, as a stranger would. After
   three unsuccessful critique rounds, report the remaining issues instead of
   claiming the film is finished.
4. Check repeatability: `node scripts/render.mjs film --all --check`.
   This compares sampled frames in two orders, not every encoded frame.
5. Pick a representative poster time from the adapted story and render:
   ```bash
   node scripts/render.mjs film --all --video --blur 4 --music --sound --poster <time>
   ```
   Output: `out/1x1.mp4` (1440 × 1440), `out/16x9.mp4` (1920 × 1080) and
   `out/9x16.mp4` (1080 × 1920), each at 60 fps with motion blur, music and effects,
   mastered around −14 LUFS. For the user's own licensed song use `--audio song.wav`
   instead of `--music`: `song.mjs` fits it to the film (it starts on a bar line and, near
   the end, lands one hit and closes and fades; cleanest with the song's stems in a
   `song-stems/` folder beside it). A song near 120 BPM fits the cuts; `--from <seconds>`
   starts at another section of it.
6. Start `node scripts/preview.mjs film` and provide its actual localhost URL.
   It plays and scrubs the live film in each shape, jumps to its scenes,
   edits and saves words, and links each shape's MP4 when rendered. The rendered video has sound;
   the live canvas is silent. Explain that saved word edits require a new
   render to update the MP4. Keep the preview process available for review.
   Include the restart command and project folder in the handoff. If the host
   stops background processes, restart the preview on request and return its
   new URL. Expiry does not affect saved edits or the MP4; another expiry is
   not a reason to refuse a useful review session.
7. Write a project `README.md` with files, preview and render commands, how
   to change words, and example revision requests. Write `out/CAPTION.md`: a
   post to share the film on X or LinkedIn, under 280 characters, in the
   product's own words, with its URL; no hashtags unless the user asks.
   Deliver preview and MP4 links, the posters (`out/<shape>-poster.png`), the
   caption, a short check summary and the most useful remaining improvement.
   Record detailed scores in `out/REVIEW.md`; do not bury the film under logs.

## Revisions and another clip

For requests such as “hold the results longer” or “show saving instead of
starring,” edit the current story and film. Preserve approved scenes and the
user's saved words. Explain the intended change briefly and proceed within
the request; a targeted revision does not need another full story approval.
Keep 14 seconds by adjusting neighbouring holds unless the user asks for a
new duration. If duration changes, update the loop, music, cues and metadata.
Rerun the relevant visual checks and determinism, then render the new MP4.
Refresh the preview and return the updated links. Record changed preferences
in `PRODUCT.md`. For another clip, reuse that context and assets, recheck
current facts, and propose the new story once.

## Hard rules

- Real product UI and actions only; sample data only; only the user's brand.
- One continuous container; keep the motion quality and readable type.
- `seek(t, values)` paints only from its arguments: no clocks, unseeded
  randomness, timers or network. Use CPU-backed canvas contexts including
  helper canvases, and reset their context at each frame.
- Every file loaded by the film lives inside `film/`; assets load in `prepare()`.

## Files

- `reference/`: finished Fennick film, runtime, its can render (`assets/art/`) and the licensed font (DM Sans, OFL).
- `style.md`: motion grammar, reference measurements and adaptation checklist.
- `critique.md`: visual and story review; `spec.md`: original measurements.
- `scripts/`: capture, render, compare, local preview, music, effects (from the
  sound kit in `scripts/sounds/`) and browser discovery.

This skill is omnigami's (https://omnigami.ai), © 2026 Auberon LLC. Use what it makes for anything,
commercial work included, and change the skill for your own use; don't redistribute or
sell the skill. Full terms: https://github.com/omnigami-ai/skills/blob/main/LICENSE.md
