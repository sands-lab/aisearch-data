# Correction: a page changes. When do vendors see the new version?

Each page shows one version, then switches to a new version at the same address. We ask the vendor
about the page again at set times and check which version its answer quotes.

Six sittings, three on each origin:

| Sitting | Origin | Run id | Dates (2026) | Question wording |
|---|---|---|---|---|
| s1 | A | `run20261013-193817-jixfj` | 13–17 Oct | old |
| s2 | A | `run20261014-114417-akrf4` | 15–19 Oct | old |
| s3 | A | `run20261014-114417-ghfrh` | 17–21 Oct | old |
| b1 | B | `run20261026-154521-bino7` | 26–30 Oct | old |
| b2 | B | `run20261028-204349-5kcma` | 30 Oct–2 Nov | new |
| b3 | B | `run20261028-204349-e5fpg` | 1–5 Nov | new |

The paper's main correction panel uses s1–s3. The origin B sittings repeat it.

## Files

| File | What it holds |
|---|---|
| `logs/correction-<sitting>.state.json` | Each page's two versions, the switch time, and every answer. Pages we threw out are still there, marked void with the reason |
| `logs/probe.jsonl` (origin A), `logs/probe-vps.jsonl` (origin B), lines on `/correction/html/` and `/correction/txt/` | When each vendor downloaded each version |
| `logs/raw-replies.jsonl`, lines for b3 | Whole replies. The appendix counts OpenAI answers that quote the old version after downloading the new one |
| `logs/correction-<sitting>.plan.txt` and `.out` | The planned schedule and the run's printed output. Times in the plan files are UTC+3 |

## Redraw the figures

From the code repo's top folder, with `logs/` in place:

```sh
mkdir -p figures
python3 scripts/correction_plot.py --logs logs \
  --origin A=logs/probe.jsonl --origin B=logs/probe-vps.jsonl \
  --out figures A:s1:old A:s2:old A:s3:old
```

This writes `correction-timeline` and `correction-fetched-but-old`. Each sitting is given as
`origin:sitting:wording`. Add `B:b1:old B:b2:new B:b3:new` to include origin B.
