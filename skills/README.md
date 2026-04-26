# skills/

Reusable skill definitions. Each skill lives in its own subfolder and contains a `SKILL.md` file describing what it does and when to trigger it.

## Structure

```
skills/
├── my-skill-name/
│   ├── SKILL.md
│   └── (optional supporting files: scripts, templates, prompts)
└── another-skill/
    └── SKILL.md
```

## How to populate this folder

1. **Lift existing skills.** Skills you've already installed for Claude Code or Cowork live in `~/.claude/skills/` or in plugin caches. Copy folders you use frequently into this repo so they're version-controlled and portable.
2. **Create new skills.** Use the `skill-creator` skill to scaffold new ones. Anything you find yourself doing more than three times is a skill candidate.
3. **Reference them in `manifest.yaml`.** Map each skill to the project types it belongs to so `claude-init` knows when to install it.

## What makes a good skill

- A clear, specific trigger description (when should Claude reach for this?)
- A focused job (one workflow per skill)
- Self-contained instructions in `SKILL.md` — no implicit context required
- Example inputs and outputs where helpful

## Notes

Skills synced from third parties (like Anthropic's official skills) should generally stay in their managed location, not be copied here. This folder is for *your* skills — custom or modified — that you want under your own version control.
