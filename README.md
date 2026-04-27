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

## Getting started

Setting up the kit takes about five minutes. After that, starting a new project takes about ten seconds.

### Step 1 — Set up the kit on your Mac (one time, ~5 minutes)

You do this once. Open Terminal and run these commands one at a time:

**1. Clone this repo to a stable location on your Mac.**

```bash
git clone https://github.com/lstrycharz/claude-project-setup.git ~/claude-project-setup
```

This downloads the kit into a folder called `claude-project-setup` in your home directory.

**2. Install `yq`, the small tool the kit needs to read its config file.**

```bash
brew install yq
```

(If you don't have Homebrew installed yet, install it first from [brew.sh](https://brew.sh).)

**3. Make `claude-init` runnable from anywhere.**

```bash
echo 'export PATH="$HOME/claude-project-setup/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

This tells your terminal where to find the `claude-init` command so you can run it from any folder, not just from inside the kit.

**4. Verify it worked.**

```bash
claude-init --help
```

You should see the script's usage info. If you see "command not found," open a new Terminal window and try again.

That's it for setup. The kit is installed.

If anything goes wrong, `INSTALL.md` has a more detailed walkthrough including troubleshooting.

### Step 2 — Use it on a new project (every time, ~10 seconds)

Once the kit is set up, every new project follows the same pattern:

**1. Create a folder for your project.** Anywhere on your Mac. Example:

```bash
mkdir ~/Projects/my-new-project
cd ~/Projects/my-new-project
```

**2. Run `claude-init`.** It will show you a list of project types and ask you to pick one:

```bash
claude-init
```

Type the project type name (e.g. `recurring_report`) and press Enter.

**3. The kit copies the right files into a hidden `.claude/` folder inside your project.** That's where your team's standards, templates, and reference material now live for this project.

**4. Open Claude in this project folder.** Claude will pick up the standards automatically — you don't have to paste anything in or remind it of anything.

You're now ready to do the work. Claude will use the loaded standards every time you work in this folder, on this project.

## What's ready vs. what you build

The kit has two layers, and they each pay off at different points.

**Layer 1 — ready to use the moment you install.** The script (`claude-init`), the four starter project types in the manifest, the PRD/Spec/Work Plan templates, and the folder structure all work out of the box. Day one, you can install the kit and start running `claude-init` on real projects. The templates are deliberately generic — they have the right sections; you fill in the project-specific content.

**Layer 2 — built up over time as your team uses the kit.** The reference files (your team's actual standards), the validation checklists (your team's quality criteria), and any custom skills are what *you* contribute over weeks or months. These start empty. They get built as you work on real projects and notice what conventions are worth capturing.

You don't have to build Layer 2 before getting value from the kit. Adopt as little or as much as makes sense. A reasonable progression:

**Day 1.** Install the kit, run `claude-init` on a real project, get the standard PRD/Spec/Work Plan templates. Already useful.

**First couple of weeks.** Look at the four starter project types in `manifest.yaml`. If "Recurring Report" or "Strategic Initiative" don't match the way your team talks about its work, rename them or add new ones. Write a short reference file for the kind of work you do most often — even a single page is useful.

**First couple of months.** Reference files get sharper as you use them. Validation checklists get added — these are short lists of yes/no questions Claude runs against output before declaring it done. Custom skills get built for the things you do repeatedly. The kit captures your team's standards in a way that didn't exist anywhere before.

**Ongoing.** Each time you notice Claude (or a teammate) making the same mistake twice across projects, you update the relevant reference file. The kit gets sharper through use. Lessons that would otherwise stay in individual heads end up captured in shared files.

The starter project types you'll see in `manifest.yaml`:

- **Recurring Report** — for cyclical reporting work that follows a stable structure (monthly KPIs, quarterly reviews, regular performance updates)
- **Multi-Asset Project** — for projects producing multiple deliverables that need shared voice and standards (campaign briefs + assets, policy rollouts with multiple comms pieces, report packages)
- **Research / Analysis** — for one-time projects that synthesize multiple sources into a defensible view (competitive landscapes, deep-dive analyses, ad-hoc business questions)
- **Strategic Initiative** — for larger planning projects that benefit from explicit why/what/how structure (campaign strategy, organizational design, framework redesigns)

These names are starting points. Edit them to match your team's vocabulary the moment they don't fit.

## What you fill in for each project type

The kit ships with a **skeleton** for every reference file the manifest expects — meaning the files exist, with section headings and placeholder notes, ready for you to replace the placeholders with your team's actual content. Nothing is missing. You just need to populate.

Below is exactly which files belong to which project type, so you know what to fill in when you decide to use one.

### Files that ship pre-built and work as-is

These don't need any editing to use. They work for any project type:

- `templates/prd-template.md` — the *why* (audience, goals, outcomes)
- `templates/spec-template.md` — the *what* (components, KPIs, milestones)
- `templates/workplan-template.md` — the *how* (phases, tasks, validation gates)
- `templates/claude-md-starter.md` — project-specific instruction file Claude reads automatically
- `bin/claude-init` — the bootstrap script
- `manifest.yaml` — the project type definitions

### Files that ship as skeletons and need your team's content

For each project type you plan to actually use, fill in the corresponding files in `references/<project-type>/`. Each one starts as a skeleton with section headers and placeholder notes — you replace the placeholders with your team's standards.

**Always-loaded (applies to every project regardless of type):**

| File | What goes in it |
|------|----------------|
| `references/global/general-rules.md` | Voice and tone, forbidden words, formatting conventions, anti-patterns that apply universally. **Start here if you only fill in one file** — it pays off across every project. |

**For `recurring_report` (monthly/quarterly reports):**

| File | What goes in it |
|------|----------------|
| `references/recurring-report/report-rules.md` | First principles, required structure, content requirements per section, tone for the audience |
| `references/recurring-report/visualization-rules.md` | When to use charts vs. tables, axis conventions, what to flag visually |
| `references/recurring-report/report-checklist.md` | Yes/no validation questions Claude runs against the report before delivery |

**For `multi_asset_project` (campaigns, policy rollouts, document packages):**

| File | What goes in it |
|------|----------------|
| `references/multi-asset-project/voice-and-standards.md` | Shared voice across assets, cross-asset messaging consistency, asset-specific exceptions |
| `references/multi-asset-project/asset-coordination-rules.md` | Cross-references, versioning, order of production, approval flow |
| `references/multi-asset-project/multi-asset-checklist.md` | Validation checklist run against the full asset set, not just individual assets |

**For `research_analysis` (competitive landscapes, deep-dive analyses, ad-hoc questions):**

| File | What goes in it |
|------|----------------|
| `references/research-analysis/research-rules.md` | Source rules, age-weighting evidence, citation conventions, anti-patterns |
| `references/research-analysis/research-checklist.md` | Validation checklist focused on rigor and defensibility |

**For `strategic_initiative` (planning documents, big projects):**

| File | What goes in it |
|------|----------------|
| `references/strategic-initiative/planning-rules.md` | Decision rules, milestone rules, stakeholder rules, outcome rules, living-document rules |

### A reasonable order to fill these in

You don't have to populate everything before using the kit. A practical sequence:

1. **First** — `references/global/general-rules.md`. It applies to every project, so the payoff is immediate.
2. **Second** — the rules file for the project type you'll use most. If your team produces a lot of recurring reports, that's `recurring-report/report-rules.md`. If you do a lot of campaigns, `multi-asset-project/voice-and-standards.md`. Pick whichever maps to the work you do most.
3. **Third** — the validation checklist for that same project type. Distill 15–25 yes/no questions from the rules file. The checklist is what catches drift in long sessions.
4. **Then** — populate the other project types over time, as you start using them on real work.

Each rules file can take 30 minutes to fill in if you're working from memory, or 2-3 hours if you want to do external research first. The kit is useful even when files are partial — partial standards are better than no standards.

### Files you can ignore unless you need them

These exist in the manifest as empty arrays (`skills: []`, `plugins: []`) for every project type. You only populate them if you have something to put there:

- **`skills/<skill-name>/SKILL.md`** — Custom skills your team builds for repeated tasks
- **`plugins/`** entries — Lists of Claude plugins to install per project type

Both are optional. The kit works fine without any custom skills or plugins.

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
