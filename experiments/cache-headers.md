# Cache headers: do vendors follow `Cache-Control` and similar headers?

The `/cacheHeaders/` pages on origin A send caching headers. Those headers tell a fetcher how long
it may reuse a saved copy. We ask about each page, then ask again after growing gaps: 2.5, 5, 10,
20, 40 and 80 minutes. Each answer is graded "downloaded again" or "reused a copy", and checked
against what the headers allow.

| Run | Run id | Date (2026) | Question wording | Printed report |
|---|---|---|---|---|
| Day 1: 19 header settings, all through OpenRouter | `run20261007-144023-gu7nd` | 7 Oct | old | `ttlmap-ccdepth-scout-1007.log` |
| Day 2 | `run20261015-060022-firmp` | 15 Oct | old | `ttlmap-ccdepth-day2-1015.log` |
| Day 3 | `run20261017-190024-oprn4` | 17 Oct | old | `ttlmap-ccdepth-day3-1017.log` |
| `no-store` A: Anthropic's default fetch tool | `run20261018-151536-p2w7b` | 18 Oct | old | `ttlmap-nostore-A-1018.log` |
| `no-store` A: Anthropic's basic fetch tool | `run20261018-163712-5dojv` | 18 Oct | old | `ttlmap-nostore-A-basic-1018.log` |
| `no-store` B | `run20261019-070008-y8ku6` | 19 Oct | old | `ttlmap-nostore-B-1019.log` |
| `no-store` through OpenRouter | `run20261019-114042-xnmr6` | 19 Oct | old | `ttlmap-nostore-OR-1019.log` |
| `no-store` C | `run20261021-200009-l5iw8` | 21 Oct | old | `ttlmap-nostore-C-1021.log` |
| Re-check, old wording | `run20261107-171631-riww3` | 7 Nov | old | `ttlmap-nostore-Aold-1107.log` |
| Re-check, new wording | `run20261107-183703-hgztj` | 7 Nov | new | `ttlmap-nostore-Anew-1107.log` |
| Long re-check: one `no-store` page every 45 min for about 25 hours | `run20261107-195737-ezwzu` | 7–8 Nov | new | `ttlmap-nostore-B-1107.log` |

`no-store` is the header that forbids reusing a copy at all. The `no-store` runs and the re-checks
ask Anthropic only.

## Files

| File | What it holds |
|---|---|
| `logs/ttlmap-*.log` | Each run's printed report. The paper's two cache tables (each vendor against each header setting, days 1–3; and the `no-store` runs) were made by hand from these |
| `logs/results/ttlmap-<run id>.jsonl` | Every call |
| `logs/raw-replies.jsonl`, lines for the two 7 Nov new-wording runs | Whole replies. They hold Anthropic's own `retrieved_at` time for each copy it used |
| `logs/probe.jsonl`, lines on `/cacheHeaders/` | Every vendor download |

The 7–8 Nov re-checks are not in the paper.
