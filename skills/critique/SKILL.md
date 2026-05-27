---
name: critique
description: Spawn a fresh sub-agent in hostile-reviewer mode to attack a draft file. Critic runs with no conversation history, ideally on a different model than the Thinker, and produces an enumeration of problems — no fixes, no balanced feedback. Use when the user runs /critique <file> or asks to challenge, attack, stress-test, or independently review a draft.
---

# /critique — hostile review by an independent sub-agent

Pass a draft to a fresh Critic agent that has no memory of how the draft was produced. Return its issue list verbatim.

## When to use

- The user runs `/critique <file>`
- The user says "attack this", "stress-test this", "challenge this", "what's wrong with this", "what am I missing"
- Before a draft is treated as settled, especially before sharing it externally

## Independence is the point — read this carefully

The Critic must be **uncontaminated** by the Thinker's reasoning. Four contamination sources, four defenses:

1. **Conversational contamination** — the Critic runs as a **fresh sub-agent** with no conversation history. Spawn via the Agent tool. Do not "switch into critic mode" in the current thread.
2. **Prompt-framing contamination** — the Critic forms its own view of what a good answer needs *before* reading the draft. The prompt in `references/global/critic-prompt.md` enforces this.
3. **Model-bias contamination** — the Critic should run on a **different model** than the Thinker. Read `.claude/settings.json` for `critic_model`; use that. If unset, ask the user which model to use, or default to a different tier (e.g., if Thinker is Sonnet, Critic is Opus, or vice versa).
4. **Task-framing contamination** — the prompt explicitly forbids strengths, fixes, and softening. Don't relax that.

## What to do

1. **Identify the target file.** From the user's invocation: `/critique notes/risks.md` → target is `notes/risks.md`. If unclear, ask.
2. **Identify the original question.** Find it in `notes/questions.md` or ask the user verbatim. The Critic needs it independently of the draft.
3. **Read `references/global/critic-prompt.md`.** This is the verbatim prompt the Critic receives. Do not paraphrase it; pass it as-is.
4. **Read `.claude/settings.json`** for `critic_model`. If unset, surface this to the user before proceeding — running Critic and Thinker on the same model defeats half the point.
5. **Spawn a sub-agent** (Agent tool, `subagent_type: general-purpose` or `claude` with the configured model). The sub-agent's prompt contains:
   - The verbatim text of `references/global/critic-prompt.md`
   - The **original question** (verbatim)
   - The **draft** (verbatim contents of the target file)
   - The **source index** (verbatim contents of `sources/index.md`)
   - **Nothing else.** No brainstorm transcript. No working notes. No prior thinking.
6. **Return the sub-agent's output verbatim** to the user. Do not summarize, soften, or filter it. The user reads the raw critique.
7. **Save the critique** to `notes/critique-<target-filename>-<timestamp>.md` so it's auditable and so `/synthesize` can find it.

## Hard rules

- **Never run the Critic in the current thread.** Always spawn a sub-agent.
- **Never pass the brainstorm transcript or working notes to the Critic.** The Critic sees the question, the draft, and the source index. Period.
- **Never edit or soften the Critic's output before showing the user.** Raw is the deliverable.
- **Surface model overlap.** If Thinker and Critic ended up on the same model (config not set, or set to the same model on both sides), warn the user — shared training data means shared blind spots.

## When you finish

Tell the user:
- Where the critique was saved
- How many issues the Critic found, by category (just the counts — let the user read the details)
- Suggest running `/synthesize` next to fold the findings into the draft
