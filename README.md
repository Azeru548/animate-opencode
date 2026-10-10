# animate-opencode

Procedural animation in any style, ported for [opencode](https://opencode.ai).
Short single-file canvas videos with story, look and storyboard check-ins:
7 built-in styles (cut paper, crosshatch ink, riso print, sketchbook, math,
pixel, isometric) or a new look matched from your references, your own music
(beat-mapped), real product screenshots, every format from one piece.

Based on [cth9191/animate](https://github.com/cth9191/animate) (MIT) —
see LICENSE. Only the agent-facing docs and packaging were changed; the
drawing kits, tools and examples are untouched.

## Install

Copy the folders into opencode's config (global) or your project:

- `skills/animate/` → `~/.config/opencode/skills/animate/`
  (or `<project>/.opencode/skills/animate/`)
- `commands/animate.md` → `~/.config/opencode/commands/animate.md`

Requirements: Node 18+, Playwright with Chromium, ffmpeg on PATH.

```sh
npm i -g playwright && npx playwright install chromium
```

On Windows, if `npm`/`npx` are blocked by the PowerShell execution policy,
call `npm.cmd`/`npx.cmd` by full path instead. For voice-overs: Python with
`faster-whisper` (`pip install faster-whisper`) times every word; without it
the word times are estimated.

Then quit and restart opencode so the skill and command register.

## Use

```text
/animate a 45-second history of the bicycle, cut paper
/animate how a hash map works, in the math style
/animate a 20s launch reel for https://my-product.com, vertical and square
```

The skill walks you through intake, then three check-ins (story, look,
storyboard) before animating, and proves the result with measured review
checks. No animating before the storyboard is approved.

## What the port changed

- `AskUserQuestion` → opencode's `question` tool (recommended option first).
- Removed the `argument-hint` skill frontmatter field (not valid in opencode).
- Skill base paths rewritten for opencode's skills folders.
- ElevenLabs connector flow (Claude Settings → OAuth) replaced with
  environment-agnostic options: your own API key/MCP or own recordings.
- `new-style.md`: added PowerShell-safe `$env:SKILL` / `$env:P` invocations.
- Added `commands/animate.md`: the `/animate` slash command.
- "Split across agents" now means opencode subagents via the task tool.
