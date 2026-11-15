# aisearch-data

Data for the paper: what AI search tools (OpenAI, Anthropic, Google, xAI and others) fetched from
our test pages, and what they answered. The code that collected it and draws the figures is in the
companion code repo.

Licence: CC-BY 4.0 (see `LICENSE`).

## Using it

To redraw a figure, put this repo's `logs/` folder in the code repo's top folder, run the script
from there, and follow the guide for that experiment.

To read the data yourself: most files are JSON Lines, one record per line.

```python
import json
visits = [json.loads(line) for line in open("logs/probe.jsonl")]
```

## Guides

Each guide says which file feeds which figure or table.

| Experiment | Guide |
|---|---|
| A page changes. When do tools see the new version? | [correction](experiments/correction.md) |
| A page fails. How do tools retry? | [fault-recovery](experiments/fault-recovery.md) |
| A failed page is fixed. When do tools see the fix? | [heal-time](experiments/heal-time.md) |
| Does a tool give one user's saved copy to another user? (API) | [sharing-api](experiments/sharing-api.md) |
| The same, in the chat apps | [sharing-web-apps](experiments/sharing-web-apps.md) |
| Does a tool follow caching headers? | [cache-headers](experiments/cache-headers.md) |
| Which file types does each tool read? | [document-type](experiments/document-type.md) |
| How far into a long page does each tool read? | [read-depth](experiments/read-depth.md) |
| What does Anthropic's filtering step cost? | [dynamic-filtering](experiments/dynamic-filtering.md) |
| Does a tool see text added by JavaScript? | [javascript](experiments/javascript.md) |
| Public pages whose numbers only go up: how old are the answers? | [public-endpoints](experiments/public-endpoints.md) |
| Real homepages: how old are the answers? | [public-homepages](experiments/public-homepages.md) |
| Real XML files, feeds and llms.txt: which does each tool read? | [public-xml-files](experiments/public-xml-files.md) |

## Shared files

| File | One line is |
|---|---|
| `logs/probe.jsonl` | A request a tool made to test server A |
| `logs/probe-vps.jsonl` | A request a tool made to test server B |
| `logs/results/*.jsonl` | A question we sent a tool, and its answer |
| `logs/raw-replies.jsonl` | A tool's whole API reply |

Times are UTC.

## Words used in the guides

- **Vendor**: the company whose AI tool we asked (OpenAI, Anthropic, Google, xAI and others).
  `or:` in front of a vendor name means the call went through OpenRouter, a service that passes
  calls on to many vendors.
- **Origin A, origin B**: our two test web servers, `origin-a.example` and `origin-b.example`.
  They ran the same code on different networks.
- **Run id**: a name like `run20261013-193817-jixfj` (start date, start time, random letters).
  Every test page address holds one, so you can match a server request to the question that
  caused it.
- **Depth page**: a test page with five codes starting `TRUNC-`. They sit at 0%, 25%, 50%, 75% and
  95% of the way down. The codes an answer quotes show how far the vendor read.
- **Old and new question wording**: before 28 Oct 2026, we sent "Fetch <address> and answer from
  that page only. Question: …", ending with a request for the "study reference code". The depth
  pages have no code by that name. From 28 Oct we sent only the address, a blank line, and the
  question. Some experiments were repeated with the new wording to check the results held.
- **Whole replies** (`logs/raw-replies.jsonl`): the full API reply, saved only for runs from late
  October 2026 on. Earlier runs have only the answer text. Each guide says which runs have them.

## Left out

- Our server names. They appear as `origin-a.example` and `origin-b.example`.
- Our own visits to the test servers.
- Encrypted parts of replies. They cannot be read and no result uses them.
- Real site names in the homepage and XML file tests. Each site is an ID such as `site-017`. Some
  of those tables cannot be rebuilt from this data. Their guides say which.
