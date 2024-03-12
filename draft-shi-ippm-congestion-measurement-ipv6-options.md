---
stand_alone: true
category: std
submissionType: IETF
ipr: trust200902
lang: en

title: IPv6 Options for Congestion Measurement
abbrev: CM
docname: draft-shi-ippm-congestion-measurement-ipv6-options-latest
obsoletes:
updates:
# date: 2022-02-02 -- date is filled in automatically by xml2rfc if not given

area: "Operations and Management"
workgroup: "IP Performance Measurement"

kw:
  - Congestion Measurement
  - IPv6

author:
 -
  ins: H. Shi
  name: Hang Shi
  organization: Huawei
  email: shihang9@huawei.com
  role: editor
  city: Beijing
  country: China
 -
  ins: T. Zhou
  name: Tianran Zhou
  organization: Huawei
  city: Beijing
  country: China
  email: zhoutianran@huawei.com
 -
  ins: Y. Liu
  name: Ying Liu
  organization: China Unicom
  city: Beijing
  country: China
  email: liuy619@chinaunicom.cn
 -
  ins: M. Han
  name: Mengyao Han
  organization: China Unicom
  city: Beijing
  country: China
  email: hanmy12@chinaunicom.cn


informative:


--- abstract

The Congestion Measurement enables precise congestion control, aids in effective load balancing, and simplifies network debugging by accurately reflecting the degree of congestion across network paths. This document outlines how Congestion Measurement Data-Fields are encapsulated in IPv6.

--- middle

# Introduction {#intro}

{{?I-D.draft-shi-ippm-congestion-measurement-data}} defines data fields of Congestion Measurement which enables sender to obtain the degree of congestion across the path. This document defines the IPv6 encapsulation of the Congestion Measurement Data-Fields.

## Requirements Language

{::boilerplate bcp14-tagged}

# Congestion Measurement Option {#option}

One IPv6 header option, Congestion Measurement Option is defined to carry the Congestion Measurement Data-Fields.

~~~
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
                                +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
                                |Opt Type = TBD1|  Opt Data Len |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                                                               |
.                                                               .
.        Congestion Measurement Data-Fields (Variable)          .
.                                                               .
|                                                               |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
~~~
{: #CM-procedure title="Congestion Measurement Option"}

where:

- Opt Type: Type value is TBD1, an 8-bit unsigned integer. Identifier of the type of this Congestion Measurement Option.
- Opt Data Len: An 8-bit unsigned integer. Length of the Option Data field of this option, that is, length of the Congestion Measurement Data-Fields.
- Congestion Measurement Data-Fields: Option-Type-specific data. It carries the data fields for Congestion Measurement as specified in {{?I-D.draft-shi-ippm-congestion-measurement-data}}.

## Congestion Measurement Hop-by-hop Options Header (HBH)

The Congestion Measurement option can be carried in the IPv6 Hop-by-Hop Options Header. In this case, each node along the path can inspect the Congestion Info Data field if they are configured the support this option. If the U bit of Congestion Measurement Data-Fields is set, intermediate nodes will modify the Congestion Info Data field accordingly.In theory, the presence of the Hop-by-Hop Option should not affect the traffic throughput both on nodes that do not recognize this Option and on the nodes that support it. However, in a real implementation, a packet with a Hop-by-hop Option may be skipped or processed in the slow path. Proposals to mitigate the problem are out of the scope for this document.

## Congestion Measurement Destination Options Header (DOH)

The Congestion Measurement option can be carried in the IPv6 Destination Options Header. In this case, it is usually processed by the destination node. Note that, if there is also a Routing Header (RH), any visited destination in the route list can process it. If the U bit of Congestion Measurement Data-Fields is set, intermediate nodes will modify the Congestion Info Data field accordingly.

# Security Considerations

TBD.

# IANA Considerations

IANA is requested to assign an IPv6 Header Option as follows:

| Value | Description | Reference |
|-------|-------------|-----------|
| TBD1  | Congestion Measurement Option | {{option}} |
