# Anthropic's filtering step: what does it cost?

Anthropic's `web_fetch` tool comes in two versions. `web_fetch_20250910` sends the page as is
(filtering off). `web_fetch_20260209` first runs a filtering step (filtering on). We ask the same
depth pages with each version and compare input tokens. All direct Anthropic calls use
`claude-sonnet-5`. All on origin A, on `/depth/<type>/` pages.

| Part | Run ids | Dates (2026) |
|---|---|---|
| Round 1: 8 types at 8 KB, with an OpenRouter control (`or:anthropic`, no filtering) | `run20261015-13*` | 15 Oct |
| 8 types at 2, 4 and 16 KB, with the OpenRouter control | `run20261015-14*`, `run20261015-15*`, plus the csv 16 KB rerun `run20261015-161817-j6iho` | 15 Oct |
| HTML 32, 64 and 128 KB | `run20261015-17*` | 15 Oct |
| Round 2 | all `run20261016-*` | 16 Oct |
| Round 3 | all `run20261017-*` | 17 Oct |
| HTML 2, 4 and 16 KB, extra repeats | all `run20261019-*`, `run20261020-*` | 19–20 Oct |

The `extra.web_fetch_version` field in each record says off or on.

## Which file feeds what

| File | Feeds |
|---|---|
| `logs/results/truncprobe-<run id>.jsonl` (75 runs) | Input tokens, deepest depth code quoted, number of rounds, tool version. `dynFilter_score.py` pools the rounds into a mean and spread. `dynFilter_plot.py` draws the paper's two-panel figure `dynamic-filtering-combined` |
| `logs/probe.jsonl`, lines on `/depth/<type>/` | Crawler visits only. Cost and read depth come from the result files |

The raw replies that showed the filtering step's code blocks were not kept, so they are not here.
