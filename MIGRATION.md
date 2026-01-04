# Migration guide

This repository was renamed from **asn-info** to **as-metadata**.

## Migration steps

1. Update repository references from `ipverse/asn-info` to `ipverse/as-metadata` (git remote, download URLs, etc.)
2. Update CSV parsing to handle the new 4th column (`country-code`) - you can ignore it if you don't need it
3. Optionally, switch to the new JSON format for richer metadata including full country names and origin tracking

## What's changing

### Repository name
- Old: `ipverse/asn-info`
- New: `ipverse/as-metadata`

### File formats

**as.csv**:

Old format (3 columns):
```csv
asn,handle,description
1,LVLT-1,Level 3 Parent LLC
2,UDEL-DCN,University of Delaware
```

New format (4 columns, added country-code):
```csv
asn,handle,description,country-code
1,LVLT-1,Level 3 Parent LLC,US
2,UDEL-DCN,University of Delaware,US
```

**as.json** - New file (previously not available):
```json
[
  {
    "asn": 1,
    "metadata": {
      "handle": "LVLT-1",
      "description": "Level 3 Parent LLC",
      "countryCode": "US",
      "country": "United States",
      "origin": "authoritative",
      "lastAnnounced": "2026-01-04T07:48:56.025859Z"
    }
  }
]
```

### New fields

- **country-code** (CSV) / **countryCode** (JSON): ISO 3166-1 alpha-2 country code (XX if unknown in CSV)
- **origin** (JSON only): Metadata source indicator
  - `authoritative`: From authoritative source
  - `inferred`: Inferred from routing information; may be inaccurate
  - `overlaid`: Overlay from [as-overlay](https://github.com/ipverse/as-overlay) applied
  - `none`: No metadata available
- **lastAnnounced** (JSON only): ISO 8601 timestamp (UTC) when the AS was last seen announcing prefixes (may be `null` for inactive ASNs)

### URL changes

**Old:**
```
https://raw.githubusercontent.com/ipverse/asn-info/master/as.csv
```

**New:**
```
https://raw.githubusercontent.com/ipverse/as-metadata/master/as.csv
https://raw.githubusercontent.com/ipverse/as-metadata/master/as.json
```