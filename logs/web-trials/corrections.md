# Corrections to the web-app sharing sittings

The pasted-reply files (`web-trials/raw/<run>.jsonl`) and step files
(`sharing-redo/web-<run>.jsonl`) are shipped as recorded, with one exception: the paste
mistake in sitting 1, step 2 (below), where two replies were put back together. All times are UTC.

## How "before the answer" was drawn in sitting 1

Sitting 1 (`run20261011-160853-iau5p` and `run20261011-164744-6v78n`) ran before the helper
recorded when each reply was pasted (`answered_unix` exists from sitting 2 on). For these two
runs, a download counts as "before the answer" if it falls between that step's prompt time and
the next prompt's time (roughly when the reply was pasted). Anyone can redo this from the shipped
server-log lines in `logs/probe.jsonl`, which are matched by page id.

## run20261011-160853-iau5p (sitting 1: Claude, ChatGPT, Gemini, Mistral, plus steps 1-2 for Grok, DeepSeek, Qwen, Meta AI)

A multi-line reply from Qwen was pasted into the terminal instead of the editor. Its lines spread
over the next prompts. Both affected replies were put back together; each record carries a
`reply_rebuilt` field saying so.

- `qwen-sh2-run20261011-161941-o42rc` (Qwen, step 2): the reply started in the one-line notes
  prompt (after two stray terminal characters and a left-arrow key code, which are removed) and
  continued in the reply field of the next app's record (Meta AI, below). The rebuilt reply is:
  the notes line, then the piece found in Meta AI's reply field. Qwen's own reply field held only
  the last line of that piece again, so it is not used. A few characters between the two pieces
  were lost in the paste (the second piece starts mid-word, "ode at depth=25%"); they are not
  filled in. Verdict comes from the server log: Qwen downloaded the page again at
  16:21:02-16:21:17. Unchanged.
- `metaai-sh2-run20261011-162211-j7yay` (Meta AI, step 2): the reply field held the end of
  Qwen's reply (Qwen's page code `564fc6bcacc0`), not Meta AI's. Meta AI's own reply was typed
  into the notes prompt and holds its own page code `091a537e42a3`. The rebuilt reply is that
  notes text. The step file's "code quoted: false" for this step comes from the mistake; grade
  the code from the rebuilt reply. Verdict comes from the server log: Meta AI downloaded the page
  again at 16:22:41. Unchanged.
- Steps 3-4 were not run for Grok, DeepSeek, Qwen and Meta AI in this run. Those four apps were
  rerun with all four steps as `run20261011-164744-6v78n`.

## run20261011-164744-6v78n (sitting 1 for Grok, DeepSeek, Qwen, Meta AI; all four steps)

The helper read the server log only when each reply was pasted, so it missed requests that came
after an answer. The recorded verdicts are right and stay as they are; these entries add facts.

- Grok, step 2 (account A asks again): 0 downloads before the answer, 2 after (16:54:55,
  16:57:48). It answered from a stored copy.
- Grok, step 3 (account B asks): 0 downloads before the answer, 2 after (16:58:44, 16:58:51).
  Account B was answered from account A's copy, so the copy was shared.
- The after-answer requests cannot have produced either answer.
- DeepSeek, Qwen and Meta AI had no requests after any answer, so their recorded downloads are
  complete.
