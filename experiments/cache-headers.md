# Cache headers: does a vendor follow `Cache-Control` and similar headers?

All on origin A, on `/cacheHeaders/` pages (the only pages that send caching headers). Each page is
asked about, then asked again after growing gaps (2.5, 5, 10, 20, 40, 80 min). Each answer is
graded as "downloaded again" or "reused a copy", against what the headers allow.

| Run | Run id | Date (2026) | Question wording | Run report |
|---|---|---|---|---|
| Day 1 (19 settings, all through OpenRouter) | `run20261007-144023-gu7nd` | 7 Oct | old | `ttlmap-ccdepth-scout-1007.log` |
| Day 2 | `run20261015-060022-firmp` | 15 Oct | old | `ttlmap-ccdepth-day2-1015.log` |
| Day 3 | `run20261017-190024-oprn4` | 17 Oct | old | `ttlmap-ccdepth-day3-1017.log` |
| `no-store` A (default tool) | `run20261018-151536-p2w7b` | 18 Oct | old | `ttlmap-nostore-A-1018.log` |
| `no-store` A, basic tool | `run20261018-163712-5dojv` | 18 Oct | old | `ttlmap-nostore-A-basic-1018.log` |
| `no-store` B | `run20261019-070008-y8ku6` | 19 Oct | old | `ttlmap-nostore-B-1019.log` |
| `no-store` through OpenRouter | `run20261019-114042-xnmr6` | 19 Oct | old | `ttlmap-nostore-OR-1019.log` |
| `no-store` C | `run20261021-200009-l5iw8` | 21 Oct | old | `ttlmap-nostore-C-1021.log` |
| Re-check, A-old (18 Oct program) | `run20261107-171631-riww3` | 7 Nov | old | `ttlmap-nostore-Aold-1107.log` |
| Re-check, A-new | `run20261107-183703-hgztj` | 7 Nov | new (address + question) | `ttlmap-nostore-Anew-1107.log` |
| Re-check, B (one `no-store` page every 45 min for about 25 h) | `run20261107-195737-ezwzu` | 7–8 Nov | new | `ttlmap-nostore-B-1107.log` |

The `no-store` runs and the re-check ask Anthropic only.

## Which file feeds what

| File | Feeds |
|---|---|
| `logs/ttlmap-*.log` (the run reports) | Paper Table 1 (vendor × setting, days 1–3) and Table 2 (the `no-store` change: days 2–3, A, A basic, B, OpenRouter, C), both made by hand from these reports |
| `logs/results/ttlmap-<run id>.jsonl` | Every call |
| `logs/raw-replies.jsonl`, the lines for A-new and B (7 Nov) | Anthropic's own `retrieved_at` time for each copy |
| `logs/probe.jsonl`, lines on `/cacheHeaders/` | Every download |

The 7–8 Nov re-check is not in a paper table yet.
