# Install Guide

How to install the kit and get `claude-init` on your PATH. Pure bash — no external dependencies (no `yq`, no `jq`).

## Prerequisites

- macOS or Linux (the script is portable bash; Windows works via WSL)
- `git`
- Claude installed and working — this kit adds workflow scaffolding to projects you'll use with Claude. It doesn't install Claude itself.

## Step 1 — Clone

```bash
git clone https://github.com/lstrycharz/claude-project-setup.git ~/claude-project-setup
cd ~/claude-project-setup
```

SSH variant if you've set up an SSH key with GitHub:

```bash
git clone git@github.com:lstrycharz/claude-project-setup.git ~/claude-project-setup
```

You can put it anywhere; `~/claude-project-setup` is just the convention. The script resolves its own location, so it works wherever you clone it.

## Step 2 — Put `claude-init` on your PATH

Add this line to your `~/.zshrc` (or `~/.bashrc` for bash):

```bash
export PATH="$HOME/claude-project-setup/bin:$PATH"
```

The one-liner version:

```bash
echo 'export PATH="$HOME/claude-project-setup/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

Verify:

```bash
which claude-init
# /Users/you/claude-project-setup/bin/claude-init

claude-init --help
# Prints usage info
```

If `which claude-init` returns nothing, your shell hasn't picked up the new PATH. Open a fresh terminal or `source ~/.zshrc` again.

## Step 3 — Try it on a test project

```bash
mkdir -p ~/test-claude-init && cd ~/test-claude-init
claude-init
```

You should see directories created and starter files written. Re-run the same command; everything should report `[skip - exists]`. That confirms the script is idempotent and safe to re-run.

To preview without writing anything:

```bash
claude-init --dry-run
```

## Step 4 — Configure your models

Open `~/test-claude-init/.claude/settings.json`. Set `thinker_model` and `critic_model` to two **different** Claude models you have access to. The defaults (`claude-sonnet-4-6` for Thinker, `claude-opus-4-7` for Critic) are reasonable starting points — adjust to match what your account supports.

The full reasoning for why they must be different lives in `.claude/references/global/critic-prompt.md` under "Why this prompt is shaped this way."

## Step 5 — Use it on a real project

```bash
cd ~/Projects/my-research-project
claude-init
```

Then drop source materials into `inputs/`, open the project in Claude, and run `/intake`. From there the workflow is:

1. `/intake` — build the source index
2. `/brainstorm <question>` — produce a structured draft
3. `/critique <file>` — spawn the independent Critic
4. `/synthesize` — fold the critique back in
5. Repeat as needed

## Step 6 — Updating an existing project after improving the master kit

When you improve a rule or a skill in `~/claude-project-setup/`, push the change to your existing projects:

```bash
cd ~/Projects/old-research-project
claude-init --update
```

`--update` overwrites only files in `.claude/references/` and `.claude/skills/`. Your `CLAUDE.md`, `notes/`, `sources/`, and `inputs/` are never touched.

## Troubleshooting

**`claude-init: command not found`**

Your PATH doesn't include the kit's `bin/` directory. Run:

```bash
echo $PATH | tr ':' '\n' | grep claude-project-setup
```

If empty, the line in your `~/.zshrc` didn't take effect. Open a fresh terminal or `source ~/.zshrc` manually.

**Files copied but not visible in Finder**

`.claude/` is hidden by default on macOS (starts with a dot). Press `Cmd+Shift+.` in Finder to toggle hidden files.

**"refusing to scaffold inside the claude-project-setup kit itself"**

Run `claude-init` from a *target* project folder, not from inside `~/claude-project-setup/`. The kit's own directory is protected from being scaffolded into itself.

## Optional — commit your improvements

Treat the kit like a small product. When you tune a rule or add a skill, commit it with a message explaining *why*. Six months from now you'll thank yourself, and if you push to your fork, teammates inherit the same improvements.
