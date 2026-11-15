# Public endpoints: how old are the answers?

We use public web addresses that return a single number, where the number only goes up. Examples
are a blockchain's block count, or a public random-number service's pulse number. We ask each vendor
to fetch the address and return only the number. We compare it with the true number at that time,
read by us every 5 minutes. The gap shows how old the vendor's copy was. None of our own servers
are involved.

## Files

| File | What it holds |
|---|---|
| `logs/results/anchor-probe-lifetime.jsonl` | Main run, 3–6 Nov 2026. 4 vendors, up to 9 addresses, 80 rounds, one round every 45 minutes |
| `logs/results/anchor-truth-lifetime.jsonl` | The true number at each of the 9 addresses, read every 5 minutes. We use it to date the OpenAI, xAI and Google answers. It also gives the table's "Updates" column: how often each number changes |
| `logs/results/anchor-probe-anthfill.jsonl` | Anthropic only, 7–10 Nov. The 6 addresses it did not answer in the main run, plus a re-test of the NIST address. Anthropic's replies give the time it fetched its copy (`retrieved_at`) |
| `logs/results/nist-usecache.jsonl` | Anthropic, 8 Nov, 20 rounds, with `use_cache:false` (tells Anthropic not to use its saved copy) |

The NIST address sends a `no-store` header, which forbids reusing a copy. Anthropic still answers
from an old copy, but fetches a fresh one when told not to use its saved copy.

## Redraw the figure

From the code repo's top folder, with `logs/` in place:

```sh
cat logs/results/anchor-probe-lifetime.jsonl logs/results/anchor-probe-anthfill.jsonl > anchor-all.jsonl
python3 scripts/publicPageEndpoint_plot.py --answers anchor-all.jsonl --out figures/anchor-lifetime-staleness
```

The first line joins the main run with Anthropic's later run, so Anthropic's panel is complete.
Without it, the script reads only the main run.

The figure leaves out Google's answers for the USGS address. Google misread its 13-digit time value,
which is a reading mistake, not an old copy. Those answers are still in the files.
