---
name: brainstorm
description: Structured brainstorm against the source packet. Forces explicit separation of what the sources say, what's inferred, what's missing, and ranks candidate answers by confidence. Use when the user runs /brainstorm <question>, or asks an open-ended research question that should be answered from the project's sources.
---

# /brainstorm — structured brainstorm

Open-ended research and synthesis, run with structure that the Critic can target.

## When to use

- The user runs `/brainstorm <question>`
- The user asks an open-ended research or analytical question and the project has sources in `inputs/`
- The user says "think through this", "what do we know about", "draft an answer to"

## Before you start

- Confirm `sources/index.md` exists. If not, run `/intake` first.
- Read every source listed in the index. Yes, every one. If a source is too large, sample it but say so.
- Hold the rules in `references/global/thinking-rules.md` and `references/global/source-discipline.md` in mind — they govern this output.

## What to produce

Write to `notes/<question-slug>.md`. The file has five sections, in order, and they are not optional:

### 1. What the sources say

Direct observations from the source packet. Every claim has a source ID and the `[observation]` tag.

```
- Acme has 35% market share in 2024. [observation; S-03]
- Customer interviews cite price as the top buying factor. [observation; S-02, S-05]
```

### 2. What I infer from them

Your reasoning over the observations. Each inference cites the sources it's reasoning from and is tagged `[inference]`.

```
- The segment is consolidating around three vendors. [inference; S-01, S-03, S-04]
```

### 3. What's missing from the sources

The single most important section. What can't be answered with this packet?

```
- No data on customer LTV in the mid-market segment.
- All pricing data is list price; actual transaction prices not represented.
- One competitor (Vendor X) is absent from S-01 entirely.
```

### 4. Candidate answers, ranked by confidence

Order by confidence, not by the order they occurred to you. Each candidate states the answer, the supporting evidence, and what would change your confidence.

```
1. **Most likely answer:** [answer]
   - Support: [citations]
   - Would change my view: [what evidence would lower confidence]

2. **Plausible alternative:** [answer]
   - Support: [citations]
   - Would change my view: [...]
```

### 5. Open questions to push next

Specific, actionable next-step questions — not general "we should research more."

```
- What's the LTV gap between segments? Needs a finance source we don't have.
- Is Vendor X's absence from S-01 because they're below the threshold or because they were missed?
```

## Hard rules

- **Every claim is tagged.** `[observation]`, `[inference]`, `[opinion]`, or `[unverified]`. Untagged claims are a bug.
- **One claim per sentence.** Compound sentences hide which half is unsupported.
- **No averaging conflicting sources.** Log conflicts in `notes/open-threads.md`.
- **Anti-fabrication applies.** Per `source-discipline.md`, don't invent stats, people, URLs, or quotes. Mark `[unverified]` if you can't confirm.
- **The "Not in the sources" section is mandatory.** A brainstorm without it is overclaiming by omission.

## When you finish

Tell the user:
- Where the brainstorm landed (`notes/<slug>.md`)
- The top open questions
- Suggest running `/critique notes/<slug>.md` before treating the result as settled
