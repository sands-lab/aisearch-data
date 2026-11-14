# Account sharing in the chat apps

The same question as `sharing-api.md`, asked by a person in eight chat apps (Claude, ChatGPT,
Gemini, Mistral, Grok, DeepSeek, Qwen, Meta AI) with two separate logins (`account-a`,
`account-b`). Four steps per app: A reads the page, A asks again in a new chat, B asks the same
page, B asks a control page. All on origin A, with the web prompt (address line plus the standard
question).

| Sitting | Run id | Date (2026) |
|---|---|---|
| 1 | `run20261011-160853-iau5p` (Claude, ChatGPT, Gemini, Mistral; all 4 steps) and `run20261011-164744-6v78n` (Grok, DeepSeek, Qwen, Meta AI; all 4 steps) | 11 Oct |
| 2 | `run20261012-115926-xpged` | 12 Oct |
| 3 | `run20261013-183019-6jnf3` | 13 Oct |

## Which file feeds what

| File | Feeds |
|---|---|
| `logs/sharing-redo/web-<run id>.jsonl` | The steps: downloads before and after each answer, and the inputs to each verdict. Paper table `tab:app-sharing` (same login kept a copy, different login shared, out of 3 per app) was made by hand from these |
| `logs/web-trials/raw/<run id>.jsonl` | The replies as pasted from each app. From sitting 2 on, it also holds the time each reply was pasted (`answered_unix`) |
| `logs/web-trials/corrections.md` | Read this first. It explains the one paste mistake in sitting 1 (two replies put back together, marked `reply_rebuilt`), and the downloads after an answer that the helper missed in sitting 1 |
| `logs/results/sharing-<run id>.jsonl` | The standard per-call records |
| `logs/probe.jsonl`, lines on `/depth/html/sh-<run id>-<app>…` and the icon requests that came from them | Every download. Some pages got vendor visits days later, so the lines are matched by page id, not by a time window |

The hand-typed notes field was removed from the pasted replies. It held remarks like "opened a
new chat", which no result uses.
