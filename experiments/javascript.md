# Does a vendor see text added by JavaScript?

The 4 KB depth page in five versions. The first depth code is plain HTML in all of them. The other
four are: plain HTML (`/depth/html/`, the baseline), scrambled inside an inline script
(`/depth/jsInline/`), scrambled inside a separate script file (`/depth/jsExternal/`, which loads
`/depth/jsExternalScript/`), plain JSON in a data block that a script copies in (`/depth/jsData/`),
and plain text in a schema.org JSON-LD block (`/depth/jsonLd/`). All on origin A, one fresh page
per vendor and version.

| Part | Run ids (plain, inline, external, data block) | Date (2026) | Question wording |
|---|---|---|---|
| Sitting 1 (Anthropic basic tool, OpenAI, xAI) | `run20261022-120649-p94xf`, `-120846-6m6hw`, `-121030-bhc9a`, `-121207-uklyf` | 22 Oct | old |
| Sitting 2 | `run20261023-193301-9xonb`, `-193504-f3cnr`, `-193644-bbz4z`, `-193820-b3q4h` | 23 Oct | old |
| Sitting 3 | `run20261025-061801-cba86`, `-062005-uxsz4`, `-062205-byc3f`, `-062343-5hobv` | 25 Oct | old |
| Filtering side check (Anthropic only, default tool) | `run20261022-121925-kq25z`, `-122155-gxaeb`, `-122242-tgi68`, `-122335-3d6u2` | 22 Oct | old |
| JSON-LD | `run20261026-185350-g7jht` | 26 Oct | old |
| JSON-LD | `run20261028-074101-jkuul` | 28 Oct | old |
| JSON-LD | `run20261030-191701-ip3gi` | 30 Oct | new (address + question) |

## Which file feeds what

| File | Feeds |
|---|---|
| `logs/results/truncprobe-<run id>.jsonl` (19 runs) | The deepest depth code each vendor quoted. Paper table `tab:js-variants` was made by hand from these. The filtering sentence comes from the four side-check runs |
| `logs/probe.jsonl`, lines on the five page versions and `/depth/jsExternalScript/` | Downloads per question, and that no vendor asked for the script file |
| `logs/jsdepth-*.log`, `logs/jsld-*.log` | Printed run output, for reading only |

No whole replies: all runs came before whole replies were kept.
