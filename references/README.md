# references/

Long-form rules files and reference documentation, organized by domain. These are the deep-research outputs Chris describes in the Trust Insights episode — first principles, hard constraints, anti-patterns, design patterns, hidden gotchas — distilled into instructions Claude can read at the start of a project.

## Structure

```
references/
├── global/
│   └── general-rules.md        # Rules that apply to every project
├── blog-content/
│   ├── seo-rules.md
│   ├── forbidden-words.md
│   ├── structure-rules.md
│   └── blog-checklist.md
├── data-analysis/
│   ├── analysis-rules.md
│   ├── visualization-rules.md
│   └── analysis-checklist.md
├── research/
│   └── research-rules.md
└── code/
    └── general-coding-rules.md
```

## How to build a great reference file

The Trust Insights method:

1. Pick a domain you do work in (e.g., "writing evergreen blog posts").
2. Run a deep research prompt on it in three different tools (Gemini Deep Research, Perplexity Deep Research, Alibaba Qwen). Trust Insights' Casino prompt framework is one option: trustinsights.ai/casino.
3. Each report should cover: first principles, hard constraints, anti-patterns, design patterns, common mistakes, hidden gotchas, validation criteria.
4. Merge the three reports into a single rules file. Have Claude do the merge — instruct it to keep specifics, remove redundancy, resolve contradictions in favor of the most-cited claim.
5. Pair every rules file with a checklist file. The rules file is reference material; the checklist is what gets actively run against output before declaring work done.

## What "good" looks like

A reference file should be specific enough that a smart contractor reading it could produce work that matches your standards without asking questions. If it's vague enough that the model can interpret it any number of ways, it's not done.

## Maintenance

When you notice the model making the same mistake twice in real projects, update the relevant reference file. Don't let lessons stay siloed inside individual projects' `CLAUDE.md` files forever — periodically distill them back into the master references.
