# CLAUDE.md — [Project Name]

> **Purpose:** Project-specific instructions for Claude. Per Anthropic's guidance, the best content here is anti-patterns Claude has fallen into during this project — explicit "don't do X, do Y instead" rules. Add to this file as the project progresses; don't try to anticipate everything upfront.

## Project context

One paragraph: what this project is, the audience, the deliverable.

## Reference materials

- PRD: `prd.md`
- Spec: `spec.md`
- Work plan: `workplan.md`
- Rules: see `.claude/references/`
- Checklist: `.claude/checklists/[relevant-checklist].md`

## Voice and tone

(For writing projects.) Describe the voice the deliverable should have. Reference the brand voice rules file if applicable.

## Project-specific rules

Rules that apply to this project specifically — not covered by the global references.

- Rule:
- Rule:

## Anti-patterns observed during this project

Add entries here whenever Claude makes a mistake worth flagging. Format:

> **Don't:** [What Claude did wrong]
> **Do:** [What it should have done instead]
> **Why:** [The reason this matters]

(Empty at project start. Populate as you go.)

## Validation requirements

Before declaring any output done, Claude must run the project's validation checklist. Reference the file in `.claude/checklists/`.

## Out of scope reminders

Things this project explicitly is *not* doing. List them here so Claude doesn't drift.

---

*Distill recurring entries from the "anti-patterns observed" section back into the master `references/` folder so future projects inherit the lessons.*
