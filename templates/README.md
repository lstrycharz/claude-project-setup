# templates/

Skeleton documents with the standard sections pre-populated. Drop them into a new project, fill in the project-specific content, and you have a complete project plan.

## The three core templates

Every non-trivial project benefits from three documents at the start, in order:

1. **PRD** (Product Requirements Document) — the *why*. Who is this for, what problem are we solving, what does success look like?
2. **Spec** — the *what*. What components or sections does the deliverable have? What KPIs or milestones are we tracking?
3. **Work Plan** — the *how*. What's the step-by-step plan to get from start to finished deliverable?

This sequence is universal — it applies whether you're producing a campaign brief, a research synthesis, a strategy document, an analysis report, or anything else. The vocabulary changes by domain; the underlying structure doesn't.

For smaller or more routine projects, you may not need all three documents. Use what's useful, skip what isn't.

## What's in this folder

```
templates/
├── README.md
├── prd-template.md
├── spec-template.md
├── workplan-template.md
└── claude-md-starter.md
```

The `claude-md-starter.md` is a starter `CLAUDE.md` for new projects. A `CLAUDE.md` is a project-specific instruction file Claude reads automatically — it's the right place to capture project-specific rules, voice notes, and any anti-patterns you discover during the project itself. The starter is mostly empty by design: the most useful content in a `CLAUDE.md` is what you learn while doing the work, not what you predicted before starting.

## Using these in a project

When `claude-init` bootstraps a new project, the relevant templates land in the project's `.claude/templates/` folder. Copy them up into the project root (or wherever you want them in your project structure) and fill them in. Don't edit the master copies in place — the master copies are the templates everyone on your team inherits, so changes here affect every future project.

## Customizing

Edit the templates as your team's standards evolve. If you find yourself adding the same section to every PRD, add it to the template. If a section is consistently empty across projects, remove it. The templates should reflect the work your team actually does, not a generic version.

If different project types need very different templates (e.g., a creative campaign brief vs. an HR policy proposal), you can create project-type-specific variants — `prd-creative.md`, `prd-hr.md`, etc. — and reference them from the relevant project type in `manifest.yaml`. The generic templates work well as a single source for most teams to start with; specialize only when you find yourself wanting to.
