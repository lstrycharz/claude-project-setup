# claude-project-setup

A reusable starter kit that gives every new Claude project the same ground rules, templates, and reference material — automatically.

If you use Claude for work, you know the experience: every project starts with you re-explaining your standards, your preferred structure, your style rules, your preferences. Every. Time. This kit eliminates that step. You set up your standards once, then bootstrap any new project with a single command.

---

## What it actually does

When you start a new project — a research brief, a campaign plan, a monthly client report, anything — you run one command from your project folder:

```bash
claude-init
```

The command asks what kind of work this is, then drops the relevant rules, templates, and reference material into a hidden `.claude/` folder inside your project. From that moment on, Claude reads those standards automatically every time you work in that folder. You stop re-typing instructions; Claude stops drifting from your conventions.

Think of it as the difference between briefing a contractor every time vs. handing them a folder of standards they already know to follow.

## When would you actually use this?

Some concrete scenarios where this earns its keep:

**A recurring monthly client report.** Every month you produce the same kind of analysis — same metrics, same structure, same conventions. Without standards loaded automatically, you fight to remember the format and the things to flag. With the kit, all of that loads with one command. You focus on the analysis, not on re-establishing what "good" looks like.

**A new client onboarding.** Different brand voice, different industry context, different standards from your usual work. The kit lets you set up a project with the right voice and standards loaded from the start, so Claude isn't guessing or pulling from generic defaults.

**A multi-asset campaign launch.** You're producing a brief, an email sequence, landing page copy, and social posts. Different assets, but they need consistent voice and brand rules across all of them. The kit ensures every piece Claude touches knows the same rules — even when different team members work on different assets.

**A quarterly strategic deliverable.** Something bigger than a normal week's work. The kit ships with templates for a project's *why* (PRD), *what* (Spec), and *how* (Work Plan), turning vague "let's plan this" into a structured sequence with measurable outcomes.

If your day-to-day work is light and Claude already handles it well, you may not need this. The kit pays off when projects are big enough or recurring enough that having standards pre-loaded saves real time.

## What's in the kit

```
claude-project-setup/
├── README.md              # This file
├── INSTALL.md             # Step-by-step setup on your Mac
├── manifest.yaml          # Defines project types and what they need
├── bin/
│   └── claude-init        # The command you run from new project folders
├── skills/                # Custom skill files (small instruction sets Claude reads)
├── plugins/               # Lists of Claude plugins to install per project type
├── references/            # Long-form rules and best-practices docs per domain
└── templates/             # Starter docs: PRD, Spec, Work Plan, project rules file
```

A few terms in plain English, in case you're new to Claude:

- **Skill** — a small instructional file that tells Claude how to handle a specific kind of task. Think "follow this checklist" or "always include these elements."
- **Plugin** — a bundle of capabilities you install into Claude (similar to a browser extension).
- **Reference file** — a longer document with rules, best practices, or domain knowledge that Claude reads at the start of a project.
- **Template** — a starter document with the standard sections pre-filled, ready for you to add the project-specific content.
- **The `.claude/` folder** — a hidden folder Claude looks at inside any project. The setup script copies the right files there for each new project. (Hidden folders start with a dot; in Finder, press Cmd+Shift+. to see them.)

## How it works, in practice

You only do this once: install the kit on your Mac and put it on your `PATH`. (Full instructions in `INSTALL.md`.)

Then, every time you start a new project:

1. Create a folder for the project, anywhere on your Mac.
2. Open Terminal in that folder.
3. Run `claude-init`.
4. Pick the project type when prompted.
5. The kit creates a `.claude/` folder inside your project with the right rules, templates, and references already loaded.
6. Open Claude. It will pick up the project's standards automatically.

No re-explaining. No re-pasting. Standards stay loaded; you focus on the work.

## What's already included vs. what you customize

The kit ships with three starter project types — but they're examples. The real value comes from editing them to match the work you actually do.

In `manifest.yaml` you'll find:

- **Blog / Evergreen Content** — long-form web content
- **Marketing Data Analysis** — performance reports, traffic, retention
- **Research / Synthesis** — competitive intelligence, market research

You'll edit the manifest to add project types that match your team's work, and you'll fill in the `references/` and `skills/` folders with the standards you want every project of each type to inherit. There's no rush — populate gradually as you go.

## Setup at a glance

For the full walkthrough, see `INSTALL.md`. The short version, assuming you're on a Mac:

```bash
# Clone this repo somewhere stable.
git clone https://github.com/lstrycharz/claude-project-setup.git ~/claude-project-setup

# Install the one tool the script needs (yq is a YAML parser).
brew install yq

# Make claude-init runnable from any folder.
echo 'export PATH="$HOME/claude-project-setup/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc

# Test it on any new project folder.
mkdir -p ~/Projects/my-first-project
cd ~/Projects/my-first-project
claude-init
```

If you're not on a Mac, the kit will still work but you'll need to adapt the install steps to your shell and package manager.

## Companion repo for software work

If you write code with Claude, use [`claude-setup`](https://github.com/lstrycharz/claude-setup) instead. That repo has security hooks, slash commands, and project-progress tracking tailored specifically for software development. The two repos do not overlap — `claude-setup` for code, `claude-project-setup` for everything else.

## Maintenance

Treat this kit like a small internal product:

When you discover a recurring rule, anti-pattern, or convention worth enforcing, add it to the relevant reference file and commit. When a project type stops fitting your work, edit it. Anything you find yourself doing repeatedly across projects is a candidate to add here. The kit gets sharper the more you use it — and if multiple people on a team contribute, it captures collective experience that would otherwise stay in individual heads.

## Questions or improvements

Open an issue or a pull request on this repo. The kit is meant to evolve.
