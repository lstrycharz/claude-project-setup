---
name: intake
description: Walk the project's inputs/ folder and produce or refresh sources/index.md with stable IDs, type, date, owner, status, and a one-sentence summary per source. Use when the user runs /intake, drops new files into inputs/, or asks to inventory sources.
---

# /intake — source inventory

Build or refresh the source index for this project.

## When to use

- The user runs `/intake`
- New files have appeared in `inputs/`
- The user says "inventory the sources", "what do we have", "build the index"
- You're about to brainstorm or critique and `sources/index.md` is missing or stale

## What to do

1. **Read `sources/index.md`** if it exists. Note every ID already assigned.
2. **List `inputs/` recursively.** For each file:
   - If it already has an ID in the index, skip (do not reassign).
   - If it's new, assign the next sequential ID (`S-NN` zero-padded).
3. **For each new file**, gather:
   - `id` — next sequential
   - `filename` — relative path from `inputs/`
   - `type` — csv / md / pdf / docx / txt / transcript / image / external-url / other
   - `date` — date the source was created or published (from filename, file content, or file mtime as last resort — note which)
   - `owner` — who produced it, if discoverable from the content
   - `status` — `current` / `superseded` / `estimate` / `draft` / `raw`. Default to `raw` if unclear and flag for the user.
   - `summary` — one sentence of what the file contains. Read the file to write this; do not guess from the filename.
   - `notes` — anything else worth flagging (paywalled, partial, scraped on X date, encoding issues)
4. **For files you cannot process** (binary you can't read, encrypted, too large), add them to the index with `status: raw` and `notes: unprocessed — [reason]`. Surface this list to the user at the end.
5. **Write `sources/index.md`** in the format below. **Never modify or delete entries for IDs that already exist** — IDs are stable.

## Output format for `sources/index.md`

```markdown
# Sources Index

Updated: YYYY-MM-DD

| ID | Filename | Type | Date | Owner | Status | Summary |
|----|----------|------|------|-------|--------|---------|
| S-01 | competitors.csv | csv | 2025-03-10 | analyst team | current | Competitor pricing scrape across 12 brands. |
| S-02 | interview-jane.md | transcript | 2025-04-02 | self | current | Customer interview, mid-market segment. |
| S-03 | market-report-2024.pdf | pdf | 2024-11 | Gartner | current | Market sizing report, paywalled summary version. |

## Notes

- S-03 is the paid-summary version; full report not accessible.
- S-04 was superseded by S-09 on 2025-04-15.
```

## Hard rules

- **IDs are stable.** Never reassign an ID. If a file is replaced, mark the old ID `superseded` and assign a new ID to the replacement.
- **Never modify or delete files in `inputs/`.**
- **Read the file before summarizing.** A summary derived from the filename alone is a fabrication.
- **If you can't summarize confidently, say so** — `status: raw`, `notes: unprocessed`. Do not invent a summary.
- **Idempotent.** Running `/intake` twice in a row produces the same `sources/index.md`.

## When you finish

Report to the user:
- How many sources are now indexed
- How many were newly added this run
- Anything you flagged for attention (unprocessed files, status defaults you guessed, etc.)
