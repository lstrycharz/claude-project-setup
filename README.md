# claude-project-setup

A generic, non-code **Claude harness** for open-ended research, brainstorming, and analysis projects. One command (`claude-init`) scaffolds a project where Claude drafts material against a controlled source packet, and an **independent Critic sub-agent** attacks the drafts before you treat them as settled.

This is not a project-type starter kit, a template library, or a prompt collection. It's a small workflow harness with two roles (Thinker and Critic), three rule files, four skills, and a folder layout that makes source discipline the path of least resistance.

---

## Why this exists

If you brainstorm with Claude on real research — competitive analyses, business-idea exploration, market sizing, customer research — you've seen the failure mode: a polished-looking output where some claims are sourced, some are inferred, and some are fabricated, and you can't tell which is which. The Critic agent + source discipline solves that.

The harness rests on four claims, each defended by a specific mechanism:

1. **Drafts and critiques are different jobs and need different agents.** A model balanced between "produce something" and "attack what was produced" does both poorly. The `/critique` skill spawns a fresh sub-agent with no memory of how the draft was produced.
2. **Source discipline catches what the Critic can't.** Even an independent Critic shares training data with the Thinker. If both models hallucinate the same fact, the Critic won't flag it. The anti-fabrication rules in `source-discipline.md` (test every URL, verify every stat) catch shared-blind-spot failures.
3. **Structure beats fluency.** A free-form brainstorm hides assumptions inside flowing prose. The `/brainstorm` skill forces a five-section structure (observations, inferences, what's missing, ranked candidates, open questions) so the Critic can target precisely.
4. **The Critic must be uncontaminated.** Four contamination sources — conversational, prompt-framing, model-bias, task-framing — each get a specific defense. See `references/global/critic-prompt.md` for the full reasoning.

---

## What gets installed

Running `claude-init` in a new project folder produces this layout:

```
your-project/
├── CLAUDE.md                       ← project-root boot sector; Claude auto-loads this
├── inputs/                         ← you drop md / csv / pdf / notes / transcripts here
├── notes/                          ← Claude's drafts, brainstorms, critiques
│   ├── questions.md                ← what you're trying to answer
│   ├── findings.md                 ← living best-answer document
│   └── open-threads.md             ← parked conflicts and unresolved items
├── sources/
│   └── index.md                    ← inventory of inputs/, maintained by /intake
└── .claude/
    ├── settings.json               ← Thinker and Critic model config
    ├── references/global/
    │   ├── thinking-rules.md       ← how to brainstorm and draft
    │   ├── source-discipline.md    ← citation rules + anti-fabrication
    │   └── critic-prompt.md        ← the verbatim prompt the Critic runs
    └── skills/
        ├── intake/                 ← /intake — inventory inputs/
        ├── brainstorm/             ← /brainstorm <question> — structured brainstorm
        ├── critique/               ← /critique <file> — independent hostile review
        └── synthesize/             ← /synthesize — fold critique back into draft
```

---

## The workflow

```
You: drop source materials into inputs/
You: /intake                              → sources/index.md generated
You: /brainstorm "what are the top 3 risks for this ecomm idea?"
Thinker: writes notes/risks.md with cited claims, inferences, and open questions
You: /critique notes/risks.md             → spawns fresh Critic sub-agent (different model)
Critic: returns a numbered list of issues — unsourced claims, fabricated citations,
         reasoning gaps, missing perspectives, contradictions with sources
You: /synthesize                          → Thinker folds findings back in, parks unresolvables
You: read the revised draft and decide what's worth pushing further
```

Every step is idempotent. Re-running `/intake` doesn't reassign IDs. Re-running `/critique` produces another critique file alongside the first. `/synthesize` appends a changelog so the audit trail survives.

---

## The four skills

| Skill | What it does |
|---|---|
| `/intake` | Walks `inputs/`, assigns stable IDs (`S-01`, `S-02`, …), records type / date / owner / status / one-sentence summary into `sources/index.md`. Idempotent. |
| `/brainstorm <question>` | Reads the sources, produces a structured five-section answer in `notes/<slug>.md`. Every claim tagged `[observation]` / `[inference]` / `[opinion]` / `[unverified]`. |
| `/critique <file>` | Spawns a **fresh sub-agent** with **no conversation history**, ideally on a **different model** than the Thinker, with **only** the original question + the draft + the source index. Returns an enumeration of issues — no fixes, no balanced feedback. Saved to `notes/critique-*.md`. |
| `/synthesize` | Reads the latest critique. Each issue is either fixed in the draft, parked to `open-threads.md`, or pushed back with explicit reasoning. Writes a changelog. |

---

## Critic independence — why the harness is shaped this way

A Critic that's been contaminated by the Thinker is worse than no Critic — it gives you false confidence. The harness defends against four contamination sources:

1. **Conversational contamination** — the Critic runs in a **fresh sub-agent**, not as "now switch to critic mode" in the same thread. No prior reasoning to anchor on.
2. **Prompt-framing contamination** — the Critic forms its own view of what a good answer needs *before* reading the draft. This catches scope and framing errors a draft-anchored review misses.
3. **Model-bias contamination** — Thinker and Critic run on **different models** (configured in `.claude/settings.json`). Same-model self-review shares blind spots.
4. **Task-framing contamination** — the Critic prompt explicitly forbids strengths, fixes, and softening. "Review" is trained to mean "balanced feedback"; this prompt strips that out.

The full reasoning lives in `references/global/critic-prompt.md`.

---

## Anti-fabrication

The single most important rule: **never fabricate statistics, data, articles, people, places, URLs, or quotes.** The Thinker uses web tools to verify; the Critic flags anything it can't verify.

Verification procedures (from `source-discipline.md`):

- **Statistics** — identify the source URL where the statistic actually appears.
- **Articles** — full APA citation; test the URL resolves and the title matches.
- **Data** — return the dataset source URL.
- **People** — social media profile, personal website, or Google Scholar.
- **URLs** — test every URL. HTTP 4xx/5xx invalidates the citation.

If a citation can't be verified, the claim is tagged `[unverified]` — not silently dropped or replaced with a plausible-sounding placeholder.

---

## Install

See [INSTALL.md](INSTALL.md). Short version:

```bash
git clone https://github.com/lstrycharz/claude-project-setup.git ~/claude-project-setup
echo 'export PATH="$HOME/claude-project-setup/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

Then in any project folder:

```bash
claude-init               # scaffold the harness
claude-init --dry-run     # preview what would be created
claude-init --update      # re-sync rules and skills after the master kit changes
```

No external dependencies (no `yq`, no `jq`). Pure bash 3.2+.

---

## Customizing

The harness ships opinionated defaults. Override them by editing files in your project's `.claude/` after init:

- **Different rules for a specific project** — edit `.claude/references/global/*.md` in place. Your project, your rules.
- **Tune the Critic prompt** — edit `.claude/references/global/critic-prompt.md`. The `/critique` skill reads it verbatim, so changes take effect immediately.
- **Different models** — edit `.claude/settings.json`. Thinker and Critic must be different.

When you've improved a rule and want every future project to inherit the change, push it back to the master kit (`~/claude-project-setup/references/global/`) and run `claude-init --update` in your existing projects.

---

## What this kit is not

- **Not a code harness.** For software projects with hooks, secret scanning, and PROGRESS.md, use a code-oriented kit instead.
- **Not a project-type starter library.** No PRD/Spec/Workplan templates, no project-type selector. One shape works for any research topic.
- **Not a prompt collection.** The skills are workflow primitives, not prompt snippets.
- **Not push-button.** Knowledge work is contingent on domain knowledge; the harness handles the workflow scaffolding, not the substance of what you're researching.

---

## License

MIT. See [LICENSE](LICENSE).
