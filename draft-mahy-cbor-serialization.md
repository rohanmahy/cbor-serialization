---
title: "Standard Serialization options in the Common Binary Object Representation (CBOR)"
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

This document renames and clarifies the serialization options defined in the CBOR specification and adds one additional serialization option, presenting them concisely and clearly.

--- middle

# Introduction

The CBOR specification {{!RFC8949}} allows applications to define their own profiles of CBOR, including creating their own serialization rules.
It also defines two specific serialization options ("Preferred Serialization" and "Core Deterministic Encoding") and gives a new name ("Length-First Map Key Ordering") for the serialization described in {{?RFC7049}}.

The serialization options for CBOR have been a source of confusion both among implementers and inside the IETF community.
Some reasons for this confusion include the following.

- Map ordering recommendations changed between {{?RFC7049}} and {{!RFC8949}}.
- {{!RFC8949}} mixes advice for serialization in application-defined profiles and serializations in the standard in the same section.
- The non-normative nature of some of the guidance.
- Ambiguous language such as "preferred" and "might need to" used inside descriptions of the serializations.
- A large number of terms, some of which share the same initialisms (ex: common deterministic encoding, core deterministic encoding, and CBOR deterministic encoding) or include the name of one of the serializations in the description of other serializations.
- The verbosity of the descriptions

# Conventions and Definitions

{::boilerplate bcp14-tagged}

# Recommended CBOR Serializations

This document creates new names for "Preferred Serialization" and "Core Deterministic Encoding" serializations defined in {{!RFC8949}}, and defines a third serialization.
Each of these serializations builds on the previous serialization.
These three serializations are suitable for general use and can be referenced by application profiles and other specifications.

- **Compact Serialization**: Uses the most compact size, form, or variant of every CBOR major type, and forbids bigints that can be expressed as integers.
- **Definite Serialization**: Includes the requirements of Compact Serialization, but only allows definite-length encoding.
- **Sorted Serialization**: Includes the requirements of Definite Serialization, but also sorts map keys according to Section 4.2.1 bullet point 3 of {{!RFC8949}}.

Applications may require one of these serializations or define their own (either from scratch or based on any of the standard serializations).

## Compact Serialization

The Compact Serialization option was defined in {{!RFC8949}}, where it was referred to as Preferred Serialization.

Below is a summary of the rules for Compact Serialization:

- CBOR integer and tag types are always expressed using the smallest size representation possible.
- Unsigned integers smaller than 2^64 or negative integers smaller than -(2^64 + 1) MUST NOT be expressed as bigints. They are encoded using the corresponding integer types instead.
- The byte containing the major type for definite-length byte strings, text strings, arrays, and maps is always the selected to represent the length using the smallest number of bytes possible.
- Floating point values are expressed using smallest of the three sizes (16-bits, 32-bits, or 64-bits) which can represent that value. This requirement includes using the smallest representation of NaN values.
- Floating point numbers which are mathematically integers (ex: 5.0 or -3.0) are  expressed as floating point numbers.
- Floating point negative zero (-0.0) is distinct from floating point positive zero (0.0).
- Floating point NaN values with payloads are distinct from one another.
- Unlike for integers, Compact Serialization does not place any restriction on the expression of bigfloats or decimal fractions.


## Definite Serialization

This document defines Definite Serialization, which did not exist in {{!RFC8949}}. It includes all the requirements of Compact serialization and adds one more requirement:

- Indefinite-length encoding is forbidden.

## Ordered Serialization

This was formerly called "Deterministic Encoding" (which was confusing as the community often described any of these three serializations, and occasionally application-defined profiles, collectively as CBOR Deterministic Encoding, Core Deterministic Encoding, or Common Deterministic; or using the initialism CDE).

Ordered Serialization includes all the requirements of Definite Serialization and adds one additional requirement:

- CBOR maps are sorted bytewise lexicographically by the CBOR Ordered Serialization of their map keys. See Section 4.2.1 of {{!RFC8949}} bullet point 3 for examples of correctly sorted map keys.

> Note that a CBOR map key can be another map. Therefore, to use ordered serialization, a CBOR map key which contains maps must be processed recursively and itself represented using Ordered Serialization.

# Discouraged Serializations

{{?RFC7049}} defined a form of serialization similar to Ordered Serialization, but which used a different sorting algorithm. It is now referred to as Length-First Map Key Ordering Serialization. Use of Length-First Map Key Ordering Serialization is discouraged.

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
