---
name: ui-morph
description: Make a 16-second square UI-morph film of one real job in the user's product. One shape that never cuts walks through it, each morph being what the click before it opens (the product's button becomes its card, the card its control, the control a loader, a check and the product's own result), with a cursor that presses every step, a caption per step in the product's headline face, springs, blur hand-offs and a song, looping pixel for pixel. Plans the story with the user, delivers an editable local preview and a 1:1 MP4. Use for feature announcements, launch clips, landing-page loops and UI teasers.
---

# UI morph

Make a short film of one real job in the user's product, told by one container that never cuts. The container is
each piece of the job in turn: the button that starts it, the card that button opens, the control on that card, the
product working, done, and the product's own result; then the button again, so it loops. A cursor drives every change,
pressing each step; a caption above the container says what the product does for the viewer at each step. 16 s on a
120 BPM grid, square (1440 × 1440), with a song that lands on the check.

You work by **adapting a finished film**. `reference/` is the complete film for Fennick, a fictional sparkling-tea
shop made for omnigami's examples: "Plans changed?" → the "Your box" button opens the next box → "Skip a box" opens
"Pick a new date" → 10 Dec → saving → done → "Skipped. Next box ships 10 Dec." → "Skip, swap or pause any time."
(`reference/STORY.md`). **Keep** its machinery: the container and its springs, the hand-offs, the captions' motion,
the presses and hovers, the cursor, the beat grid, the loop, the sound. **Replace** its nouns: the job, the pieces,
the words, the colours, the fonts, the mark, the sample data.

Read `style.md` before you plan and `critique.md` before you judge anything. `spec.md` lists the reference's every
row (times, boxes, cursor points, captions, cues), so you can see what moves together.

**Shape:** this skill makes square only. The reference lays out no wide or tall frame; if the user asks for one, say
so and make the square. Never crop, letterbox or stretch it into another frame and call it that shape.

## What to ask for

- The product's URL, and where the job lives: the app itself, a live demo, a sandbox, its source, or the user's own
  screens of each step. A demo account if it needs a sign-in.
- The job to show, if they have one: one task a user comes to the product for, two to four clicks, ending on a result.
- Nothing else is required. Captions come from the product's own words.

Read the site before asking, and ask once, in one message, for what it can't answer. If the user wants no questions
or an unattended run, decide from what you can reach: pick the job the product is most for, in its own order.

## Start or resume

- Check Node 20+, ffmpeg and a local Chrome-family browser (`scripts/chrome.mjs` finds it; `CHROME_PATH` overrides).
  Explain anything missing and stop.
- If a `ui-morph-film/` folder already exists with `film/STORY.md`, this is a revision: see Revisions. For another
  clip of the same product, make a new folder, reuse its `PRODUCT.md`, fonts and mark, and keep the previous film.

Set up a first film. `SKILL_DIR` is this file's folder:

```bash
mkdir ui-morph-film && cd ui-morph-film
cp -R "$SKILL_DIR/reference" reference && cp -R "$SKILL_DIR/reference" film
cp -R "$SKILL_DIR/scripts" scripts && cp -R "$SKILL_DIR/music" music
rm -rf reference/out film/out film/capture/screens
npm init -y >/dev/null && npm i -D puppeteer-core
node scripts/render.mjs reference --size 1:1 --times key --sheet --out out/reference
```

Look at `out/reference/1x1-sheet.png` and play `reference/index.html` in the browser: that's the bar. `reference/`
stays untouched, to compare against.

## 1. Read the product

1. `node scripts/capture.mjs <url> capture`. Read every screenshot and `capture/brand.json`: what the product does in
   its own words, who it's for, its voice, its colours with what each is for, its fonts, its mark.
2. Write `PRODUCT.md`: the URL, what it does, its voice, its **ink** (its darkest text or dark buttons), its **paper**
   (its page), its **accent** (its brand colour and where the product uses it), its UI face and headline face (with
   their licences and files), its mark, the sources of any claim, the date. Sample data only; never customer data.

## 2. Choose the job and write the story

1. **One job.** A task a user does in the product, in the product's own order: start it → the piece that opens → the
   choice on it → the product saving or working → done → the product's own result message. Two to four clicks. Not a
   tour of features; no chart, slider or toggle the job doesn't use.
2. **Each morph is what the click before it opens.** For every click, the next state is exactly what the product
   shows after that click, narrowed to the piece that matters (the card, the sheet, the menu, the control), not the
   whole page. If the product shows no loader, go straight to done; if it confirms with a toast, notice or banner,
   that's the result, in its own words.
3. **Captions,** one per step, in the product's voice: a need first (the reference: "Plans changed?"), then what each
   step does for the viewer ("Skip the next box.", "Pick a new date."), then the product's promise, in its own words
   where it has them ("Skip, swap or pause any time." is the shop's own line). Two to five words, at most 22
   characters (30 for the promise). **Never the sample data:** a date, a price, a name or a filter belongs inside the
   product's pieces, not in a caption.
4. **The grid.** Keep the reference's beats (`style.md`, "The beat grid"): the brand, the question, each click on a
   beat with its caption read and the cursor's rest before it, the working, done on a bar line (where the song lands),
   the result held about 3 s, the promise, the brand held to the loop. A job with more or fewer clicks adds or removes
   whole bars (2 s) and keeps every hold; a longer film is better than a rushed one.
5. Write `film/STORY.md` in the shape of `reference/STORY.md`: the job in one sentence; the steps table (start,
   step, caption, container, cursor and action); the holds; where every word and piece comes from.
6. **Propose it** in one short message: the job as a line of arrows, the captions, the length. Ask for one review
   before building. An instruction to proceed, to avoid questions or to run unattended waives the review; silence
   doesn't. Don't ask the user to choose springs, sizes or times.

## 3. Capture each state

1. Write `film/capture/plan.json` in the shape of `reference/capture/plan.json` (the format is at the top of
   `scripts/screens.mjs`): the job's page; for each state, a capture `around` the piece the container becomes; the
   job's own clicks between them, with a short `wait` after each.
2. `node scripts/screens.mjs film/capture/plan.json film/capture/screens`, then look at every capture. These are the
   source of truth for each piece: its words, icons (take the SVG paths from the product's own markup when you can),
   order, proportions, radii, weights and colours. A piece the product doesn't have can't be in the film: change the
   story, never draw the feature.
3. If the product can't be reached, ask for a demo account, a public demo or the user's own screens of each step.

## 4. Build

Edit `film/index.html`. Its sections are labelled **KEEP** and **ADAPT**; every hard-coded time is one of `T`'s or a
cursor arrival, so change them together.

- **Colours:** `INK`, `PAPER`, the greys and the accent from `PRODUCT.md`; the ground is the product's paper a shade
  deeper (`seek()`).
- **Fonts and mark:** the product's UI face and headline face in `film/assets/fonts/` with their licence files, loaded
  in `prepare()`; the reference's DM Sans may stand in for a UI face you can't license, but the captions never keep
  the reference's Bricolage Grotesque (it's Fennick's headline face). The product's wordmark as
  `film/assets/art/wordmark.svg`; delete the reference's box render (and its line in `prepare()`) unless your card
  shows a product photo of its own.
- **Words:** `DEFAULTS` and `FIELDS` (the button, the captions, the result), with labels and limits; the pieces'
  sample data (`CARD`, `DATES` in the reference) from the product's own sample data.
- **`T`:** the beats on the grid.
- **`BOX`:** one row per state. Sizes from the captures' proportions, the biggest piece about 1040–1190 px wide at
  1440 with at least 100 px clear of the frame; the button 205 tall and wide enough for its label at 55 px with
  room (the reference: 540, for up to 12 characters); the loader 221 and the check 230 circles;
  the toast's width comes from its words. Keep the firmer springs on a big collapse (into the loader) and a big growth
  (into the toast).
- **`CONTENT`:** one function per state, drawing the product's own piece in that state's box `d`. Adapt `C.card` and
  `C.chooser` to your pieces or replace them (a list, a field, a menu, a toggle); keep `C.loader`, `C.check` and
  `C.toast` (with the product's result words and its check in its accent, if it uses one). A moving indicator keeps
  its two edge springs: the leading edge stiff, so for a move to the left, swap them.
- **`CUR` and `CLICKS`:** each target's point on its piece (the tip on the piece's lower part, beside the words), the
  row it works on, and the hover times in `box()` and the content functions (they're the cursor's arrivals).
- **`CAPTIONS`:** one row per caption, with the height of the state it sits above.
- **`cues()`, `music`, `STATES`, `keyTimes`:** in step with `T`; `DURATION` and `music.duration` change together.
- **KEEP** `logTrack`, `layoutFor`, `box()`, the press and hover curves, `cursorAt`, `drawCursor`, `drawCaptions`,
  the hand-offs in `seek()`, and the loop (the first and last states, the cursor's corner).

## 5. Check and critique

```bash
node scripts/render.mjs film --size 1:1 --stress
node scripts/render.mjs film --size 1:1 --times key --sheet
node scripts/render.mjs film --size 1:1 --phone
node scripts/render.mjs film --size 1:1 --review
node scripts/render.mjs film --size 1:1 --strip <each click minus 0.05>
node scripts/render.mjs film --size 1:1 --times 0,15.99        # the first and last frames (its length less 0.01 s)
node scripts/compare.mjs reference film out/compare.png --size 1:1
node scripts/render.mjs film --size 1:1 --check
```

`--stress` renders every key time with the default words, every field at its longest and at its shortest, and fails
when words leave the frame, overlap, fall under 28 px or are set with `textBaseline 'middle'`; look at its sheets in
`out/stress/`. `--review` writes strips around every cut and key time; the `--strip`s catch each press. `compare.mjs`
stacks the reference's beats over yours at the same times: the sizes, placement and timing of matching beats should
read the same. `--check` renders frames twice in different orders and compares them.

Score with `critique.md` and fix the worst problems. Before shipping, **get a fresh judgement**: if your agent can
start a sub-agent without this session's memory, give it `critique.md`, `film/STORY.md`, the captures and the images
(the sheet, the phone sheet, the strips), nothing else, and fix the worst problems it finds; otherwise reread
`critique.md` and score from the images alone, as a stranger would. Nothing ships below 8. After three rounds, report
what remains instead of calling it finished.

## 6. Render

Pick a poster time with the first piece and its caption settled (the reference: 4.4 s), then:

```bash
node scripts/render.mjs film --size 1:1 --video --blur 4 --sound --audio music/song.mp3 --bpm 120 --land <done> --poster <time>
```

`<done>` is the check's time (`T.done`, the reference's 10). This writes `out/1x1.mp4` (1440 × 1440, 60 fps, motion
blur, the song and the effects, around −14 LUFS) and `out/1x1-poster.png`. The song, `music/song.mp3` (glossy, bouncy
synth-pop at 120 BPM, made for this skill), starts on a bar line and lands one hit on the check, where its drums stop
(from the stems in `music/song-stems/`, found beside it) and the rest closes and fades. `--bpm 120` is its tempo,
which the fitter would otherwise misread a little. `--from <seconds>` starts at another of its 8-bar sections (it's
about two minutes long). `--music` gives the synthesised 120 BPM bed instead; the user's own licensed song works with
`--audio their.wav --land <done>` (without `--bpm 120`; cleanest with its stems in a `their-stems/` folder beside it).
Run it in the foreground and wait for the file.

Then check the MP4 itself: `node scripts/motion.mjs out/1x1.mp4 <from> <to>` over each morph (a dip at each click is
the press, by design; a stop, halt or jump elsewhere is a fault), the frames across each click (see `critique.md`),
and its first and last frames.

## 7. Deliver

- Start `node scripts/preview.mjs film` and give its localhost address: it plays and scrubs the live film, jumps to
  its states, and edits and saves the words (into `film/values.json`). The live canvas is silent; the MP4 has the
  sound. A saved word edit needs a new render to reach the MP4. Give the restart command with the project folder; if
  the host stops background processes, restart it when asked and give the new address.
- Write a project `README.md`: the files, the preview and render commands, how to change a word, and example
  revision requests.
- Write `out/CAPTION.md`: a post to share the film on X or LinkedIn, under 280 characters, in the product's own words,
  with its URL; no hashtags unless asked.
- Record the scores, round by round, in `out/REVIEW.md`.
- Hand over the preview address, the MP4 and its poster, the caption, a short check summary, and the one change that
  would most improve the film.

## Revisions and another clip

For requests like "hold the result longer" or "show pausing instead of skipping", edit the current story and film.
Keep approved beats and the user's saved words (`film/values.json`); read them before changing fields, and migrate or
remove a field only when its step changes. Explain the change in a line and make it; a targeted revision needs no
new story review. Keep the length by moving neighbouring holds unless the user asks for another; a new length
changes `DURATION`, the music, the cues, `keyTimes` and the landing. Rerun the checks for the beats you touched and
`--check`, render again, refresh the preview. Record changed preferences in `PRODUCT.md`. For another clip, reuse its
context and assets, recheck the product's current words, and propose the new job once.

## Hard rules

- One real job in the product, its real pieces and words, sample data only, only the user's brand.
- One container that never cuts; each morph is what the click before it opens.
- Captions say what the product does for the viewer; the sample data stays inside the pieces.
- A press on every click, a hover before it, and the result held long enough to read.
- `seek(t, values)` paints from its arguments only: no clocks, unseeded randomness, timers or network. CPU-backed
  canvases (`willReadFrequently: true`), helper canvases too, reset every frame.
- Every file the film loads lives inside `film/`; fonts and images load in `prepare()`.
- Square only.

## Files

- `reference/`: the finished Fennick film (`index.html`), the runtime (`kit.js`), its story (`STORY.md`), its
  evidence (`capture/plan.json` and the shop's states it captures, `capture/screens/`), the shop's box render and
  wordmark (`assets/art/`) and the fonts with their licences (DM Sans and Bricolage Grotesque, SIL Open Font License).
- `style.md`: the grammar, with its numbers. `spec.md`: the reference's tables. `critique.md`: the review.
- `music/`: the skill's song and its stems.
- `scripts/`: `render.mjs` (stills, sheets, strips, checks, the MP4), `preview.mjs`, `screens.mjs` (a product's
  states from a plan), `capture.mjs` (a site's brand and screenshots), `compare.mjs`, `motion.mjs`, `song.mjs`,
  `music.mjs`, `sfx.mjs` with the sound kit in `sounds/`, `centring.mjs` and `chrome.mjs`.

Style inspired by [@twoclipping's video](https://x.com/twoclipping/status/2103273003555402193). He didn't make or
endorse this skill.

This skill is omnigami's (https://omnigami.ai), © 2026 Auberon LLC. Use what it makes for anything,
commercial work included, and change the skill for your own use; don't redistribute or
sell the skill. Full terms: https://github.com/omnigami-ai/skills/blob/main/LICENSE.md
