---
title: "Remove SHA-1 from active use within DNSSEC"
abbrev: MUST NOT DNSSEC with SHA-1
docname: draft-hardaker-dnsop-must-not-sha1-01
category: std
ipr: trust200902

stand_alone: yes
pi: [toc, sortrefs, symrefs, docmapping]

author:
  -
    ins: W. Hardaker
    name: Wes Hardaker
    org: USC/ISI
    email: ietf@hardakers.net
  -
    ins: W. Kumari
    name: Warren Kumari
    org: Google
    email: warren@kumari.net

normative:
  RFC2119:
  RFC3174:
  RFC3685:
  RFC4033:
  RFC4034:
  RFC4035:
  RFC4509:
  RFC5155:
  RFC5702:
  RFC6605:
  RFC8080:
  DNSKEY-IANA:
    author:
      name: IANA
    target: "https://www.iana.org/assignments/dns-sec-alg-numbers/dns-sec-alg-numbers.xhtml"
    title: Domain Name System Security (DNSSEC) Algorithm Numbers
  DS-IANA:
    author:
      name: IANA
    target: "http://www.iana.org/assignments/ds-rr-types"
    title: Delegation Signer (DS) Resource Record (RR) Type Digest Algorithms

informative:
  RFC8499:


--- abstract

This document retires the use of SHA-1 within DNSSEC.

--- middle

# Introduction

The security of the SHA-1 algorithm {{RFC3174}} has been slowly
diminishing over time as various forms of attacks have weakened its
cryptographic underpinning.  DNSSEC {{RFC4033}} {{RFC4034}}
{{RFC4035}} originally made extensive use of SHA-1 as a cryptographic
verification algorithm in RRSIG and Delegation Signer (DS) records,
for example.  Since then, multiple other signing algorithms with
stronger cryptographic strength are now widely available for DS
records (such as SHA-256 {{RFC4509}}, SHA-384 ({{RFC6605}})) and for
DNSKEY and RRSIG records (such as RSASHA256 ({{RFC5702}}), RSASHA512
({{RFC5702}}), ECDSAP256SHA256 {{RFC6605}}, ECDSAP384SHA384
{{RFC6605}}, ED25519 {{RFC8080}}, and ED448 {{RFC8080}}), the use of
SHA-1 is no longer needed.

This document deprecates the use of the SHA-1 algorithm for DS records
and RSASHA1 and RSASHA1-NSEC3-SHA1 for DNS Security Algorithms.

## Requirements notation

   The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT",
   "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY",
   and "OPTIONAL" in this document are to be interpreted as described
   in BCP 14 {{RFC2119}} {{?RFC8174}} when, and only when, they appear
   in all capitals, as shown here.

# Deprecating SHA-1 algorithms in DNSSEC

The SHA-1 {{RFC3685}} algorithm MUST NOT be used when creating DS records.
Validating resolvers MUST treat DS records as insecure.  If no other DS
records of accepted cryptographic algorithms are available, the DNS
records below the delegation point MUST be treated as insecure.

The RSASHA1 {{RFC4034}}, DSA-NSEC3-SHA1 {{RFC5155}}, and
RSASHA1-NSEC3-SHA1 {{RFC5155}} algorithms MUST NOT be used when
creating DNSKEY and RRSIG records.  Validating resolvers MUST treat
RRSIG records created from DNSKEY records using these algorithms as
insecure.  If no other RRSIG records of accepted cryptographic
algorithms are available, the validating resolver MUST consider the
associated resource records as Bogus.


# Security Considerations

This document increases the security of the DNSSEC ecosystem by
deprecating algorithms that make use of older algorithms with SHA-1
derived uses.

# Operational Considerations

Zone owners currently making use of SHA-1 based algorithms should
immediate switch to algorithms with stronger cryptographic strengths,
such as those listed in the introduction.  DNS registries {{?RFC8499}}
should prohibit their clients to upload and publish SHA-1 based DS
records.

# IANA Considerations

IANA is requested to set the "DNSSEC Validation" of the "Digest
Algorithms" registry {{DS-IANA}} for SHA-1 (1) to MUST NOT.

IANA is requested to set the "Recommended for DNSSEC Validation"
column of the DNS Security Algorithm Numbers registry {{DNSKEY-IANA}}
to MUST NOT:

- RSASHA1 (5)
- RSASHA1-NSEC3-SHA1 (7)

--- back

# Acknowledgments

The authors appreciate the comments and suggestions from the following
IETF participants in helping produce this document: Mark Andrews,
Peter Dickson, Peter Thomassen, Paul Wouters and the many members of
the DNSOP working group that discussed this draft.

# Current algorithm usage levels

The DNSSEC scanning project by Viktor Dukhovni and Wes Hardaker
highlights the current deployment of various algorithms on the
https://stats.dnssec-tools.org/ website.

[RFC Editor: please delete this section upon publication]

# Github Version of this document

While this document is under development, it can be viewed, tracked,
fill here:

https://github.com/hardaker/draft-hardaker-dnsop-must-not-sha1

