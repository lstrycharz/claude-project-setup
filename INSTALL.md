# Install Guide

Walks you through installing this kit on your Mac, putting it under git, and getting `claude-init` working from any project folder.

This guide assumes you're comfortable opening Terminal and running a few commands. You don't need to be a developer — but you should be willing to follow the steps in order.

## What you'll need first

Before starting, make sure you have:

- A Mac (these instructions are Mac-specific; the kit also works on Linux with minor adjustments)
- [Homebrew](https://brew.sh) installed (for installing the YAML parser this kit needs). If you don't have it, run the install command on the Homebrew homepage first.
- [Git](https://git-scm.com) installed. Mac usually has it; check with `git --version`.
- Claude installed and working. This kit doesn't install Claude itself — it adds standards and structure to projects you'll work on with Claude.

## Step 1 — Pick a permanent location

`claude-project-setup` should live somewhere stable and easy to reach. Common choices:

- `~/claude-project-setup/` — Top of your home directory. Easy to reach from any terminal. **Recommended.**
- `~/Projects/claude-project-setup/` — If you already keep a `Projects` folder for repos.
- `~/dev/claude-project-setup/` — If you prefer that convention.

Pick one. The rest of this guide assumes `~/claude-project-setup/`.

## Step 2 — Clone the repo

Open Terminal and run:

```bash
git clone https://github.com/lstrycharz/claude-project-setup.git ~/claude-project-setup
cd ~/claude-project-setup
```

If you'd rather use SSH (and have an SSH key set up with GitHub):

```bash
git clone git@github.com:lstrycharz/claude-project-setup.git ~/claude-project-setup
```

## Step 3 — Install the prerequisite for `claude-init`

The script uses [`yq`](https://github.com/mikefarah/yq) to read the project type definitions. Install it once:

```bash
brew install yq
```

Verify it installed:

```bash
yq --version
```

## Step 4 — Put `claude-init` on your `PATH`

This is what makes the entry point clean. Instead of typing the full path every time, you just type `claude-init` from any project folder.

Add this line to your `~/.zshrc` file (or `~/.bashrc` if you use bash):

```bash
export PATH="$HOME/claude-project-setup/bin:$PATH"
```

If you're not sure how to edit `~/.zshrc`, the simplest way is:

```bash
echo 'export PATH="$HOME/claude-project-setup/bin:$PATH"' >> ~/.zshrc
```

Then reload your shell:

```bash
source ~/.zshrc
```

Verify it worked:

```bash
which claude-init
# Should print something like: /Users/yourname/claude-project-setup/bin/claude-init

claude-init --help
# Should print the script's usage info
```

If `which claude-init` returns nothing, your shell didn't pick up the new PATH. Open a fresh Terminal window and try again.

## Step 5 — Edit the manifest to match your work

Open `~/claude-project-setup/manifest.yaml` in your editor. The kit ships with four starter project types — Recurring Report, Multi-Asset Project, Research / Analysis, and Strategic Initiative. These are designed to span common patterns across creative, HR, analytics, and similar teams. Adjust them, rename them, or add new ones to match the work your team actually does.

## Step 6 — Populate the folders gradually

The folders ship empty (with READMEs only). Filling them is the real value of the kit, and it happens over time, not in one sitting.

A reasonable starting sequence:

1. **A first reference file.** Pick the project type you do most often. Write a 1–2 page document covering your standards for that kind of work — what good looks like, what to avoid, what conventions to follow. Save it inside `references/<project-type>/`.
2. **A first checklist.** Distill that reference file into a 15–25 item checklist of yes/no validation questions. Save it alongside the reference file.
3. **Lift one or two skills you already use** if you've built any — copy them from your existing Claude skills folder into `skills/` here.

Don't try to populate everything at once. Build out one project type fully, use it on a real project, then expand to the next.

## Step 7 — Try it on a test project

Create a test project folder somewhere outside `~/claude-project-setup/`:

```bash
mkdir -p ~/Projects/test-claude-init
cd ~/Projects/test-claude-init
claude-init
```

The script will prompt you to pick a project type and copy the matching assets into a hidden `.claude/` folder inside `test-claude-init`. Re-run the same command — you should see "skip — exists" for everything, confirming the script is safe to re-run without overwriting.

To preview what would be copied without actually copying anything:

```bash
claude-init --type=recurring_report --dry-run
```

(Replace `recurring_report` with whichever project type you're testing — the kit ships with `recurring_report`, `multi_asset_project`, `research_analysis`, and `strategic_initiative`.)

## Step 8 — Commit changes regularly

Treat this repo like a small product. Every meaningful change to a rules file, checklist, or template gets a commit with a message that explains *why*. Six months from now you'll thank yourself.

A reasonable commit cadence:

- Add a new reference file → commit
- Update a checklist after a project taught you something → commit
- New project type added → commit
- Lessons learned from a real project distilled back into the master rules → commit

If you're working with teammates, push to GitHub regularly so others get the benefit of your improvements.

## Troubleshooting

**`yq: command not found`**

Install with `brew install yq`. If you've installed it but the command still isn't found, your shell may not have picked up Homebrew's location. Check that `/opt/homebrew/bin` (Apple Silicon) or `/usr/local/bin` (Intel Macs) is in your `$PATH`.

**`claude-init: command not found`**

Verify `$HOME/claude-project-setup/bin` is on your `$PATH`. Run:

```bash
echo $PATH | tr ':' '\n' | grep claude-project-setup
```

If it returns nothing, the line you added to `~/.zshrc` didn't take effect. Open a fresh Terminal window and try again, or run `source ~/.zshrc` manually.

**Script can't find manifest.yaml**

Make sure you're running `claude-init` from inside a target project folder, not from inside `claude-project-setup/` itself. The script uses its own location to find the manifest, but it expects to be invoked from a *target* project folder.

**Files copied but not visible in Finder**

The `.claude/` folder is hidden by default (it starts with a dot, which macOS treats as hidden). Press Cmd+Shift+. in Finder to toggle hidden files on. To revert, press the same shortcut again.
