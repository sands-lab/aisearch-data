# Heal time: a failed page is fixed. When do vendors see the fix?

Each page first fails with a 503, 404 or 403 error, and we ask about it. Then the page is fixed,
and we ask again on a schedule. There are 72 pages per sitting.

| Sitting | Origin | Run id | Dates (2026) | Question wording |
|---|---|---|---|---|
| s1 | A | `run20261022-154816-24q4v` | 22–23 Oct | old |
| s2 | A | `run20261025-144842-7meo9` | 25–26 Oct | old |
| s3 | A | `run20261025-144842-nqbxk` | 28 Oct | old |
| s4 | A | `run20261030-175410-wj5ee` | 1–2 Nov | new |
| s5 | A | `run20261030-175410-jbbdr` | 3–4 Nov | new |
| b1 | B | `run20261027-143547-wj8ef` | 29–30 Oct | new |
| b2 | B | `run20261027-143547-6gq93` | 1–2 Nov | new |
| b3 | B | `run20261027-143547-y7u3f` | 3–4 Nov | new |

## Files

| File | What it holds |
|---|---|
| `logs/heal-<sitting>.results.json` | One record per page and check time: whether the vendor downloaded the page (`fetch`) and whether its answer held the fixed page's code (`code`). These cannot be rebuilt from this data, because scoring used a secret that was not saved |
| `logs/heal-<sitting>.state.json` | The schedule, the fail and fix times, and every answer |
| `logs/raw-replies.jsonl`, 144 lines each for s4, s5, b2 and b3 | Whole replies. The other sittings have none |
| `logs/probe.jsonl`, `logs/probe-vps.jsonl`, lines on `/heal/` | Every vendor download |
| `logs/heal-<sitting>.report.txt` (s3, s4, s5, b1–b3) | A readable summary of each sitting |

## Redraw the figure

From the code repo's top folder, with `logs/` in place:

```sh
python3 scripts/heal_plot.py --out figures logs/heal-s*.results.json logs/heal-b*.results.json
```

This writes `heal-timeline`. It leaves out 4 pages and prints which ones.

To check the results files against the raw logs, rebuild one from its state file and the server
log. The codes come from `logs/page-codes.csv`, so no secret and no API key is needed:

```sh
./bin/probe-trial -heal-report -heal-stateFile logs/heal-b1.state.json \
  -serverLog logs/probe-vps.jsonl -pageCodeFile logs/page-codes.csv \
  -heal-reportFile heal-b1.check.json
```

Sittings `s1`–`s5` ran on origin A (`logs/probe.jsonl`), `b1`–`b3` on origin B
(`logs/probe-vps.jsonl`).

The appendix numbers on OpenAI (it downloads the fixed page but still answers with the failure)
come from:

```sh
python3 scripts/heal_score_openaiStale.py --group A=s4,s5 --group B=b2,b3 \
  --server-log origin-a.example=logs/probe.jsonl \
  --server-log origin-b.example=logs/probe-vps.jsonl
```
