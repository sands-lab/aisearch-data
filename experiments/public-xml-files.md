# Real XML files, feeds and llms.txt: which ones does each vendor read?

299 files from the watched sites: sitemaps and feeds by declared type (`application/xml`,
`text/xml`, RSS, Atom) and `llms.txt` served as `text/plain`. Each vendor was asked to read each
file. Its answer was scored against the file's own text, downloaded just before and just after
the run.

The files are not named. Each is a random ID (`file-001` … `file-299`), not linked to the
homepage site IDs. There is no file address, no file text and no answer text.

## Files

| File | What it holds |
|---|---|
| `logs/public-xml/files.csv` | Per file: declared type, kind (`sitemap`, `feed` or `llms.txt`, from how it was found), how it was found, size in bytes |
| `logs/public-xml/answers-four-vendors.csv` | The four-vendor run, 24–25 Oct 2026. Per file × vendor: outcome (`read`, `boilerplate only` = only standard header lines, `fetched, one line`, `refused`, `failed`, `inconclusive`, scored with both downloads). For OpenAI: the refusal class (own fetch error, site's error, no reason given, quote limit) |
| `logs/public-xml/answers-google-rerun.csv` | The Google-only re-run, 31 Oct–1 Nov 2026 (`gemini-3.1-flash-lite`). Per file: outcome, Google's fetch status, stop reason, error code and message, and the number of tool-text tokens |
| `logs/public-xml/selection-counts.csv` | How 776 watched sites became 299 test files |

## Which file feeds what

| Paper result | Files |
|---|---|
| Figure `public-xml-file-test-grid` | `files.csv` with `answers-four-vendors.csv` |
| Table `tab:gemini-public` | Google from `answers-google-rerun.csv`, OpenAI (with refusal classes) from `answers-four-vendors.csv` |
| The selection funnel | `selection-counts.csv` |

The figure script (`publicPageXmlFile_plot.py`) reads the private answers and file texts, so it
cannot be rerun on this data. These tables hold the same outcomes, made with the scoring rules
in `publicPageXmlFile_run.py score`.
