# Public endpoints: how old are the answers?

Public API endpoints whose value only goes up (block heights, pulse numbers, timestamps). We ask
each vendor to fetch an endpoint and return only its value. Comparing the value with the live
value at that time shows how old the vendor's copy was. No server of ours is involved.

## Which file feeds what

| File | What it is | Feeds |
|---|---|---|
| `logs/results/anchor-probe-lifetime.jsonl` | Main run, 3–6 Nov 2026: 4 vendors × up to 9 endpoints, 80 rounds, every 45 min | Figure `anchor-lifetime-staleness` (`publicPageEndpoint_plot.py`) and the staleness table `anchor-staleness-table` |
| `logs/results/anchor-truth-lifetime.jsonl` | The live value of the 9 endpoints, read every 5 min (`publicPageEndpoint_poll.py`) | Dates the OpenAI, xAI and Google answers. The table's "Updates" column (each endpoint's change interval) |
| `logs/results/anchor-probe-anthfill.jsonl` | Anthropic only, 7–10 Nov: the 6 endpoints not covered in the main run, plus a NIST re-test. Anthropic dates its own copies (`retrieved_at`) | Fills Anthropic's 6 endpoints in the figure and table |
| `logs/results/nist-usecache.jsonl` | Anthropic, 8 Nov, `use_cache:false`, 20 rounds | The NIST `no-store` finding: Anthropic serves an old copy, but fetches fresh when asked not to use its cache |

The Google × USGS cells are left out of the figure (a model read-out error on the 13-digit
timestamp, not staleness). Their data stays in the files.
