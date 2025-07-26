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
area: "Applications and Real-Time"
workgroup: "Concise Binary Object Representation Maintenance and Extensions"
keyword:
 - cbor
 - cde
 - deterministic encoding
 - serialization
 - serialisation
venue:
  group: "Concise Binary Object Representation Maintenance and Extensions"
  type: "Working Group"
  mail: "cbor@ietf.org"
  arch: "https://www.ietf.org/mail-archive/web/cbor/current/maillist.html"
  github: "rohanmahy/cbor-serialization"
  latest: "https://rohanmahy.github.io/cbor-serialization/draft-mahy-cbor-serialization.html"

author:
 -
    fullname: Rohan Mahy
    email: rohan.ietf@gmail.com

normative:

informative:



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

- integers and tags are always expressed using the smallest size representation possible.
- integers smaller than 2^xx MUST NOT be expressed as bigints. use the corresponding integer types instead.
- the major byte for definite-length byte strings, text strings, arrays, and maps is always expressed using the smallest number of bytes that can represent that length.
- floating point values are expressed using smallest of the three sizes (16-bits, 32-bits, or 64-bits) which can represent that value.
- Unlike for integers, common serialization does not place any restriction on the expression of bigfloats or bigfractions.
- floating point numbers which are mathematically integers (ex: 5.0 or -3.0) are  expressed as floating point numbers.
- Floating point negative zero (-0.0) is distinct from floating point positive zero (0.0)
- Floating point NaN values with payloads are distinct from one another.


## Basic Serialization

Basic serialization did not exist in {{!RFC8949}}. It includes all the requirements of Common serialization and adds one more.

- indefinite encoding is forbidden

## Ordered Serialization

This was formally called "Deterministic Encoding" (which was confusing as the community often described any of these three serializations, and occasionally application-defined proffiles, collectively as CBOR Deterministic Encoding or CDE).

Ordered Serialization includes all the requirements of Basic Serialization and adds one additional requirements.

- CBOR maps are sorted by lexicographically by the ordered CBOR serialization of their map keys. See Section 4.2.1 of {{!RFC8949}}.

> Note that a CBOR map key can be another map key. Therefore, to use ordered serialization, a CBOR map key must be (recursively) represented using Ordered Serialization.

# Application-specific Serialization Profiles

Applications can define their own serialization rules, which may build from any of the three concrete serializations defined in this document, or from none of them.


# Security Considerations

TODO Security


# IANA Considerations

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.
