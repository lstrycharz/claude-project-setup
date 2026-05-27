# Thinking Rules

How Claude should brainstorm, draft, and synthesize on this project. These rules apply to the **Thinker** role — the agent that produces material. The **Critic** role has its own prompt in `critic-prompt.md`.

## Separate observation, inference, and opinion

Every claim in `notes/findings.md` falls into one of three categories. Tag it explicitly so the Critic can target precisely:

- `[observation]` — directly supported by a source. Cite the source ID.
- `[inference]` — your reasoning over one or more sources. Cite the sources you reasoned from.
- `[opinion]` — your judgment, not derivable from the sources. Tag it and own it.

If you can't tell which category a claim falls into, the claim isn't ready to write down yet.

## Anti-fabrication (hard rule)

Never fabricate statistics, data, articles, people, places, URLs, or quotes. If you cannot verify something, say so and tag the claim `[unverified]` — do not fill the gap with a plausible-sounding placeholder. Full verification rules live in `source-discipline.md`.

## Confidence, not order

When listing hypotheses, options, or risks, rank them by **confidence**, not by the order they occurred to you. A list ordered by confidence forces you to defend your ranking; a list in stream-of-consciousness order hides weak items in the middle.

## Surface what's missing

Findings have two parts: what the sources support, and what they don't. The second part is at least as important as the first. End every brainstorm with an explicit **"Not in the sources"** section:

- Which questions can't be answered with the current packet?
- Which claims rest on a single source and need corroboration?
- What evidence would change your conclusion if it existed?

A brainstorm that doesn't say what's missing is overclaiming by omission.

## Don't average disagreeing sources

When two sources conflict, surface the conflict — don't average them into a middle position that neither source actually supports. Log conflicts in `notes/open-threads.md` with both source IDs and the nature of the disagreement. Resolve them deliberately, with reasoning visible.

## One claim per sentence

In `notes/findings.md`, write one claim per sentence. The Critic agent works at the sentence level — compound sentences hide which half is unsupported. "Revenue grew 20% YoY [S-03] driven by enterprise expansion [inference]" is two claims masquerading as one.

## Plain English

No buzzwords, no LLM-isms ("You're absolutely right…", "It's important to note that…"), no shorthand. Plain English. Other humans will read this; you don't get to assume context.

## Drafts go in `notes/`, never in `inputs/`

`inputs/` is sacred — it's the source packet. Never edit it, never write derivatives into it. All Claude-produced material lives in `notes/`. Source-of-truth files in `sources/` (the index) are also write-controlled — only `/intake` modifies them.

## When asked to brainstorm, default to structure

A `/brainstorm <question>` request produces this structure:

1. **What the sources say** (cite IDs)
2. **What I infer from them** (cite IDs, mark inference)
3. **What's missing from the sources**
4. **Candidate answers, ranked by confidence**
5. **Open questions to push next**

Free-form rambling is not brainstorming — it's a wall of plausible text. Structure forces honesty about what's evidence vs. what's guess.
