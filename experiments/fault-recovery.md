# Fault recovery: a page fails, how does the vendor retry?

Pages under `/fault/<kind>` fail in a chosen way (for example 404, 500, slow, or flaky). We count
each vendor's requests per fault and the tokens billed.

| Run | Origin | Run id | Date (2026) | Question wording |
|---|---|---|---|---|
| A1 | A | `run20261008-205249-kqsuv` | 8 Oct | old (A1 also asked an older question that did not name the depth codes) |
| A2 | A | `run20261010-190856-brrjp` | 10 Oct | old |
| A3 | A | `run20261013-070000-iq5kp` | 13 Oct | old |
| B1 | B | `run20261025-192546-u7swp` | 25 Oct | old |
| B2 | B | `run20261028-070001-mm2ba` | 28 Oct | old |
| B3 | B | `run20261030-130001-rt7qx` | 30 Oct | new (address + question) |
| Success baseline | B | `run20261101-122858-g2ip9`, `run20261101-123408-6egg4`, `run20261101-123913-3dmen` | 1 Nov | new |

## Which file feeds what

| File | Feeds |
|---|---|
| `logs/faults-redo-20261008.jsonl` (A1–A3), `logs/faults-originb-20261025.jsonl` (B1–B3), `logs/faults-originb-baseline.jsonl` | Per-fault results. Paper tables `tab:fault-behavior` and `tab:fault-behavior-full` (requests per fault per run) |
| `logs/results/faults-<run id>.jsonl` (all nine run ids) | Every call with its tokens. Figure `fault-token-cost` (`fault_plot.py`; the run ids are listed at the top of the script) |
| `logs/faults-originb-r3-anthropic-raw.jsonl` | Anthropic's whole replies for B3: its single error code and its reuse of a stored failure |
| `logs/raw-replies.jsonl`, the 9 lines for the baseline run ids | Whole replies for the baseline |
| `logs/probe.jsonl`, `logs/probe-vps.jsonl`, lines on `/fault/` | Each vendor request per fault (the run id is in the address's `?probe=` part) |
| `logs/faults-*-<date>-<time>.log` | Each run's printed table, for reading only |
