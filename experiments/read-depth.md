# Read depth: how far into a long page does each vendor read, and what does it cost?

We use HTML depth pages (`/depth/html/<id>/<bytes>`) from 4 KB to 2 MB. Each has five codes at set
points down the page. The codes an answer quotes show how far the vendor read. We judge read depth
from the answers, not from the server log. The input tokens each call was billed show the cost.

| Part | Run ids | Date (2026) | Question wording |
|---|---|---|---|
| Main test, origin A | `run20261006-133840-n4lnt`, `-142315-ihseh`, `-153657-maa2d` (4 KB repeats); `-162352-7geo3`, `-165202-apkax` (8 KB repeats); `-182646-5ssxn` (4 KB to 256 KB, three vendors); `-185735-maxx7` (512 KB); `-195108-p72fo` (1 MB); `-195648-xq5yo` (2 MB); `-202129-mquyx` (OpenAI, 4 KB to 128 KB); `-203451-wfn95` (main run: 4 KB to 2 MB, three vendors, 60 calls) | 6 Oct | old |
| Repeat, origin A | `run20261101-150249-cgf9c` (4 KB), `-151556-rmvir` (1 MB), `-151744-cvv3i` (2 MB, xAI) | 1 Nov | new |
| Repeat, origin B | `run20261101-152159-jgizc` (4 KB), `-153355-to5cl` (1 MB), `-153543-wt84b` (2 MB, xAI) | 1 Nov | new |

A short run id like `-142315-ihseh` has the same date as the one before it.

## Files

| File | What it holds |
|---|---|
| `logs/results/truncprobe-<run id>.jsonl` | Every call: the codes quoted, and input and output tokens. The 11 runs of 6 Oct give the paper's read-depth table and figures. The 1 Nov runs check that the result holds with the new wording and on origin B |
| `logs/n2-html-20261006-203451.log` | Printed output of the main run |
| `logs/raw-replies.jsonl`, lines for the 1 Nov runs | Whole replies. The 6 Oct runs have none |
| `logs/probe.jsonl`, `logs/probe-vps.jsonl`, lines on `/depth/html/` | Vendor downloads |

## Redraw the figures

From the code repo's top folder, with `logs/` in place:

```sh
R=logs/results/truncprobe-run20261006
python3 scripts/readDepth_plot_tokens.py figures/read-window-by-vendor \
  $R-133840-n4lnt.jsonl $R-142315-ihseh.jsonl $R-153657-maa2d.jsonl \
  $R-162352-7geo3.jsonl $R-165202-apkax.jsonl $R-182646-5ssxn.jsonl \
  $R-185735-maxx7.jsonl $R-195108-p72fo.jsonl $R-195648-xq5yo.jsonl \
  $R-202129-mquyx.jsonl $R-203451-wfn95.jsonl
```

This draws input tokens against page size for each vendor. Without the file list, the script reads
every `truncprobe` file, which mixes in other experiments.

The second figure, `read-depth-grid` (`readDepth_plot_markers.py`), shows which of the five codes
each vendor quoted. It reads each page's codes from `logs/page-codes.csv`, so it needs no network:

```sh
python3 scripts/readDepth_plot_markers.py --codes logs/page-codes.csv figures/read-depth-grid \
  logs/results/truncprobe-run2026100[567]-*.jsonl
```
