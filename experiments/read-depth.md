# Read depth and token cost: how far into a long page does each vendor read?

HTML depth pages (`/depth/html/<id>/<bytes>`) from 4 KB to 2 MB. Five depth codes sit at fixed
places in each page. Which codes an answer quotes shows how far the vendor read. Read depth is
judged from the answers, not from the server log.

| Part | Run ids | Date (2026) | Question wording |
|---|---|---|---|
| Main ladder, origin A | `run20261006-133840-n4lnt`, `-142315-ihseh`, `-153657-maa2d` (4 KB repeats); `-162352-7geo3`, `-165202-apkax` (8 KB repeats); `-182646-5ssxn` (4 KB–256 KB, three vendors); `-185735-maxx7` (512 KB); `-195108-p72fo` (1 MB); `-195648-xq5yo` (2 MB); `-202129-mquyx` (OpenAI, 4 KB–128 KB); `-203451-wfn95` (main run: 4 KB–2 MB, three vendors, 60 calls) | 6 Oct | old |
| Repeat, origin A | `run20261101-150249-cgf9c` (4 KB), `-151556-rmvir` (1 MB), `-151744-cvv3i` (2 MB, xAI) | 1 Nov | new (address + question) |
| Repeat, origin B | `run20261101-152159-jgizc` (4 KB), `-153355-to5cl` (1 MB), `-153543-wt84b` (2 MB, xAI) | 1 Nov | new |

## Which file feeds what

| File | Feeds |
|---|---|
| `logs/results/truncprobe-<run id>.jsonl` (the 11 runs of 6 Oct) | Figure `read-window-by-vendor` (`readDepth_plot_tokens.py`: input tokens against page size; this is also the token-cost figure) and figure `read-depth-grid` (`readDepth_plot_markers.py`: which of the 5 positions each vendor returned). The paper's read-depth table and cost shapes |
| `logs/n2-html-20261006-203451.log` | Printed output of the main run |
| `logs/results/truncprobe-<run id>.jsonl` (the 1 Nov runs) and `logs/raw-replies.jsonl` (their lines) | The repeat with the new question wording and on the second origin |
| `logs/probe.jsonl`, `logs/probe-vps.jsonl`, lines on `/depth/html/` | Crawler visits only |

Known gap: `readDepth_plot_markers.py` gets each page's 5 depth codes by downloading the live
page again. The test pages are not online anymore, so that figure cannot be redrawn from this data
alone.
