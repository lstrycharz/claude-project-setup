# plugins/

Plugin install lists and any custom plugin source you maintain.

## Structure

```
plugins/
├── README.md
├── recommended.txt        # Plain-text list of plugins to install per project type
└── custom/                # Your own plugin source code, if any
    └── my-plugin/
        └── plugin.json
```

## How this folder works

Unlike skills (which can be copied directly into a project's `.claude/skills/` folder), plugins are installed via Claude's plugin marketplace command. So this folder is mostly **a record of which plugins should be installed** for which project type — not the plugins themselves.

The `manifest.yaml` references plugin names. The `claude-init` script writes those names into `.claude/recommended-plugins.txt` inside each new project so you have a single command to run after bootstrapping.

## Plugins worth installing

Based on the Trust Insights episode and broader experience:

- **superpowers** — Brainstorming, plan-writing, plan-execution, sub-agent dispatching, parallel agent orchestration. Token-efficient. Originally by Jesse Vincent, acquired by Anthropic. Install for code projects at minimum.
- **marketing** — Already installed in your environment. Covers brand voice, campaign planning, content creation, performance analytics.

## Adding custom plugins

If you build your own plugin (using the `cowork-plugin-management:create-cowork-plugin` skill), drop the source in `plugins/custom/` so it lives alongside your other tooling and is version-controlled here.

## Security note

Plugins from third parties run with significant access. Vet the author and source before installing. Stick to plugins from Anthropic's official marketplace, Trust Insights, or other trusted publishers. The episode flags this explicitly — don't accidentally open your environment to a malicious plugin.
