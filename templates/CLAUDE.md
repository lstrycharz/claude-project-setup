# [Project Name] — research / brainstorm project

## What this is

Open-ended research and brainstorming. Source material lives in `inputs/`. Claude's working material lives in `notes/`. The source index lives in `sources/index.md`.

## How to operate

1. When new files appear in `inputs/`, run `/intake` to refresh `sources/index.md`.
2. Brainstorming and drafting goes in `notes/`. Never edit `inputs/`.
3. Every claim in `notes/` cites a source ID from `sources/index.md`, or is tagged `[inference]`, `[opinion]`, or `[unverified]`.
4. Before treating any finding as settled, run `/critique notes/<file>.md` to have an independent agent attack it.
5. Run `/synthesize` to fold the critique back into the draft.

## Rules (read these — they're loaded automatically)

- `.claude/references/global/thinking-rules.md` — how to brainstorm and draft
- `.claude/references/global/source-discipline.md` — citation and anti-fabrication rules
- `.claude/references/global/critic-prompt.md` — what the Critic sub-agent runs (read-only; the `/critique` skill uses it)

## Skills available in this project

- `/intake` — inventory `inputs/` into `sources/index.md`
- `/brainstorm <question>` — structured brainstorm against the source packet
- `/critique <file>` — spawn an independent Critic sub-agent to attack a draft
- `/synthesize` — fold the latest critique findings into the draft

## Settings

`.claude/settings.json` configures which models the Thinker and Critic use. They must be different — see `critic-prompt.md` for why.

## Project-specific rules

(Add rules learned during this project. Format: "Don't X / Do Y / Why Z." Periodically distill recurring entries back into the master `references/` folder so future projects inherit them.)

## Out of scope

(List things this project explicitly is *not* doing, to keep Claude from drifting.)
