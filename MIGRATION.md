# Migration guide

This repository was renamed from **asn-info** to **as-metadata**.

## Migration steps

1. If only consuming raw text files: just update the download URL, no code changes needed
2. Update repository URLs in your code from `ipverse/asn-info` to `ipverse/as-metadata`
3. If parsing CSV: handle the new country-code column (4th column)
4. Consider using the new JSON format for richer metadata including origin tracking

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
      "origin": "authoritative"
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