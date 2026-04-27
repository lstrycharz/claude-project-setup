# plugins/

Plugin install lists and any custom plugin source you maintain. Plugins are bundles of capabilities you install into Claude — similar to a browser extension. They can add specialized skills, commands, integrations with other tools, or whole workflow patterns.

## Structure

```
plugins/
├── README.md
├── recommended.txt        # Plain-text list of plugins to install per project type
└── custom/                # Your own plugin source code, if you build any
    └── my-plugin/
        └── plugin.json
```

## How this folder works

Unlike skills (which can be copied directly into a project's `.claude/skills/` folder), plugins are installed through Claude's plugin marketplace command. So this folder doesn't contain the plugins themselves — it contains a record of *which plugins should be installed* for which project type.

The `manifest.yaml` references plugin names. When you run `claude-init` for a project type, the script writes those names into a `recommended-plugins.txt` file inside the new project's `.claude/` folder. From there, you (or a teammate setting up their machine) can install them via Claude's plugin command.

## Plugins worth considering

Two plugins are worth knowing about regardless of your team:

- **superpowers** — official Anthropic plugin. Adds workflows for brainstorming, plan-writing, plan-execution, and dispatching multiple Claude agents in parallel. Most useful for non-routine work where structure matters — bigger projects, multi-source research, complex deliverables. Less useful for routine work that's already well-handled by skills.
- **marketing** — covers brand voice, campaign planning, content creation, and performance analytics. Useful if your team produces marketing or communications content regularly.

Beyond these, the marketplace has plugins for many specific workflows and integrations. Browse what's available before assuming you need to build something custom.

## Adding custom plugins

If your team needs something specific that doesn't exist in the marketplace, you can build a custom plugin. Drop the source in `plugins/custom/` so it lives alongside your other tooling and is version-controlled here.

## A note on security

Plugins from third parties run with significant access to your environment. Vet the author and source before installing anything. Stick to plugins from Anthropic's official marketplace or other trusted publishers. Don't install plugins from unfamiliar sources without reviewing them — the cost of a malicious plugin is much higher than the cost of doing without one.
