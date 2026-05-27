# Source Discipline

The rules that keep research defensible. Every claim Claude writes in `notes/` is either traceable to a source in `sources/index.md`, or tagged as inference/opinion/unverified. No exceptions.

## Anti-fabrication (hard rule)

**Never fabricate statistics, data, articles, people, places, URLs, or quotes.**

Use web search and web browsing tools to validate citations. The verification procedure depends on the citation type:

- **Statistics** — identify the source URL of the statistic. The URL must point to the page where the statistic actually appears, not a search result or a homepage.
- **Articles** — return the full APA citation (author, year, title, publication, URL). Test that the URL resolves and that the title on the page matches the citation. A "good URL" that loads a different article is still wrong.
- **Data / datasets** — return the dataset's source URL. If the data is behind a paywall or login, say so explicitly.
- **People** — return the person's social media profile URL, personal website, or Google Scholar citation when available. "A researcher at MIT" is not a citation; a verifiable name + affiliation + link is.
- **URLs** — test every URL. If it returns HTTP 4xx or 5xx, the citation is invalid and cannot be used. If your tools can't fetch the URL, mark the claim `[unverified]` — do not assume the URL works.

**If you cannot verify a citation, tag the claim `[unverified]` and surface it explicitly.** Do not silently fill the gap with a plausible-sounding placeholder. An honest "I couldn't verify this" beats a fabricated citation every time, and the Critic agent is specifically instructed to flag fabrications — getting caught is worse than admitting the miss.

## Source IDs

When `/intake` runs, every file in `inputs/` gets a stable ID: `S-01`, `S-02`, `S-03`, … recorded in `sources/index.md` with:

- `id` — `S-NN`
- `filename`
- `type` — csv / md / pdf / transcript / image / external-url
- `date` — date the source was created or published (not the date you ingested it)
- `owner` — who produced it, if known
- `status` — `current` / `superseded` / `estimate` / `draft` / `raw`
- `summary` — one sentence of what it contains
- `notes` — anything else (paywalled, partial, scraped on X date)

IDs never change once assigned, even if files are renamed or replaced. A superseded source stays in the index with `status: superseded` so older notes citing it remain interpretable.

## Citation format in `notes/`

Inline, square-bracketed, one citation per claim:

> Revenue grew 20% YoY in 2024. [S-03]

Multiple sources supporting one claim:

> Customer churn is rising across the segment. [S-02, S-05]

Inferences cite the sources they're reasoning from:

> The segment is consolidating around three vendors. [inference; S-01, S-02, S-04]

Single-source claims must be tagged so the Critic can target them:

> The market is worth $4.2B. [S-07; single-source]

Unverified claims get the loudest tag:

> Acme reportedly raised a Series C in March. [unverified; needs sourcing]

## When sources disagree

Don't average. Don't pick silently. Log the disagreement in `notes/open-threads.md`:

```
## Conflict: market size
- S-03 (Gartner, 2024): $4.2B
- S-07 (industry analyst blog, 2024): $6.1B
- Notes: S-03 uses narrower segment definition; S-07 includes adjacent categories.
- Resolution: use S-03's number in findings; flag the definition difference.
```

The resolution is recorded and visible. Future you (and the Critic) can audit it.

## Status taxonomy

- `current` — believed accurate as of the date in the source
- `superseded` — newer source replaces it (link the newer source ID in `notes`)
- `estimate` — explicitly an estimate, not measured data
- `draft` — preliminary, not finalized
- `raw` — raw data needing interpretation, not a finished claim

Sources tagged `superseded`, `estimate`, or `draft` require an explicit caveat when cited.

## What `/intake` does

- Walks `inputs/` and assigns IDs to any new files
- Never reassigns existing IDs
- Updates `sources/index.md` (idempotent — safe to re-run)
- Flags files it can't summarize (binary, too large, encrypted) so you can decide what to do
- Does **not** delete or modify anything in `inputs/`

## Things that are not sources

- Your own prior outputs (a draft in `notes/` is not a source for another claim in `notes/`)
- LLM-generated content from earlier in this project (or any project)
- Wikipedia, unless you've also opened the citation Wikipedia is pulling from
- "Common knowledge" — if it's worth claiming, it's worth citing

If a claim's only support is "the model knows this," it's an `[inference]` or `[unverified]`, not an observation.
