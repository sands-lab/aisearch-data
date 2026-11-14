# Real homepages: how old are the answers?

One run on 2 Nov 2026. 90 real, often-changing homepages, four vendors, three questions each: a
warm-up (`warmup`), then 20 minutes later the normal address (`plain`) and a tagged address
(`tagged`) at the same moment. Each answer is compared with our own download of the page.

The sites are not named. Each site is a random ID (`site-001` … `site-090`) with a rough category.
There is no page text, no answer text and no address. The real site list stays private.

## Files

| File | What it holds |
|---|---|
| `logs/public-homepage/sites.csv` | Per site: category, and its Cache-Control group on the last watch visit (and whether it changed during the 24 h watch) |
| `logs/public-homepage/questions.csv` | Per site × vendor × question: when it was sent. OpenAI and xAI on 8 pages were asked again later (`sitting` = `redo`) after OpenRouter credit ran out; only the re-run is kept for those |
| `logs/public-homepage/outcomes.csv` | Per site × vendor: the outcome when the answer is compared with our own downloads only: `stale`, `chance mismatch`, `both match`, `neither matches`, or `not usable` (in `status`). `compared_without_spaces` is true for pages compared with spaces ignored |
| `logs/public-homepage/anthropic-copies.csv` | Per site × Anthropic question: Anthropic's own fetch time (`retrieved_at`), the copy's age, its fetch result or error code, and how much of its copy was found in our download |
| `logs/public-homepage/selection-counts.csv` | How 776 watched sites became 90 asked pages |

**Category:** from Cloudflare URL Scanner labels for the exact address asked, put into one group:
news (News & Media); entertainment (Entertainment, Video Streaming, Sports, Gaming, Cartoons &
Anime, Comic Books, Hobbies & Interests); shopping (Shopping & Auctions, Ecommerce, Auctions &
Marketplaces, Shopping); technology (Technology, Shareware/Freeware, Artificial Intelligence);
other (any other label). A site with several labels takes the first group in that order. A site
with no label is `unknown`.

## Which file feeds what

| Paper result | Files |
|---|---|
| Main table: stale against chance mismatch per vendor | `outcomes.csv` |
| Anthropic's copy age, reuse and share tables | `anthropic-copies.csv` |
| The Cache-Control split | `sites.csv` with `outcomes.csv` |
| The selection funnel | `selection-counts.csv` |

The scripts that made these tables (`publicPageHomepage_score_table.py`,
`publicPageHomepage_score_anthropicCopies.py`) need the private answers and page downloads, so they
cannot be rerun on this data. The tables here are their output.
