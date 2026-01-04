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
      "lastAnnounced": "2026-01-04T07:48:56.025859Z"
    }
  },
  {
    "asn": 4712,
    "metadata": {
      "handle": "JT-NET",
      "description": "JAPAN TOBACCO INC.",
      "countryCode": "JP",
      "country": "Japan",
      "origin": "authoritative",
      "lastAnnounced": null
    }
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
- **lastAnnounced**: ISO 8601 timestamp (UTC) when the AS was last seen announcing prefixes (may be `null` for inactive ASNs)

## Update notes

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
