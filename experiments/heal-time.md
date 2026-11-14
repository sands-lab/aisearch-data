# Heal time: a failed page is fixed. When does the vendor see the fix?

Each page first fails (503, 404 or 403), is asked about, is then fixed, and is asked about again
on a schedule. 72 pages per sitting.

| Sitting | Origin | Run id | Dates (2026) | Question wording |
|---|---|---|---|---|
| s1 | A | `run20261022-154816-24q4v` | 22–23 Oct | old |
| s2 | A | `run20261025-144842-7meo9` | 25–26 Oct | old |
| s3 | A | `run20261025-144842-nqbxk` | 28 Oct | old |
| s4 | A | `run20261030-175410-wj5ee` | 1–2 Nov | new (address + question) |
| s5 | A | `run20261030-175410-jbbdr` | 3–4 Nov | new |
| b1 | B | `run20261027-143547-wj8ef` | 29–30 Oct | new |
| b2 | B | `run20261027-143547-6gq93` | 1–2 Nov | new |
| b3 | B | `run20261027-143547-y7u3f` | 3–4 Nov | new |

## Which file feeds what

| File | Feeds |
|---|---|
| `logs/heal-<sitting>.results.json` | Figure `heal-timeline` (`heal_plot.py --out <dir> <results files…>`; it leaves out 4 pages and prints each one). These files cannot be rebuilt from this data: scoring needs the page-code secret, which is not stored anywhere |
| `logs/heal-<sitting>.state.json` | The schedule, fail and fix times and every answer |
| `logs/raw-replies.jsonl`, the 576 lines for s4, s5, b2 and b3 (144 each) | With the state and results files and both server logs, the appendix numbers on OpenAI downloading the fixed page but still answering with the failure (`heal_score_openaiStale.py`). s1–s3 and b1 ran before whole replies were kept |
| `logs/probe.jsonl`, `logs/probe-vps.jsonl`, lines on `/heal/` | Each vendor download |
| `logs/heal-<sitting>.report.txt` (s3, s4, s5, b1–b3) | Readable reports, for reading only |
