# Real homepages: how old are the answers?

One run on 2 Nov 2026. We picked 90 real homepages that change often. We asked four vendors three
questions about each page:

- `warmup`: the normal address, asked first.
- `plain`: the normal address again, 20 minutes later.
- `tagged`: the address with an extra tag added, asked at the same moment as `plain`. No vendor
  can have a saved copy of the tagged address, so it must download the page fresh.

We downloaded the page ourselves just before and just after, and compared each answer with those
downloads.

The sites are not named. Each site is a random ID (`site-001` to `site-090`) with a rough category.
There is no address, no page text and no answer text.

## Files

| File | One row is | What it holds |
|---|---|---|
| `logs/public-homepage/sites.csv` | A site | Its category. Its caching-header group (`Cache-Control`) on our last visit, and whether that changed during our 24-hour watch |
| `logs/public-homepage/questions.csv` | A site, vendor and question | When the question was sent. For 8 pages, OpenAI and xAI were asked again later (`sitting` = `redo`), after our OpenRouter credit ran out. Only the later sitting is listed for those |
| `logs/public-homepage/outcomes.csv` | A site and vendor | The outcome. Each of the `plain` and `tagged` answers either matches our downloads or does not. `stale`: only the tagged answer matches, so the plain answer came from an old copy. `chance mismatch`: only the plain answer matches. `both match` and `neither matches` mean what they say. If either answer was an error or empty, `status` says so and `outcome` is blank. `compared_without_spaces` is true where spaces were ignored in the comparison |
| `logs/public-homepage/anthropic-copies.csv` | A site and Anthropic question | When Anthropic fetched its copy (`retrieved_at`), how old the copy was, Anthropic's fetch result or error code, and how much of its copy appears in our download |
| `logs/public-homepage/selection-counts.csv` | A selection step | How 776 watched sites became the 90 asked pages |

**Category** comes from Cloudflare URL Scanner's labels for the exact address asked, grouped as:

- news: News & Media
- entertainment: Entertainment, Video Streaming, Sports, Gaming, Cartoons & Anime, Comic Books,
  Hobbies & Interests
- shopping: Shopping & Auctions, Ecommerce, Auctions & Marketplaces, Shopping
- technology: Technology, Shareware/Freeware, Artificial Intelligence
- other: any other label
- unknown: no label

A site with several labels takes the first group in this list.

## Which file gives which paper result

| Paper result | Files |
|---|---|
| Main table: old copies against chance mismatches, per vendor | `outcomes.csv` |
| Anthropic's copy age, reuse and sharing tables | `anthropic-copies.csv` |
| Results split by caching header | `sites.csv` with `outcomes.csv` |
| How the sites were chosen | `selection-counts.csv` |

These tables are the output of `publicPageHomepage_score_table.py` and
`publicPageHomepage_score_anthropicCopies.py`. Those scripts need the answers and page text, which
are not shared, so they cannot be rerun on this data.
