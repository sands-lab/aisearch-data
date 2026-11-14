# Correction: a page changes at the same address

Each page shows one version, then switches to a new version at the same address. We then ask the
vendor about it again at fixed times and check which version it quotes.

Six sittings, three per origin:

| Sitting | Origin | Run id | Dates (2026) | Question wording |
|---|---|---|---|---|
| s1 | A | `run20261013-193817-jixfj` | 13–17 Oct | old |
| s2 | A | `run20261014-114417-akrf4` | 15–19 Oct | old |
| s3 | A | `run20261014-114417-ghfrh` | 17–21 Oct | old |
| b1 | B | `run20261026-154521-bino7` | 26–30 Oct | old |
| b2 | B | `run20261028-204349-5kcma` | 30 Oct–2 Nov | new (address + question) |
| b3 | B | `run20261028-204349-e5fpg` | 1–5 Nov | new (address + question) |

The origin B sittings are named `b1`–`b3`; the raw records used a different name for them.

## Which file feeds what

| File | Feeds |
|---|---|
| `logs/correction-<sitting>.state.json` | Each page's versions, switch time and every answer. Voided pages stay in, marked void with a reason |
| `logs/probe.jsonl` (origin A), `logs/probe-vps.jsonl` (origin B), lines on `/correction/html/` and `/correction/txt/` | When each vendor downloaded each version. With the state files, this feeds figures `correction-timeline` and `correction-fetched-but-old` (`correction_plot.py`, runs given as `ORIGIN:RUN:PROMPT`) |
| `logs/raw-replies.jsonl`, the lines for b3 | The appendix numbers on OpenAI answering with the old version after downloading the new one |
| `logs/correction-<sitting>.plan.txt`, `.out` | The planner's printed schedule and the run's printed output, for reading only. Local times in the plan files are marked UTC+3 |

The paper's correction panel (d) uses s1–s3.
