# as-metadata (formerly asn-info)

> **📢 Heads up:** This repo has been upgraded! 
> Now includes a new **JSON format** with full country names and origin tracking, plus country codes in CSV. 
> The repo has been renamed to `as-metadata` to reflect the richer dataset. 
> Check out [MIGRATION.md](MIGRATION.md) for the quick migration steps (most users just need to update URLs).

## 🔍 Try it online

Explore AS metadata interactively at **[Lens by ipverse](https://lens.ipverse.net)** — search IP addresses, prefixes, and autonomous systems without downloading anything.

## Overview

A comprehensive dataset of autonomous system metadata for all assigned ASNs (autonomous system numbers). 
Includes handle, organization name, and country code sourced from regional internet registries (RIR). 
Updated automatically when source data changes (checked daily).

Perfect for offline lookups, network analysis, threat intelligence, or any project where you need to map ASNs to organizations—no API rate limits, no external dependencies.

## Update notes

- **2026-01-27**: Added `providerAsns` field with list of upstream transit provider ASNs
- **2026-01-18**: **Breaking change:** Replaced `upstreams`/`downstreams` with `providers`/`customers`/`peers` to accurately distinguish transit relationships from peering. Added `degree` and `reach` fields.
- **2026-01-08**: Added `registered` field (RIR registration date), `stats` section (prefix and connectivity statistics), and moved `lastAnnounced` to top level.
- **2026-01-03**: Repository renamed to `as-metadata`, CSV format changed to 4 columns (added country-code), JSON format added. See [MIGRATION.md](MIGRATION.md) for details.
- **2025-08-03**: Removed opinionated handle cleanup and removed quotes around descriptions to improve RFC4180 compliance
- **2023-09-03**: Removed PEM certificates from description field

## Available formats

JSON (~55-60 MB) and CSV (~6 MB)

**JSON format:**
```json
[
  {
    "asn": 4711,
    "metadata": {
      "handle": "INTEC",
      "description": "INTEC Inc.",
      "countryCode": "JP",
      "country": "Japan",
      "origin": "authoritative",
      "registered": "1997-03-14T00:00:00Z"
    },
    "stats": {
      "ipv4": {
        "prefixes": 12,
        "prefixesAggregated": 8,
        "largestPrefix": 20
      },
      "ipv6": {
        "prefixes": 3,
        "prefixesAggregated": 2,
        "largestPrefix": 32
      },
      "connectivity": {
        "providers": 2,
        "providerAsns": [174, 3356],
        "customers": 5,
        "peers": 3,
        "degree": 10,
        "reach": 12
      }
    },
    "lastAnnounced": "2026-01-04T11:40:34.965574Z"
  },
  {
    "asn": 4712,
    "metadata": {
      "handle": "JT-NET",
      "description": "JAPAN TOBACCO INC.",
      "countryCode": "JP",
      "country": "Japan",
      "origin": "authoritative",
      "registered": "1997-03-14T00:00:00Z"
    },
    "stats": null,
    "lastAnnounced": null
  }
]
```

**CSV format:**
```csv
asn,handle,description,country-code
0,IANA-RSVD-0,Internet Assigned Numbers Authority,US
1,LVLT-1,Level 3 Parent LLC,US
2,UDEL-DCN,University of Delaware,US
3,MIT-GATEWAYS,Massachusetts Institute of Technology,US
4,ISI-AS,University of Southern California,US
5,SYMBOLICS,WFA Group LLC,US
6,BULL-HN,ATOS IT Solutions and Services Inc.,US
7,DSTL,The Defence Science and Technology Laboratory,GB
.
.
.
```

## Field descriptions

### Common fields (JSON and CSV)

- **asn**: Autonomous System Number
- **handle**: Registry handle/identifier
- **description**: Organization name or description
- **country-code** (CSV): ISO 3166-1 alpha-2 country code (XX if unknown)
- **countryCode** (JSON): ISO 3166-1 alpha-2 country code

### JSON-only fields

- **country**: Full country name
- **origin**: Metadata source indicator
  - `authoritative`: From authoritative source
  - `inferred`: Inferred from routing information; may be inaccurate
  - `overlaid`: Metadata overlay from [as-overlay](https://github.com/ipverse/as-overlay) applied
  - `none`: No metadata available
- **registered**: RIR registration date (time normalized to 00:00:00Z); `null` for inferred ASNs
- **stats**: Prefix and connectivity statistics; `null` for ASNs without route collector data
  - **stats.ipv4.prefixes**: Number of IPv4 prefixes announced
  - **stats.ipv4.prefixesAggregated**: Number of IPv4 prefixes after aggregation
  - **stats.ipv4.largestPrefix**: Largest IPv4 prefix announced (e.g., /13 — smaller number = larger block)
  - **stats.ipv6.prefixes**: Number of IPv6 prefixes announced
  - **stats.ipv6.prefixesAggregated**: Number of IPv6 prefixes after aggregation
  - **stats.ipv6.largestPrefix**: Largest IPv6 prefix announced (e.g., /29 — smaller number = larger block)
  - **stats.connectivity.providers**: Number of transit provider ASNs
  - **stats.connectivity.providerAsns**: List of transit provider ASNs (enables upstream quality analysis)
  - **stats.connectivity.customers**: Number of transit customer ASNs
  - **stats.connectivity.peers**: Number of settlement-free peer ASNs
  - **stats.connectivity.degree**: Total unique neighbor ASNs (providers + customers + peers)
  - **stats.connectivity.reach**: Customer cone size (ASNs reachable via customer relationships)
- **lastAnnounced**: ISO 8601 timestamp when AS was last seen announcing prefixes; `null` if never seen

## How to use

Download the data directly:

**JSON:**
```bash
curl -O https://raw.githubusercontent.com/ipverse/as-metadata/master/as.json
```

**CSV:**
```bash
curl -O https://raw.githubusercontent.com/ipverse/as-metadata/master/as.csv
```

Or just clone the repo if that's your thing.

**Quick example (Python):**
```python
import json
with open('as.json') as f:
    data = {entry['asn']: entry for entry in json.load(f)}
print(data[4711]['metadata']['description'])  # INTEC Inc.
```

## Use cases
- Figure out who owns an ASN
- Enrich your IP intelligence tools
- Threat hunting and security research
- BGP analysis and network research
- Building dashboards or monitoring tools
- Offline lookups (no API rate limits to deal with)
- Pretty much anything where you need to map ASNs to operators

## Related projects

- **[as-overlay](https://github.com/ipverse/as-overlay)**: Autonomous system metadata overlays that supplement and enhance the authoritative data in this repository. When overlay data is applied, entries will have an `origin` value of `overlaid` in the JSON format.

## Questions or issues?

Head over to the [feedback repository](https://github.com/ipverse/feedback) if you have questions, issues, or suggestions.

## License

This data is released under [CC0 1.0 Universal](LICENSE).
