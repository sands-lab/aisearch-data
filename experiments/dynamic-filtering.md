# Anthropic's filtering step: what does it cost?

Anthropic's `web_fetch` tool comes in two versions. `web_fetch_20250910` passes the page on as it
is (filtering off). `web_fetch_20260209` first runs a filtering step (filtering on). We ask about
the same depth pages with each version and compare the input tokens billed.

All direct Anthropic calls use `claude-sonnet-5`. All runs are on origin A, on `/depth/<type>/`
pages. The field `extra.web_fetch_version` in each record says which version was used.

| Part | Run ids | Dates (2026) |
|---|---|---|
| Round 1: 8 types at 8 KB, plus the same calls through OpenRouter (`or:anthropic`), which has no filtering step | `run20261015-13*` | 15 Oct |
| 8 types at 2, 4 and 16 KB, plus the OpenRouter calls | `run20261015-14*`, `run20261015-15*`, and the csv 16 KB re-run `run20261015-161817-j6iho` | 15 Oct |
| HTML at 32, 64 and 128 KB | `run20261015-17*` | 15 Oct |
| Round 2 | all `run20261016-*` | 16 Oct |
| Round 3 | all `run20261017-*` | 17 Oct |
| HTML at 2, 4 and 16 KB, extra repeats | all `run20261019-*` and `run20261020-*` | 19–20 Oct |

All runs use the old question wording.

## Files

| File | What it holds |
|---|---|
| `logs/results/truncprobe-<run id>.jsonl` (75 runs) | Input tokens, the deepest code quoted, number of rounds, and the tool version |
| `logs/probe.jsonl`, lines on `/depth/<type>/` | Vendor downloads. Cost and read depth come from the result files, not from here |

There are no whole replies for these runs.

## Redraw the figure

From the code repo's top folder, with `logs/` in place:

```sh
python3 scripts/dynFilter_score.py           # prints the mean and spread over the rounds
python3 scripts/dynFilter_plot.py --out figures/dynamic-filtering-combined
```

Both scripts read `logs/results/truncprobe-run*.jsonl` by default.
