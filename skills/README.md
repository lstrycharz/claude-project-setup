# skills/

Reusable skill definitions. A skill is a small instruction file that tells Claude how to handle a specific kind of task — think of it as "follow this checklist" or "always include these elements when you do X." Each skill in this folder lives in its own subfolder and contains a `SKILL.md` file that describes what the skill does and when Claude should use it.

## Structure

```
skills/
├── my-skill-name/
│   ├── SKILL.md
│   └── (optional supporting files: prompts, templates, scripts)
└── another-skill/
    └── SKILL.md
```

## How to populate this folder

You have three options for getting skills into this folder.

**Lift skills you already use.** If you've installed skills for Claude in the past, they live in your Claude skills folder (typically `~/.claude/skills/`). Copy folders you use frequently into this repo so they're version-controlled and travel with the kit. This is the fastest way to get started.

**Create new skills.** If you don't have any custom skills yet, ask Claude to help you build one. Claude has a built-in skill called `skill-creator` that walks through the process. Anything you find yourself doing more than three times — across any kind of work — is a good candidate to turn into a skill so you only have to define it once.

**Reference each skill in `manifest.yaml`.** For each skill in this folder, add it to the relevant project type's `skills:` list in the manifest. That way, when someone runs `claude-init` for that project type, the skill gets installed automatically.

## What makes a good skill

A few characteristics worth aiming for when you build or borrow a skill:

- A clear, specific trigger description. The skill's description should make it obvious when Claude should reach for it. Vague triggers ("for any writing task") cause skills to misfire.
- A focused job. One workflow per skill. If a skill is doing three different things, split it into three skills.
- Self-contained instructions. The `SKILL.md` should be readable on its own, without the reader needing context from outside the file.
- Examples of good vs. bad output, where helpful. Skills that show what they expect tend to produce more consistent results than skills that only describe what they expect.

## A note on built-in skills

Claude ships with a number of official skills built in. You don't need to copy those into this folder — they're already available. This folder is for skills that are *yours*: custom-built or modified to match how your team actually works. Built-in skills sit alongside yours; they don't compete.
