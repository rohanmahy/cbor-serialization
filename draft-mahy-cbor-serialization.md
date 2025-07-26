---
title: "Clarifying Serialization options in the Common Binary Object Representation (CBOR)"
abbrev: "CBOR Serialization"
category: info

docname: draft-mahy-cbor-serialization-latest
submissiontype: IETF  # also: "independent", "editorial", "IAB", or "IRTF"
number:
date:
consensus: true
v: 3
area: AREA
workgroup: WG Working Group
keyword:
 - cbor
 - cde
 - deterministic encoding
 - serialization
 - serialisation
venue:
  group: WG
  type: Working Group
  mail: WG@example.com
  arch: https://example.com/WG
  github: USER/REPO
  latest: https://example.com/LATEST

author:
 -
    fullname: Rohan Mahy
    organization:
    email: rohan.ietf@gmail.com

normative:

informative:

...

--- abstract

This document clarifies the serialization options defined in the CBOR specification and presents them in a concise way.

--- middle

# Introduction

The serialization options for CBOR have been a source of confusion both among implementers and inside the IETF community.
Some reasons for this confusion include the following.

- Map ordering recommendations changed between {{?RFC7049}} and {{!RFC8949}}.
- The non-normative nature of some of the guidance.
- Ambiguous language such as "preferred" used inside descriptions in the serializations.
- A large number of terms, some of which share the same initialisms (ex: common deterministic encoding, CBOR deterministic encoding) or include the name of one of the serializations.
- the verbosity of the descriptions

# Conventions and Definitions

{::boilerplate bcp14-tagged}

# Existing CBOR Serializations

The following CBOR serialization are defined in {{!RFC8949}}. Their definitions are clarified here. 

CBOR defines three specific serializations: common, basic. These build on each 

## Common Serialization

- integers are always expressed using the smallest size representation possible.
- integers smaller than 2^xx MUST NOT be expressed as bigints. use the corresponding integer types instead.
- 

## Basic Serialization


- indefinite encoding is forbidden

## Ordered Serialization

This was formally called "Deterministic Encoding". This is confusing as the community often described all three serializations collectively as deterministic encoding. 

- CBOR maps are sorted lexicographically by the CBOR serilization of their map keys. See Section 4.2.1 of {{!RFC8949}}.



# Security Considerations

TODO Security


# IANA Considerations

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.
