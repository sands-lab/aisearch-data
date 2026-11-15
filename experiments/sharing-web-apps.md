# Sharing in the chat apps: does an app give one account's saved copy to another account?

The same question as [sharing through the API](sharing-api.md), but a person typed the questions
into eight chat apps: Claude, ChatGPT, Gemini, Mistral, Grok, DeepSeek, Qwen and Meta AI. Each app
was used with two separate logins, `account-a` and `account-b`.

Four steps per app:

1. Account A asks about the page.
2. Account A asks again, in a new chat.
3. Account B asks about the same page.
4. Account B asks about a control page that no one asked about before.

All runs are on origin A. The person pasted the address and the standard question.

| Sitting | Run id | Date (2026) |
|---|---|---|
| 1 | `run20261011-160853-iau5p` (Claude, ChatGPT, Gemini, Mistral) and `run20261011-164744-6v78n` (Grok, DeepSeek, Qwen, Meta AI) | 11 Oct |
| 2 | `run20261012-115926-xpged` | 12 Oct |
| 3 | `run20261013-183019-6jnf3` | 13 Oct |

## Files

| File | What it holds |
|---|---|
| `logs/web-trials/corrections.md` | Read this first. It explains one paste mistake in sitting 1 (two replies joined back together, marked `reply_rebuilt`), and some downloads in sitting 1 that the helper tool missed |
| `logs/sharing-redo/web-<run id>.jsonl` | The steps: downloads before and after each answer, and what each verdict was based on. The paper's chat-app table (per app, out of 3 sittings: did the same login reuse a copy, and did a different login get it) was made by hand from these |
| `logs/web-trials/raw/<run id>.jsonl` | The replies as pasted from each app. From sitting 2 on, also the time each reply was pasted (`answered_unix`) |
| `logs/results/sharing-<run id>.jsonl` | The same calls in the standard per-call format |
| `logs/probe.jsonl`, lines on `/depth/html/sh-<run id>-<app>…` and the icon requests that came from them | Every download. Some pages were visited days later, so match lines by page id, not by time |

There is no figure for this experiment.
