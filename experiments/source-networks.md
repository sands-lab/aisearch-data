# Source networks: which networks do each vendor's fetches come from?

For every request a vendor's fetcher made to one of our test pages, we looked up which network
owns the sender's address. A network is a block of internet addresses run by one organisation,
such as Google Cloud or Comcast. Its number is called an ASN. We used the free iptoasn.com table,
offline. We then sorted each network into a type, using words in its name and its own entry in
PeeringDB, a public list where networks state their type.

The counts cover every request for our tagged test pages on both origins, 31 Aug to 9 Nov 2026,
not only the runs in this data. A request counts for OpenAI or Anthropic only if it also carried
that vendor's own fetcher name. xAI's fetcher uses an ordinary browser name, so for xAI the tag in
the address is the proof. Requests from our own network are left out, and so are the chat-app
sharing runs, where a person typed the questions into the vendors' own chat apps.

| Vendor | Requests | Distinct addresses | Networks |
|---|---|---|---|
| OpenAI | 2,296 | 235 | 1 |
| Anthropic | 1,489 | 47 | 2 |
| xAI | 8,286 | 7,774 | 1,259 |

## Files

| File | One row is | What it holds |
|---|---|---|
| `logs/source-networks/per-network-counts.csv` | A vendor and network | The network's number (`asn`), owner name and country. Its type: `hosting` (data centres and cloud), `home/mobile provider`, `business` or `unclassified`. Which rule decided the type (`type_decided_by`) and PeeringDB's own label. The number of requests, and the number of distinct addresses |

Adding up `requests` and `distinct_addresses` per vendor gives the table above. No address is in
the file.

**Type rules.** The first rule that fits is used:

1. The name has a hosting word ("host", "server", "data center", "cloud", "CDN", or a known hosting
   company): `hosting`.
2. PeeringDB says "Cable/DSL/ISP" or "NSP" (carrier): `home/mobile provider`.
3. The name has a carrier word ("telecom", "cable", "mobile" and others): `home/mobile provider`.
4. PeeringDB says "Content" or "Network Services": `hosting`.
5. PeeringDB gives any other type: `business`.
6. None of the above: `unclassified`.

The type shows what kind of network an address belongs to, not who runs the device behind it.

The server logs in this data (`logs/probe.jsonl`, `logs/probe-vps.jsonl`) carry the same
network fields on every line (`source_asn`, `source_network`, `source_country`), with a random
`source_id` in place of the address. They hold only the runs in this data, so they give smaller
totals than the table.
