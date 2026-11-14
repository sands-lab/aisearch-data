# Account sharing through the API

Does a vendor hand one caller's stored copy of a page to another caller? Four kinds of
comparison, each for OpenAI, Anthropic and xAI (12 comparisons): the same caller twice
(`within`), two models (`model`), two paying accounts (`account`), and two OpenRouter user names
(`user`). Each try uses a fresh shared page plus a control page.

| Rounds | Origin | When (UTC, 2026) | Question wording | Files |
|---|---|---|---|---|
| r1–r6 | A | 11 Oct 13:01 to 12 Oct 19:00, every 6 hours | old | `sharing-redo/r<N>-<comparison>-<vendor>.*` (72 run ids) |
| ob1 | B | 28 Oct (ob1, ob2 and ob3us all ran 18:37–19:32) | old | `sharing-redo/ob1-*` (12 run ids) |
| ob2 | B | 28 Oct | new (address + question) | `sharing-redo/ob2-*` (12 run ids) |
| ob3us | B | 28 Oct | new | `sharing-redo/ob3us-account-*` (3 run ids). Our direct-key calls were sent out through a US tunnel |
| gem1, gem2, gem3, gem3b | B | 29 Oct, 31 Oct, 2 Nov, 2 Nov | new | `sharing-redo/gem*-within-gemini.*`: Gemini side check, same caller twice (4 run ids) |

## Which file feeds what

| File | Feeds |
|---|---|
| `logs/sharing-redo/r<N>-*.log` | The run output with each try's verdict. The paper's API sharing table (71 of 72 shared, 1 void) was made by hand from these |
| `logs/sharing-redo/r<N>-*.jsonl`, `ob*-*.jsonl`, `gem*-*.jsonl` | The steps of each try (each page id is `sh-<run id>`) |
| `logs/sharing-redo/<label>-graded.json` | The grading of the origin B rounds and the Gemini check, made after each round from the full server log (`sharingApi_score.py`). Use these, not the printed verdicts, on origin B |
| `logs/results/sharing-<run id>.jsonl` | Every call with its tokens |
| `logs/sharing-redo/originB-fetcher-ips.csv` | The country, region and network owner of every address that downloaded a page on origin B. Rows with `run` = `ob3us` are the tries whose direct-key calls went through the US tunnel |
| `logs/sharing-redo/schedule.log` | When each round on origin A started and which code version it used. Its times carry the local offset +03:00 |
| `logs/raw-replies.jsonl`, the 4 lines for the Gemini run ids | Google's `urlRetrievalStatus` for the Gemini check |
| `logs/probe.jsonl` (r1–r6), `logs/probe-vps.jsonl` (ob*, gem*), lines on `/depth/html/sh-<run id>…` | Every download of each page |

The origin B repeat and the Gemini side check are not in a paper table yet.
