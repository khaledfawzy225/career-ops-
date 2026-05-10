# Shared Configuration

All scan/apply/track modes inherit these defaults. Override per-mode as needed.

## Target persona
Software / AI / ML engineer — 5+ years experience — open to remote-first or
hybrid roles in North America or fully remote globally.

## Preferred titles
- Software Engineer (L4/L5/L6 equivalent)
- Senior Software Engineer
- Staff Engineer
- Principal Engineer
- Backend Engineer
- Full-Stack Engineer
- Platform Engineer
- Infrastructure Engineer
- Machine Learning Engineer
- ML Engineer
- AI Engineer
- Data Engineer
- Site Reliability Engineer (SRE)
- Engineering Manager (IC-track preferred)

## Locations
- Remote (worldwide)
- Remote (US)
- San Francisco Bay Area, CA
- New York, NY
- Seattle, WA
- Austin, TX

## Compensation floor
USD 150,000 / year base (or equivalent for non-US).

## title_filter
Rules applied in order. A result must match at least one **include** pattern
and must not match any **exclude** pattern (all regex, case-insensitive).

### include
```
software\s+engineer
senior\s+engineer
staff\s+engineer
principal\s+engineer
backend\s+engineer
full.?stack\s+engineer
platform\s+engineer
infrastructure\s+engineer
machine\s+learning\s+engineer
\bml\s+engineer\b
\bai\s+engineer\b
data\s+engineer
site\s+reliability
\bsre\b
engineering\s+manager
```

### exclude
```
\bintern(ship)?\b
\bjunior\b
entry.?level
\bstudent\b
associate\s+engineer
sales\s+engineer
solutions\s+engineer
security\s+engineer
qa\s+engineer
test\s+engineer
embedded\s+engineer
hardware\s+engineer
```

## Standard offer record format (pipeline.md)
Each new offer is appended as a Markdown table row:

| Date found | Title | Company | Location | URL | Source | Notes |
|---|---|---|---|---|---|---|
| YYYY-MM-DD | … | … | … | … | portal-id | — |

## scan-history.tsv columns
```
url\tdate_found\ttitle\tcompany
```
One row per offer URL ever seen; used for exact-URL deduplication.
