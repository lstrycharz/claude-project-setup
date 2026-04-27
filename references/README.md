# references/

Long-form rules files and reference documentation, organized by domain. These are the documents Claude reads at the start of a project to learn your team's standards — first principles, hard constraints, conventions to follow, things to avoid.

## Structure

The convention is one subfolder per project type, plus a `global/` folder for rules that apply everywhere:

```
references/
├── global/
│   └── general-rules.md          # Rules that apply to every project
├── <project-type-1>/
│   ├── <project-type-1>-rules.md      # Long-form rules document
│   └── <project-type-1>-checklist.md  # Validation checklist
├── <project-type-2>/
│   └── ...
└── <project-type-3>/
    └── ...
```

Subfolder names should match the project types defined in `manifest.yaml`. The kit ships with starter project types you can rename or replace to fit your team's work.

## How to build a useful reference file

A reference file is essentially a written-down version of "what good looks like" for a kind of work. The aim is that any team member — or Claude — could read it and produce work that matches your team's expectations without having to ask questions.

A practical method:

1. **Pick one kind of work your team does regularly.** Examples: a recurring report, a particular type of document, an analysis pattern, a creative deliverable.

2. **List what makes that kind of work good vs. bad.** What's required every time? What's never acceptable? What patterns work? What patterns fail? What conventions does your team follow that newcomers don't know?

3. **Optional — for higher-stakes domains, run external research.** Use a deep-research tool (Gemini, Perplexity, or similar) to ask for first principles, hard constraints, anti-patterns, and common mistakes for that domain. Repeating the prompt across two or three different tools surfaces what's consensus vs. what's model-specific. Merging the reports into a single rules file produces something more authoritative than any individual model would generate alone.

4. **Pair every rules file with a checklist file.** The rules file is reference material Claude reads at the start of a project. The checklist is what Claude actively runs against output before declaring the work done. The checklist is where the rules get enforced in practice — without it, rules tend to be applied inconsistently across long projects.

A rules file usually takes 1–3 hours to produce well. The first version doesn't have to be perfect; it gets sharper as you use it on real projects and notice what's missing.

## What "good" looks like in a reference file

A useful reference file has a few specific characteristics:

- **Specific, not aspirational.** "Communicate clearly" is aspirational and doesn't change anyone's behavior. "Open every section with a takeaway, not a setup" is specific and actionable.
- **Causally explained.** Rules name the consequence — "do X, because if you don't, Y happens." This helps Claude (and team members) make good judgment calls when the rule doesn't perfectly cover their situation.
- **Opinionated.** It makes calls where reasonable people might disagree, and shows its work.
- **Names anti-patterns by their failure mode.** Not "avoid weak openings" but "don't open with a definition of the topic — readers either already know what it is or get bored before the payoff."
- **Respects domain vocabulary.** A finance file should use the right finance terms; an HR file should use the right HR terms. Don't substitute generic terms for domain-specific ones.
- **Has graduation criteria.** How do you know when the rule has been followed well vs. poorly? If you can't tell, the rule is probably too vague.

A good test for any line in a reference file: would Claude (or a junior team member) produce meaningfully different output if this line were removed? If no, delete it. The file should be lean and load-bearing — every line should be doing real work.

## How long should a rules file be?

Aim for 1,500–3,000 words. Long enough to be comprehensive, short enough that loading it into Claude's context doesn't crowd out the actual project content. If a domain genuinely needs more, split into two files (e.g., one for rules, one for glossary or terminology). The validation checklist is always a separate file from the rules — different purpose, different format.

## Maintenance

When you notice Claude (or a teammate) making the same mistake twice across real projects, update the relevant reference file. Don't let lessons stay siloed inside individual projects' `CLAUDE.md` files forever — periodically distill them back into the master references here. That's how the kit gets sharper over time.

If multiple people on your team contribute, the reference files become a record of collective experience — captured once, available to everyone, automatically loaded into every relevant project.
