# references/

Long-form rules files and reference documentation, organized by domain. These are the documents Claude reads at the start of a project to learn your standards — first principles, hard constraints, anti-patterns, design patterns, conventions to follow.

## Structure

A reasonable layout, with one subfolder per domain:

```
references/
├── global/
│   └── general-rules.md          # Rules that apply to every project
├── blog-content/
│   ├── seo-rules.md
│   ├── forbidden-words.md
│   ├── structure-rules.md
│   └── blog-checklist.md
├── data-analysis/
│   ├── analysis-rules.md
│   ├── visualization-rules.md
│   └── analysis-checklist.md
└── research/
    └── research-rules.md
```

You don't have to use these exact subfolders or filenames — they're examples. Match what your team actually produces.

## How to build a great reference file

A practical method that consistently produces useful files:

1. **Pick a domain you do real work in** (e.g., "monthly client PPC reports" or "evergreen blog posts").
2. **Run a research prompt in a deep-research-capable AI tool** (Gemini, Perplexity, or similar). Ask for: first principles, hard constraints, anti-patterns, design patterns, common mistakes, hidden gotchas, and validation criteria for that specific domain.
3. **Run the same prompt in a second tool**, then a third. Three independent reports surface what's consensus (likely correct), what's model-specific (worth questioning), and what's unique to one source (worth investigating before trusting).
4. **Merge the three reports into a single rules file.** Have Claude do the merge — instruct it to keep specifics, remove redundancy, and resolve contradictions in favor of the most-cited claim.
5. **Pair every rules file with a checklist file.** The rules file is reference material Claude reads at the start of a project; the checklist is what Claude actively runs against output before declaring the work done. The checklist is where the rules get enforced in practice.

This whole sequence takes 2–4 hours per domain done well. It's an investment, but the resulting file lives for years and improves the quality of every project it touches.

## What "good" looks like

A useful reference file has a few specific characteristics:

- **Specific, not aspirational.** "Write engaging content" is aspirational and useless. "Open every section with a stat or specific number, never a question or scenario" is specific and actionable.
- **Causally explained.** Rules name the consequence — "do X, because if you don't, Y happens."
- **Opinionated.** It makes calls where experts disagree, and shows its work.
- **Names anti-patterns by their failure mode.** Not "avoid generic content" but "don't open with a paragraph that summarizes the whole article — readers bounce because the payoff is upfront."
- **Respects domain vocabulary.** A finance file should use the right finance terms; a marketing file should use the right marketing terms.
- **Has graduation criteria.** How do you know when a rule has been followed well vs. poorly?

A good test for any line in a reference file: would Claude produce meaningfully different output if this line were removed? If no, delete it. The file should be lean and load-bearing.

## Maintenance

When you notice Claude making the same mistake twice on real projects, update the relevant reference file. Don't let lessons stay siloed inside individual projects' `CLAUDE.md` files forever — periodically distill them back into the master references here. That's how the kit gets sharper over time.
