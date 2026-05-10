# Scan Mode

## Purpose
Discover new job offers by querying enabled portals and company career pages,
filter by `title_filter`, deduplicate against `data/scan-history.tsv`, and
append net-new matches to `data/pipeline.md`.

## Inputs
- `portals.yml` — portal definitions and search queries
- `modes/_shared.md` — title_filter patterns and offer format
- `data/scan-history.tsv` — previously seen offer URLs (dedup set)
- `data/pipeline.md` — running list of tracked offers

## Steps

### 1. Load configuration
Read `portals.yml`. Collect:
- All portals where `enabled: true` → run their `query` via WebSearch.
- All entries under `company_pages` where `enabled: true` → fetch the URL
  directly and parse visible job listings.

### 2. Search each enabled portal
For each portal:
- Execute the portal's `query` string as a web search.
- Extract every distinct job posting: title, company, location, URL, post date.
- If post date is unavailable, record today's date.

### 3. Apply title_filter
Keep a result only if:
- Its title matches at least one `include` pattern (from `_shared.md`), AND
- Its title does NOT match any `exclude` pattern.

### 4. Deduplicate
Load `data/scan-history.tsv`. For each filtered result:
- If the offer URL already appears in column 1, discard it.
- Otherwise, mark it as new.

### 5. Append new offers
For each new offer (sorted by company name):
- Append a row to `data/pipeline.md` following the standard format in `_shared.md`.
- Append a row to `data/scan-history.tsv`: `url\tdate_found\ttitle\tcompany`.

### 6. Report
Print a summary: how many portals queried, raw results found, title-filtered,
deduplicated, and net-new offers appended.

### 7. Commit
Stage `data/pipeline.md` and `data/scan-history.tsv` and create a git commit:
`scan: add N new offers (YYYY-MM-DD)`.

## Notes
- Do not modify any existing rows in `pipeline.md`.
- Preserve existing rows in `scan-history.tsv`.
- If zero new offers are found, still commit (with a 0-offer message) to log
  the run date.
