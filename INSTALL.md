# Install Guide

Walks you through moving this scaffold from its current location into a permanent home on your Mac, putting it under git, publishing it as a private repo on GitHub, and putting `claude-init` on your `PATH` so it works from any project folder.

## Step 1 — Pick a permanent location

`claude-project-setup` should live somewhere stable and easy to reach. Common choices:

- `~/claude-project-setup/` — Top of your home directory. Easy to reach from any terminal. Recommended.
- `~/Projects/claude-project-setup/` — If you already keep a `Projects` folder for repos.
- `~/dev/claude-project-setup/` — If you prefer that convention.

Pick one. Throughout the rest of this guide I'll assume `~/claude-project-setup/`.

## Step 2 — Move the scaffold to its permanent location

Open Terminal on your Mac and run:

```bash
# Replace the source path with wherever you copied this scaffold to.
mv ~/Downloads/claude-project-setup ~/claude-project-setup
cd ~/claude-project-setup
```

If you'd rather copy than move, use `cp -R` instead of `mv`.

## Step 3 — Initialize git

```bash
cd ~/claude-project-setup
git init
git add .
git commit -m "Initial scaffold"
```

## Step 4 — Push to a private GitHub repo

This is a long-lived asset. You want backup and history.

1. Create a new private repo on GitHub named `claude-project-setup` (don't initialize it with a README — yours is already done).
2. Wire up the remote and push:

```bash
git remote add origin git@github.com:lstrycharz/claude-project-setup.git
git branch -M main
git push -u origin main
```

## Step 5 — Install the prerequisite for `claude-init`

The script uses `yq` to parse the manifest. Install it once:

```bash
brew install yq
```

(If you don't have Homebrew, install it first from brew.sh, or replace `yq` in `bin/claude-init` with another YAML parser of your choice.)

## Step 6 — Put `claude-init` on your `PATH`

This is what makes the entry point clean. Instead of typing `~/claude-project-setup/bin/claude-init` every time, you just type `claude-init` from any project folder.

Add this to your `~/.zshrc` (or `~/.bashrc` if you use bash):

```bash
export PATH="$HOME/claude-project-setup/bin:$PATH"
```

Reload your shell:

```bash
source ~/.zshrc
```

Verify:

```bash
which claude-init
# Should print: /Users/lukaszstrycharz/claude-project-setup/bin/claude-init
claude-init --help
# Should print the script's usage block
```

> **Naming note.** Your other repo's entry point is `init-claude` (the order is reversed). Keeping them distinct prevents confusion. If you ever want a single mental shortcut, `claude-init` = projects, `init-claude` = code.

## Step 7 — Edit the manifest

Open `manifest.yaml` and adjust the project types to match the work you actually do. The scaffold ships with four examples (`blog_content`, `data_analysis`, `research`, `code`). The `code` entry is intentionally minimal here — your `claude-setup` repo handles real code projects. You can leave it, repurpose it, or remove it entirely.

## Step 8 — Populate the folders

The folders ship empty (with READMEs only). Filling them is the real work and happens over time. Suggested first additions:

1. **A first reference file.** Pick the project type you do most often (blog content is the natural first candidate). Run a deep research prompt in Gemini, Perplexity, and one other tool on "best practices for high-performing SEO-optimized evergreen blog posts." Merge the three reports into a single `references/blog-content/seo-rules.md`.
2. **A first checklist.** Distill that reference file into a 15–25 item checklist at `references/blog-content/blog-checklist.md`. Each item is a yes/no validation question.
3. **Your forbidden-words list.** Codify it as `references/blog-content/forbidden-words.md`.
4. **Lift one or two skills you already use.** Copy them from `~/.claude/skills/` into `skills/` here, or create new ones with the skill-creator skill.

Don't try to populate everything at once. Build out one project type fully, use it on a real project, then expand to the next.

## Step 9 — Try it

Create a test project folder somewhere outside `~/claude-project-setup/`:

```bash
mkdir -p ~/Projects/test-claude-init
cd ~/Projects/test-claude-init
claude-init
```

It will prompt you for a project type and copy the matching assets into a `.claude/` folder inside `test-claude-init`. Re-run it — you should see "skip — exists" for everything, confirming idempotency.

To preview without copying:

```bash
claude-init --type=blog_content --dry-run
```

## Step 10 — Commit changes regularly

Treat this repo like any other production codebase. Every meaningful change to a rules file, checklist, or template gets a commit with a message that explains *why*. You'll thank yourself in six months when a rule changed and you don't remember the reason.

A reasonable commit cadence:

- Add a new reference file → commit
- Update a checklist after a project taught you something → commit
- New project type → commit
- Anti-pattern lesson distilled from a `CLAUDE.md` back into the master rules → commit

## Troubleshooting

- **`yq: command not found`** — Install with `brew install yq`. Verify your `$PATH` includes `/opt/homebrew/bin` (Apple Silicon) or `/usr/local/bin` (Intel Macs).
- **`claude-init: command not found`** — Verify `$HOME/claude-project-setup/bin` is on your `$PATH`. Run `echo $PATH | tr ':' '\n' | grep claude-project-setup` — if it returns nothing, the export in your `~/.zshrc` didn't take effect. Reload your shell or open a new terminal window.
- **Script can't find manifest.yaml** — Make sure you're running `claude-init` from inside a target project folder, not from inside `claude-project-setup/` itself. The script uses its own location to find the manifest, but it expects to be invoked from a *target* project.
- **Files copied but not visible in Finder** — `.claude/` is hidden by default (leading dot). Press Cmd+Shift+. in Finder to toggle visibility.
