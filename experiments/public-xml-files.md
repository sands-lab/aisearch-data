# Real XML files, feeds and llms.txt: which ones does each vendor read?

We collected 299 real files from the sites we watched:

- sitemaps (lists of a site's pages) and news feeds, grouped by the type the site declared:
  `application/xml`, `text/xml`, RSS or Atom.
- `llms.txt` files (a site's short guide for AI tools), served as `text/plain`.

We asked each vendor to read each file and quote its first lines. We downloaded each file ourselves
just before and just after the run, and scored each answer against those downloads.

The files are not named. Each is a random ID (`file-001` to `file-299`). These IDs are not linked to
the site IDs in the homepage test. There is no address, no file text and no answer text.

## Files

| File | One row is | What it holds |
|---|---|---|
| `logs/public-xml/files.csv` | A file | Its declared type. Its kind (`sitemap`, `feed` or `llms.txt`), from how we found it. How we found it. Its size in bytes |
| `logs/public-xml/answers-four-vendors.csv` | A file and vendor | The run with four vendors, 24–25 Oct 2026. The outcome (see below). For OpenAI, why it refused: its own fetch error, the site's error, no reason given, or a limit on how much it may quote |
| `logs/public-xml/answers-google-rerun.csv` | A file | A later run with Google only, 31 Oct–1 Nov 2026 (`gemini-3.1-flash-lite`). The outcome, Google's own fetch status, why the reply stopped, any error code and message, and how many tokens of file text the tool passed to the model |
| `logs/public-xml/selection-counts.csv` | A selection step | How 776 watched sites became 299 test files |

**Outcomes.** The first rule that fits is used:

| Outcome | Meaning |
|---|---|
| `failed` | The call returned an error or an empty answer |
| `read` | The answer holds at least 5 distinctive words from the file, or copies one of its first 3 lines |
| `boilerplate only` | The answer copies only standard lines that every XML file or feed starts with, such as `<?xml …?>` or `<rss>` |
| `fetched, one line` | The answer says the file came as one long line. xAI's tool sometimes passes sitemaps on this way |
| `refused` | The answer says it could not read or fetch the file |
| `inconclusive` | None of the above |
| `no key` | Google re-run only: we could not download the file ourselves, so the answer could not be scored |

## Which file gives which paper result

| Paper result | Files |
|---|---|
| The grid figure of outcomes per file and vendor | `files.csv` with `answers-four-vendors.csv` |
| The Google table | Google from `answers-google-rerun.csv`. OpenAI, with why it refused, from `answers-four-vendors.csv` |
| How the files were chosen | `selection-counts.csv` |

The figure script, `publicPageXmlFile_plot.py`, needs the answers and file text, which are not
shared, so it cannot be rerun on this data. The outcomes here are the same ones it draws.
