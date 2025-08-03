# ipverse-asn-info

A list of autonomous systems used in Border Gateway Protocol (BGP) routing with their AS number (ASN), AS name and description ordered by ASN. The data is available in CSV format:

```
asn,handle,description
0,IANA-RSVD-0,Internet Assigned Numbers Authority
1,LVLT-1,Level 3 Parent LLC
2,UDEL-DCN,University of Delaware
3,MIT-GATEWAYS,Massachusetts Institute of Technology
4,ISI-AS,University of Southern California
5,SYMBOLICS,WFA Group LLC
6,BULL-HN,ATOS IT Solutions and Services Inc.
7,DSTL,The Defence Science and Technology Laboratory
.
.
.
```

This repository is updated daily (if the underlying data changes).

## Update notes

- 2025-8-3: Removed opinionated handle cleanup and removed quotes around descriptions to improve RFC4180 compliance
- 2023-9-3: Removed PEM certificates from description field

## Use cases
- Find out more about a specific ASN (autonomous system number), use it in your own software project for bulk/offline use
- OSINT/CTI Cyber Threat Intelligence

## How to use

Clone the repository or download the raw data:  
```$ curl -O https://raw.githubusercontent.com/ipverse/asn-info/master/as.csv```
