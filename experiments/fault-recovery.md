# Fault recovery: a page fails. How do vendors retry?

Pages under `/fault/<kind>` fail in a chosen way, for example 404, 500, slow, or failing only some
of the time. For each fault we count how many requests each vendor makes, and how many tokens it
bills.

| Run | Origin | Run id | Date (2026) | Question wording |
|---|---|---|---|---|
| A1 | A | `run20261008-205249-kqsuv` | 8 Oct | old. A1 also asked an earlier question that did not mention the codes |
| A2 | A | `run20261010-190856-brrjp` | 10 Oct | old |
| A3 | A | `run20261013-070000-iq5kp` | 13 Oct | old |
| B1 | B | `run20261025-192546-u7swp` | 25 Oct | old |
| B2 | B | `run20261028-070001-mm2ba` | 28 Oct | old |
| B3 | B | `run20261030-130001-rt7qx` | 30 Oct | new |
| Normal page, for comparison | B | `run20261101-122858-g2ip9`, `run20261101-123408-6egg4`, `run20261101-123913-3dmen` | 1 Nov | new |

## Files

| File | What it holds |
|---|---|
| `logs/faults-redo-20261008.jsonl` (A1–A3), `logs/faults-originb-20261025.jsonl` (B1–B3), `logs/faults-originb-baseline.jsonl` (normal page) | Per fault and run: requests made and the outcome. The paper's fault tables come from these |
| `logs/results/faults-<run id>.jsonl` | Every call, with its token counts |
| `logs/faults-originb-r3-anthropic-raw.jsonl` | Anthropic's whole replies for B3. They show its one error code, and that it reused a stored failure |
| `logs/raw-replies.jsonl`, lines for the three normal-page runs | Whole replies for those runs |
| `logs/probe.jsonl`, `logs/probe-vps.jsonl`, lines on `/fault/` | Every vendor request. The run id is in the `?probe=` part of the address |
| `logs/faults-*-<date>-<time>.log` | Each run's printed summary table |

## Redraw the figure

From the code repo's top folder, with `logs/` in place:

```sh
python3 scripts/fault_plot.py --logs logs --out figures \
  --runs A=run20261008-205249-kqsuv,run20261010-190856-brrjp,run20261013-070000-iq5kp \
  --runs B=run20261025-192546-u7swp,run20261028-070001-mm2ba,run20261030-130001-rt7qx \
  --baseline B=logs/faults-originb-baseline.jsonl
```

This writes `fault-token-cost`.
