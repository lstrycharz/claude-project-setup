# claude-project-setup

A single, version-controlled home for everything that prepares Claude (Cowork, Code, or any other agentic system) to do high-quality non-code work: skills, plugins, reference rules, validation checklists, and templates — wired together by a single entry-point script (`claude-init`) that bootstraps any new project with the right context.

> **Scope note.** This repo is the companion to [`claude-setup`](https://github.com/lstrycharz/claude-setup), which handles software development projects. `claude-project-setup` handles everything else: writing, analysis, research, marketing, content. The two stay deliberately separate.

## Why this exists

Most people open Claude and start typing. The Trust Insights "Setting Up Claude Code for Success" episode makes the case — and experience confirms — that the work which determines whether Claude produces high-quality, consistent output happens *before* you open the tool. That preparation is reusable across every project, but only if it lives in one canonical place. This repo is that place.

The benefits of centralizing:

- **Portability.** When you switch from Claude Cowork to Code, OpenCode, Codex, or whatever comes next, you change one path and your entire library moves with you.
- **Consistency.** Every project starts with the same governance, the same checklists, and the same reference material. No drift.
- **Improvement compounds.** When you discover an anti-pattern or a new best practice, you update the master copy once and every future project inherits it.
- **Auditability.** Git history tells you when a rule changed, what changed, and why.

## Folder structure

```
claude-project-setup/
├── README.md             # This file
├── INSTALL.md            # Step-by-step setup on your Mac
├── .gitignore            # Excludes secrets, OS junk, etc.
├── manifest.yaml         # Maps project types to assets
├── bin/
│   └── claude-init       # Idempotent project bootstrapper (entry point)
├── skills/               # Reusable skill definitions (SKILL.md folders)
├── plugins/              # Plugin install lists / custom plugin source
├── references/           # Deep-research rules files, per project type
└── templates/            # PRD / Spec / Work Plan / CLAUDE.md starters
```

The five top-level content folders mirror the asset types Claude understands. The manifest is the brain that maps "I'm starting a blog post project" to "copy these references, these templates, install these skills." The `bin/claude-init` script is the single entry point that reads the manifest and does the work.

## How to use it

1. Edit `manifest.yaml` to define the project types you actually work on.
2. Drop your skills, plugins, references, and templates into the matching subfolders.
3. When you start a new project, `cd` into the project folder and run `claude-init`. It will read the manifest, ask which project type you're starting, and copy the right assets into the project's `.claude/` folder.
4. Commit changes to this repo regularly. Treat it like a product.

## What goes where

- **bin/** — The `claude-init` script. Add it to your `PATH` (see `INSTALL.md`) so it can be run from any project folder.
- **skills/** — Each skill is its own subfolder containing a `SKILL.md` file. Lift these from `~/.claude/skills/` or build new ones with the skill-creator skill.
- **plugins/** — Plugin install manifests and any custom plugin source. The actual install happens via Claude's plugin command; this folder records what should be installed for which project type.
- **references/** — Long-form rules files, one subfolder per domain (e.g., `references/blog-content/`, `references/data-analysis/`). These are deep-research outputs — first principles, hard constraints, anti-patterns, design patterns, hidden gotchas.
- **templates/** — Skeleton documents with the standard sections pre-populated. PRD, Spec, and Work Plan are the core three.

## What this repo is *not*

It's not a project workspace. Don't put actual project files here. `claude-project-setup` is a library; projects live elsewhere and pull from it via `claude-init`.

It's also not for code projects. Use [`claude-setup`](https://github.com/lstrycharz/claude-setup) for those — it has hooks, secret scanning, slash commands, and `PROGRESS.md` cross-session memory built specifically for software work.

## Maintenance discipline

- Treat this repo like any other production codebase. Commit messages should explain *why* a rule changed.
- Periodically distill `CLAUDE.md` lessons from real projects back into the rules files here.
- Review references quarterly. AI best practices move fast.
- Anything you do more than three times → turn it into a skill or template here.

## Quick start

See `INSTALL.md` for the full walkthrough. The short version:

```bash
git clone git@github.com:lstrycharz/claude-project-setup.git ~/claude-project-setup
brew install yq
echo 'export PATH="$HOME/claude-project-setup/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc

# Then, in any project folder:
cd ~/Projects/my-new-blog-post
claude-init
```
