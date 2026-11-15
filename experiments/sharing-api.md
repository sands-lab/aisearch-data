# Sharing through the API: does a vendor give one caller's saved copy to another caller?

One caller asks about a fresh page. The page then changes. A second caller asks about the same page.
If the second caller's answer quotes the first version, the vendor shared its saved copy. Each try
also asks about a control page, which no one asked about before.

We test four kinds of second caller, each for OpenAI, Anthropic and xAI, which makes 12
comparisons:

| Comparison | Second caller |
|---|---|
| `within` | The same caller again |
| `model` | The same account, a different model |
| `account` | A different paying account |
| `user` | The same OpenRouter account, a different user name |

| Rounds | Origin | When (UTC, 2026) | Question wording | Files in `logs/sharing-redo/` |
|---|---|---|---|---|
| r1–r6 | A | 11 Oct 13:01 to 12 Oct 19:00, every 6 hours | old | `r<N>-<comparison>-<vendor>.*` (72 run ids) |
| ob1 | B | 28 Oct, 18:37–19:32, with ob2 and ob3us | old | `ob1-*` (12 run ids) |
| ob2 | B | 28 Oct | new | `ob2-*` (12 run ids) |
| ob3us | B | 28 Oct | new | `ob3us-account-*` (3 run ids). Our direct calls to each vendor went out through a US network address |
| gem1, gem2, gem3, gem3b | B | 29 Oct, 31 Oct, 2 Nov, 2 Nov | new | `gem*-within-gemini.*`: a check on Google's Gemini, same caller twice (4 run ids) |

The paper reports r1–r6: 71 of 72 tries shared, and 1 was thrown out. The origin B rounds and the
Gemini check are repeats and are not in the paper.

## Files

| File | What it holds |
|---|---|
| `logs/sharing-redo/r<N>-*.log` | Each try's printed output, with its verdict. The paper's sharing table was made by hand from these |
| `logs/sharing-redo/*.jsonl` | The steps of each try. Each page id is `sh-<run id>` |
| `logs/sharing-redo/<round>-graded.json` | Grading of the origin B rounds and the Gemini check, made from the full server log. On origin B, use these, not the printed verdicts |
| `logs/sharing-redo/originB-fetcher-ips.csv` | The country, region and network owner of every address that downloaded a page on origin B. Rows with `run` = `ob3us` are the tries sent through the US address |
| `logs/sharing-redo/schedule.log` | When each round on origin A started. Its times are UTC+3 |
| `logs/results/sharing-<run id>.jsonl` | Every call, with its tokens |
| `logs/raw-replies.jsonl`, the 4 lines for the Gemini runs | Google's fetch status (`urlRetrievalStatus`) |
| `logs/probe.jsonl` (r1–r6), `logs/probe-vps.jsonl` (ob*, gem*), lines on `/depth/html/sh-<run id>…` | Every download of each page |
