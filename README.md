# claude-project-setup

A reusable starter kit that gives every new Claude project the same ground rules, templates, and reference material — automatically.

If you use Claude for work, you know the experience: every project starts with you re-explaining your standards, your preferred structure, your style rules, your preferences. Every. Time. This kit eliminates that step. You set up your standards once, then bootstrap any new project with a single command.

It's designed to be useful to any team — creative, HR, analytics, or anything else. The examples in this README come from those three, but the underlying mechanics work for any work where standards, structure, and consistency matter.

---

## What it actually does

When you start a new project — a quarterly review, a campaign brief, a new policy document, a research synthesis, anything — you run one command from your project folder:

```bash
claude-init
```

The command asks what kind of work this is, then drops the relevant rules, templates, and reference material into a hidden `.claude/` folder inside your project. From that moment on, Claude reads those standards automatically every time you work in that folder. You stop re-typing instructions; Claude stops drifting from your conventions.

Think of it as the difference between briefing a contractor every time vs. handing them a folder of standards they already know to follow.

## When would you actually use this?

Four concrete scenarios where this kit earns its keep, with how each one might look on different teams:

**A recurring report you produce on a regular cadence.** Every month or quarter you produce the same kind of report — same structure, same metrics, same conventions, same audience expectations. Without standards loaded automatically, you fight to remember the format and the things to flag. With the kit, all of that loads with one command. You focus on the substance, not on re-establishing what "good" looks like.

> *On the analytics team:* a monthly executive KPI memo or quarterly performance review.
> *On the HR team:* a quarterly hiring funnel update or people analytics review.
> *On the creative team:* a monthly campaign performance recap or content effectiveness report.

**A multi-asset deliverable where consistency matters across pieces.** You're producing several outputs that need to share voice, framing, and conventions — even if different team members touch different pieces. Without shared standards, the assets drift apart in tone and quality. With them, every piece Claude touches knows the same rules.

> *On the creative team:* a campaign with brief, landing page copy, email sequence, and social posts.
> *On the HR team:* a policy rollout with handbook update, all-staff email, manager talking points, and an FAQ.
> *On the analytics team:* a quarterly review with executive summary, full report, dashboard documentation, and methodology appendix.

**A research or analysis project drawing on multiple sources.** You need to synthesize information from multiple places into a coherent, defensible view. The kit gives Claude a methodology — triangulate sources, surface contradictions, flag single-sourced claims — that turns a "vibes" summary into something rigorous.

> *On the creative team:* a competitive landscape of brand positioning, or a content-format study across competitors.
> *On the HR team:* a people-analytics deep dive on a specific question (why is attrition up in Department X, what's driving manager survey scores).
> *On the analytics team:* a customer-segment analysis, an ad-hoc business question, or a market sizing exercise.

**A strategic deliverable larger than a typical week's work.** Something where you want structure, clear milestones, and a way to track decisions. The kit ships with templates for the *why* (PRD), *what* (Spec), and *how* (Work Plan), turning vague "let's plan this thing" into a structured sequence with measurable outcomes.

> *On the creative team:* a strategy document for a major campaign or rebrand.
> *On the HR team:* an organizational design document, a workforce plan, or a benefits redesign proposal.
> *On the analytics team:* a data strategy roadmap, a measurement framework, or a KPI redesign initiative.

If your day-to-day work is light and Claude already handles it well, you may not need this. The kit pays off when projects are big enough or recurring enough that having standards pre-loaded saves real time — and especially when multiple people need to produce work that looks like it came from the same place.

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

The kit ships with four starter project types — but they're examples. The real value comes from editing them to match the work your team actually does.

In `manifest.yaml` you'll find:

- **Recurring Report** — for cyclical reporting work that follows a stable structure
- **Multi-Asset Project** — for projects where multiple deliverables need shared voice and standards
- **Research / Analysis** — for projects that synthesize multiple sources into a defensible view
- **Strategic Initiative** — for larger planning projects that benefit from PRD / Spec / Work Plan structure

You'll edit the manifest to rename or add project types that match your team's vocabulary, and you'll fill in the `references/` and `skills/` folders with the standards you want every project of each type to inherit. There's no rush — populate gradually as you go.

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

When you discover a recurring rule or anti-pattern worth enforcing, add it to the relevant reference file and commit. When a project type stops fitting your work, edit it. Anything you find yourself doing repeatedly across projects is a candidate to add here.

The kit gets sharper the more you use it — and if multiple people on a team contribute, it captures collective experience that would otherwise stay in individual heads.

## Questions or improvements

Open an issue or a pull request on this repo. The kit is meant to evolve.

## License

MIT — see `LICENSE` file.
