---
name: synthesize
description: Read the latest critique output and update the draft accordingly — revise where the critique is accepted, move unresolved disputes to open-threads.md, leave a changelog. Use when the user runs /synthesize, or after /critique completes and the user wants to fold findings back in.
---

# /synthesize — fold critique findings back into the draft

Walk the Critic's issue list and update the draft. Some issues get fixed; some get parked; all get accounted for.

## When to use

- The user runs `/synthesize`
- A critique file exists in `notes/` and the user wants to act on it
- The user says "fold in the critique", "apply the feedback", "fix what the critic found"

## What to do

1. **Find the most recent critique file** in `notes/critique-*.md`. If multiple exist, ask the user which to use (default: most recent).
2. **Identify the target draft** the critique was about (the filename appears in the critique filename).
3. **Read both files in full.** Plus `sources/index.md` — you may need to re-cite as you revise.
4. **For each issue in the critique**, do one of three things:

   - **Accept and fix** — revise the draft to address the issue. Cite a source if you're adding evidence; tag `[inference]` or `[unverified]` if you can't.
   - **Park as unresolved** — move the disputed point to `notes/open-threads.md` with a reference to the critique and why it can't be resolved here (missing source, requires user judgment, etc.).
   - **Push back, with reasoning** — if the critique is wrong, leave the draft unchanged and add an entry to the changelog explaining why. Pushing back requires explicit reasoning, not just disagreement. Be honest with yourself: critics are usually right, especially independent ones.

5. **Write a changelog** at the bottom of the revised draft:

```markdown
## Changelog — synthesize run YYYY-MM-DD HH:MM

Critique: notes/critique-<filename>-<timestamp>.md

| # | Issue (short) | Action | Notes |
|---|---------------|--------|-------|
| 1 | Unsourced claim about market share | Fixed — added [S-03] | |
| 2 | Reasoning gap in section 3 | Fixed — added intermediate step | |
| 3 | Disputed: critic says X, draft says Y | Parked → open-threads.md | needs user call |
| 4 | Critic flagged single-source on segment data | Tagged [single-source] | |
| 5 | "Missing perspective: regulatory" | Pushed back — out of scope per question framing | |
```

6. **Update `notes/open-threads.md`** with any items that got parked.

## Hard rules

- **Account for every issue.** Every numbered item in the critique gets a row in the changelog. Skipping items is how findings get lost.
- **Pushing back requires reasoning.** "I disagree" is not a synthesize action. Either fix it, park it, or write the argument for why the critic is wrong.
- **Re-cite as you revise.** New claims need new citations. Anti-fabrication applies during synthesis just as much as during brainstorming.
- **Preserve the draft history.** Keep the original file's structure; revise in place but leave the changelog visible at the bottom.
- **Don't re-run the critic.** That's a separate `/critique` invocation. Synthesize takes one critique and produces one revised draft.

## When you finish

Tell the user:
- How many issues were accepted, parked, or pushed back
- Where the revised draft is (same path as before)
- Where the changelog is (bottom of the draft)
- Whether `notes/open-threads.md` was updated
- Suggest running `/critique` again on the revised draft if the changes were substantial
