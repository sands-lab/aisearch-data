# Document type: which file types does each vendor read?

The same depth page served as 8 file types (`/depth/<type>/`: html, txt, md, json, xml, csv, pdf,
docx), asked of OpenAI, Anthropic and xAI.

| Part | Runs | Date (2026) | Question wording |
|---|---|---|---|
| Label test: the same bytes under one declared Content-Type each (`/depth/declaredType/<label>/`, 2 KB) | `run20261006-174712-kfnvw` (text/plain), `-174854-haa2b` (text/html), `-175048-emrwe` (text/markdown), `-175227-r6k5g` (application/xml), `-175407-ejdjg` (text/csv) | 6 Oct | old |
| Main source: 8 types, 4 KB, 3 tries per vendor | `run20261006-153152-a53j9` (txt), `-153657-maa2d` (html), `-154211-ujfip` (md), `-154711-o2ij3` (json), `-155220-ihqea` (xml), `-155720-uotxd` (csv), `-160227-xqpor` (pdf), `-160808-beg8u` (docx) | 6 Oct | old |
| Repeat on origin A: 8 types, 4 KB | `run20261101-150106-zazkt` to `run20261101-151323-dpxgw` (8 runs) | 1 Nov | new (address + question) |
| Repeat on origin B: 8 types, 4 KB | `run20261101-152027-49of8` to `run20261101-153147-siyxo` (8 runs) | 1 Nov | new |

The result is the same in every part: OpenAI reads txt, html, json and pdf and refuses md, xml, csv
and docx; Anthropic and xAI read all 8.

## Which file feeds what

| File | Feeds |
|---|---|
| `logs/results/truncprobe-<run id>.jsonl` | Every call, with the depth codes each answer quoted. The paper's file-type table and the label-test table were made by hand from these. No figure |
| `logs/newprompt-originA-20261101-150106.log`, `logs/newprompt-originB-20261101-152027.log` | Printed output of the 1 Nov repeat |
| `logs/raw-replies.jsonl`, the 1 Nov lines | Whole replies (kept from 30 Oct on, so the 6 Oct runs have none) |
| `logs/probe.jsonl`, `logs/probe-vps.jsonl`, lines on `/depth/<type>/` and `/depth/declaredType/` | Every download |
