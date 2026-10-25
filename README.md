# UI morph · omnigami

One shape, never cut, walking through one real task in your product.

A 16-second square film of one thing people do in your product, start to finish. One container becomes each step in turn: your button, the card it opens, the choice on it, then done and your product’s own confirmation. A cursor presses every step, a caption says what each one does for you, and the song lands on the check. It loops. You review the short story first, then watch and revise the film.

Watch it play live, and change its words, at [omnigami.ai/skills/ui-morph](https://omnigami.ai/skills/ui-morph).

## Install

In Claude Code:

```
/plugin marketplace add omnigami-ai/skills
/plugin install omnigami-ui-morph@omnigami
```

With the skills CLI, for Claude Code and other agents that read SKILL.md:

```bash
npx skills add omnigami-ai/ui-morph
```

Or copy `skills/ui-morph/` into your agent's skills folder (for Claude Code, `~/.claude/skills/ui-morph/`). Then ask:

```
Make a short film of one task in https://your-product.com
```

## What it runs

The skill works on your computer. It runs the Node scripts in `skills/ui-morph/scripts/`: they open your product's pages in a local headless browser to capture its real screens, then render the film with that browser and ffmpeg, writing MP4s and an editable HTML film to your project. It sends nothing to omnigami or anyone else, and uses no network beyond loading your own product's pages and the fonts and assets in this folder.

## You need

- Claude Code with Opus 5.5
- Node 20 or later
- ffmpeg
- Chrome, Chromium, Edge or Brave

None beyond your Claude plan’s usage. Node, ffmpeg and the browser are free.

## Licence

Free to use. Use the films and anything else the skill makes for anything, commercial work included. Don't redistribute the skill. See [LICENSE.md](LICENSE.md). The bundled fonts keep their own licence (SIL Open Font License, beside them in `reference/assets/fonts/`).

## Credits

Style inspired by @twoclipping’s video (https://x.com/twoclipping/status/2103273003555402193); @twoclipping didn’t make or endorse this skill. Its example shows Fennick, a fictional company made for omnigami’s examples, with sample data.

omnigami is not affiliated with Anthropic. More skills at [omnigami.ai](https://omnigami.ai).
