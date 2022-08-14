# ipverse-asn-info

A list of autonomous systems with their AS number (ASN), AS name and description ordered by ASN. The data is available in CSV format:
```
asn,handle,description
0,IANA-RSVD,"Internet Assigned Numbers Authority"
1,LVLT,"Level 3 Parent, LLC"
2,UDEL-DCN,"University of Delaware"
3,MIT-GATEWAYS,"Massachusetts Institute of Technology"
4,ISI,"University of Southern California"
5,SYMBOLICS,"WFA Group LLC"
6,BULL-HN,"ATOS IT Solutions and Services, Inc."
7,DSTL,"The Defence Science and Technology Laboratory"
.
.
.
```

This repository is updated daily.

## Use cases
- Find out more about a specific ASN (autonomous system number), use it in your own software project for bulk/offline use
- OSINT/CTI Cyber Threat Intelligence

## How to use

```$ curl -O https://raw.githubusercontent.com/ipverse/asn-info/master/as.csv```
