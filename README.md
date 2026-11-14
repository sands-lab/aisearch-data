# Data for the aisearch-probe study

This repo holds the data behind the paper's numbers, figures and tables. The code that collected
it and draws the figures is in the companion code repo, `aisearch-probe`.

Licence: CC-BY 4.0 (see `LICENSE`). You may reuse the data, including commercially, if you credit
the source.

## How to use it

The files keep the folder layout the scripts expect. Put this repo's `logs/` folder next to the
code (copy it or link it) and run the scripts from the code repo's top folder.

One page per experiment, in `experiments/`, says which file feeds which figure or table:

| Experiment | Page |
|---|---|
| A page changes at the same address: when do vendors see the new version? | `experiments/correction.md` |
| A page fails: how do vendors retry? | `experiments/fault-recovery.md` |
| A failed page is fixed: when do vendors see the fix? | `experiments/heal-time.md` |
| Does a vendor hand one caller's stored copy to another caller (API)? | `experiments/sharing-api.md` |
| The same, in the chat apps | `experiments/sharing-web-apps.md` |
| Does a vendor follow the page's caching headers? | `experiments/cache-headers.md` |
| Which file types does each vendor read? | `experiments/document-type.md` |
| How far into a long page does each vendor read, and what does it cost? | `experiments/read-depth.md` |
| Anthropic's filtering step: what does it cost? | `experiments/dynamic-filtering.md` |
| Does a vendor see text added by JavaScript? | `experiments/javascript.md` |
| Public endpoints whose value only goes up: how old are the answers? | `experiments/public-endpoints.md` |
| Real homepages: how old are the answers? | `experiments/public-homepages.md` |
| Real XML files, feeds and llms.txt: which ones does each vendor read? | `experiments/public-xml-files.md` |

All times in the data are UTC unless a field says otherwise.

## What was changed from the raw records

The data comes from filtered copies of the raw records. These changes apply everywhere:

- **Our two test servers are renamed.** Their domains became `origin-a.example` and
  `origin-b.example` in every address, question, answer and whole reply. When a model wrote the bare
  name without the ending, it became `origin-a` or `origin-b`.
- **Page addresses use the released code's names.** The old names were swapped for the new ones
  everywhere, including inside model answers. Nothing numeric changes: page codes do not depend on
  the address text.

  | Old address in the raw records | Address in this data |
  |---|---|
  | `/depthhtmlpage/`, `/depthtxtpage/`, `/depthmdpage/`, `/depthjsonpage/`, `/depthxmlpage/`, `/depthcsvpage/`, `/depthpdfpage/`, `/depthdocxpage/` | `/depth/html/`, `/depth/txt/`, `/depth/md/`, `/depth/json/`, `/depth/xml/`, `/depth/csv/`, `/depth/pdf/`, `/depth/docx/` |
  | `/depthctpage/<label>/` | `/depth/declaredType/<label>/` |
  | `/depthjsinlinepage/`, `/depthjsextpage/`, `/depthjsfile/`, `/depthjsdatapage/`, `/depthjsldpage/` | `/depth/jsInline/`, `/depth/jsExternal/`, `/depth/jsExternalScript/`, `/depth/jsData/`, `/depth/jsonLd/` |
  | `/ccdepthpage/` | `/cacheHeaders/` |
  | `/verhtmlpage/`, `/vertxtpage/`, `POST /control/version` | `/correction/html/`, `/correction/txt/`, `POST /control/correction` |
  | `/healpage/` | `/heal/` |
  | `/fault/<kind>` | unchanged |

- **Server logs hold vendor visits only.** A line is kept if it is a request for a kept run's page
  (the run id is in the address), or a request that came from such a page (for example a fetcher
  asking for `/favicon.ico` right after reading the page). Lines from our own machines are dropped:
  our own check tags (`probe-liveness`, `probe-selfcheck`, `probe-retention`) and our own network
  addresses. Every other visitor stays, including fetchers that use a plain browser name (xAI's
  does). Crawler addresses stay: they are public cloud ranges and let anyone check a crawler's
  identity.
- **Encrypted blocks are removed from whole replies.** Some vendors return reasoning or signature
  blocks that are encrypted. They cannot be read and feed no result, and they might hold personal
  information from before encryption, so they are left out.
- **Run output lost its first line.** Each run printed which credentials it had loaded (names
  only, never values). Those lines are removed.
- **One account link was removed.** An OpenRouter error message held a link to our account
  workspace. It now reads `openrouter.ai/workspaces/<workspace>/keys/<key>`.
- **The test page's filler text was edited in one place.** The depth page is padded with text
  copied from our own project notes. Those notes named the temporary tunnel host we first used.
  Where models quote that text, or a whole reply carries the fetched page, the host now reads
  `tunnel.example`.
- **Real sites are IDs.** In the homepage and XML file tests, every site and file is a neutral ID
  (`site-017`, `file-042`). There are no addresses and no page or file text. The real lists stay
  private.

## Allowed matches in the clean-up search

Before release, every file was searched for our names, places and addresses, for email
addresses, and for the real site names. These matches are allowed, because they come from
the vendors and say nothing about us or about which sites were tested:

- `claude-user@anthropic.com`: part of Anthropic's public crawler name.
- One Anthropic message id, which holds three letters from the search list by chance.
- `archive.org`, `facebook.com`, `www.google.com`, `cloud.google.com`, `grok.com`, `note.com`:
  a crawler's name (Meta's points to `developers.facebook.com`), a "came from" field, and pages
  that models cited or suggested. They are also on the watched-site list, which is why the
  search finds them.
