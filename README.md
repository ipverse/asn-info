# as-metadata (formerly asn-info)

> **📢 Heads up:** This repo has been upgraded! 
> Now includes a new **JSON format** with full country names and origin tracking, plus country codes in CSV. 
> The repo has been renamed to `as-metadata` to reflect the richer dataset. 
> Check out [MIGRATION.md](MIGRATION.md) for the quick migration steps (most users just need to update URLs). 

A comprehensive dataset of autonomous system metadata for all assigned ASNs (autonomous system numbers). 
Includes handle, organization name, and country code sourced from regional internet registries (RIR). 
Updated daily when the underlying data changes.

Perfect for offline lookups, network analysis, threat intelligence, or any project where you need to map ASNs to organizations—no API rate limits, no external dependencies.

Available formats: JSON and CSV

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
        "upstreams": 2,
        "downstreams": 5
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
  - **stats.ipv4.largestPrefix**: Shortest IPv4 prefix length (e.g., /13)
  - **stats.ipv6.prefixes**: Number of IPv6 prefixes announced
  - **stats.ipv6.prefixesAggregated**: Number of IPv6 prefixes after aggregation
  - **stats.ipv6.largestPrefix**: Shortest IPv6 prefix length (e.g., /29)
  - **stats.connectivity.upstreams**: Number of upstream/provider ASNs
  - **stats.connectivity.downstreams**: Number of downstream/customer ASNs
- **lastAnnounced**: ISO 8601 timestamp when AS was last seen announcing prefixes; `null` if never seen

## Update notes

- **2026-01-08**: Added `registered` field (RIR registration date), `stats` section (prefix and connectivity statistics), and moved `lastAnnounced` to top level.
- **2026-01-03**: Repository renamed to `as-metadata`, CSV format changed to 4 columns (added country-code), JSON format added. See [MIGRATION.md](MIGRATION.md) for details.
- 2025-08-03: Removed opinionated handle cleanup and removed quotes around descriptions to improve RFC4180 compliance
- 2023-09-03: Removed PEM certificates from description field

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
