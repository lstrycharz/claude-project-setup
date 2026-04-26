# templates/

Skeleton documents with the standard sections pre-populated. Drop them into a new project, fill them in, and you have a complete project plan.

## The three core templates

Every non-trivial project should produce three documents at the start, in order:

1. **PRD** (Product Requirements Document) — *Why* we're doing this. User stories, needs, pain points, intended outcomes.
2. **Spec** (Technical or Content Spec) — *What* we're producing. The ingredients of the deliverable, KPIs, milestones.
3. **Work Plan** — *How* we'll build it. Step-by-step implementation.

This sequence is universal — it applies to writing a blog post, building a piece of software, running a campaign, or producing a research report. The vocabulary changes; the structure doesn't.

## What's in this folder

```
templates/
├── README.md
├── prd-template.md
├── spec-template.md
├── workplan-template.md
└── claude-md-starter.md
```

The `claude-md-starter.md` is a starter `CLAUDE.md` for new projects — pre-populated with structure but mostly empty, since per Anthropic's guidance the best `CLAUDE.md` content is anti-patterns you discover during the project itself.

## Using these in a project

When `claude-init` bootstraps a new project, the relevant templates land in the project's `.claude/templates/` folder. Copy them up into the project root (or wherever you want them) and fill them in. Don't edit the master copies in place — the master copies are the templates everyone inherits.

## Customizing

Edit the templates as your standards evolve. If you find yourself adding the same section to every PRD, add it to the template. If a section is consistently empty, remove it. The templates should reflect the work you actually do.
