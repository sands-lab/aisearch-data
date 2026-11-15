# Document type: which file types does each vendor read?

The same depth page is served as 8 file types at `/depth/<type>/`: html, txt, md, json, xml, csv,
pdf and docx. We ask OpenAI, Anthropic and xAI about each one.

The result is the same in every part below. OpenAI reads txt, html, json and pdf, and refuses md,
xml, csv and docx. Anthropic and xAI read all 8.

| Part | Run ids | Date (2026) | Question wording |
|---|---|---|---|
| Label test: the same text, sent with a different declared type each time (`/depth/declaredType/<label>/`, 2 KB) | `run20261006-174712-kfnvw` (text/plain), `-174854-haa2b` (text/html), `-175048-emrwe` (text/markdown), `-175227-r6k5g` (application/xml), `-175407-ejdjg` (text/csv) | 6 Oct | old |
| Main test: 8 types, 4 KB, 3 tries per vendor | `run20261006-153152-a53j9` (txt), `-153657-maa2d` (html), `-154211-ujfip` (md), `-154711-o2ij3` (json), `-155220-ihqea` (xml), `-155720-uotxd` (csv), `-160227-xqpor` (pdf), `-160808-beg8u` (docx) | 6 Oct | old |
| Repeat on origin A: 8 types, 4 KB | `run20261101-150106-zazkt` to `run20261101-151323-dpxgw` (8 runs) | 1 Nov | new |
| Repeat on origin B: 8 types, 4 KB | `run20261101-152027-49of8` to `run20261101-153147-siyxo` (8 runs) | 1 Nov | new |

A short run id like `-174854-haa2b` has the same date as the one before it.

## Files

| File | What it holds |
|---|---|
| `logs/results/truncprobe-<run id>.jsonl` | Every call, with the codes each answer quoted. The paper's file-type table and label-test table were made by hand from these |
| `logs/newprompt-originA-20261101-150106.log`, `logs/newprompt-originB-20261101-152027.log` | Printed output of the 1 Nov repeats |
| `logs/raw-replies.jsonl`, the 1 Nov lines | Whole replies for the repeats. The 6 Oct runs have none |
| `logs/probe.jsonl`, `logs/probe-vps.jsonl`, lines on `/depth/<type>/` and `/depth/declaredType/` | Every vendor download |

There is no figure for this experiment.
