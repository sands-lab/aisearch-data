# JavaScript: do vendors see text that a script adds to the page?

We use the 4 KB depth page in five versions. In all five, the first code is plain HTML. The other
four codes are placed differently in each version:

| Version | Address | Where the other four codes are |
|---|---|---|
| Plain | `/depth/html/` | Plain HTML. This is the comparison page |
| Inline script | `/depth/jsInline/` | Scrambled inside a script on the page. The script unscrambles them and adds them to the page |
| Separate script | `/depth/jsExternal/` | The same, but the script is a separate file, `/depth/jsExternalScript/` |
| Data block | `/depth/jsData/` | Plain JSON in a data block, which a script copies into the page |
| JSON-LD | `/depth/jsonLd/` | Plain text in a schema.org JSON-LD block (structured data for search engines). No script runs |

All runs are on origin A, with a fresh page for each vendor and version.

| Part | Run ids (plain, inline script, separate script, data block) | Date (2026) | Question wording |
|---|---|---|---|
| Sitting 1: Anthropic's basic fetch tool, OpenAI, xAI | `run20261022-120649-p94xf`, `-120846-6m6hw`, `-121030-bhc9a`, `-121207-uklyf` | 22 Oct | old |
| Sitting 2 | `run20261023-193301-9xonb`, `-193504-f3cnr`, `-193644-bbz4z`, `-193820-b3q4h` | 23 Oct | old |
| Sitting 3 | `run20261025-061801-cba86`, `-062005-uxsz4`, `-062205-byc3f`, `-062343-5hobv` | 25 Oct | old |
| Side check: Anthropic's default fetch tool, which has a filtering step | `run20261022-121925-kq25z`, `-122155-gxaeb`, `-122242-tgi68`, `-122335-3d6u2` | 22 Oct | old |
| JSON-LD | `run20261026-185350-g7jht` | 26 Oct | old |
| JSON-LD | `run20261028-074101-jkuul` | 28 Oct | old |
| JSON-LD | `run20261030-191701-ip3gi` | 30 Oct | new |

A short run id like `-120846-6m6hw` has the same date as the one before it.

## Files

| File | What it holds |
|---|---|
| `logs/results/truncprobe-<run id>.jsonl` (19 runs) | The deepest code each vendor quoted. The paper's JavaScript table was made by hand from these. Its sentence on the filtering step comes from the four side-check runs |
| `logs/probe.jsonl`, lines on the five versions and on `/depth/jsExternalScript/` | Downloads for each question. No vendor asked for the separate script file |
| `logs/jsdepth-*.log`, `logs/jsld-*.log` | Each run's printed output |

There are no whole replies for these runs. There is no figure for this experiment.
