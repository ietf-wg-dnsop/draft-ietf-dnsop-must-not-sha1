---
title: "Deprecating the use of SHA-1 in DNSSEC signature algorithms"
abbrev: MUST NOT DNSSEC with SHA-1
docname: draft-ietf-dnsop-must-not-sha1-06
category: std
ipr: trust200902
stream: IETF
updates: 4034, 5155

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
  RFC3110:
  RFC3174:
  RFC4034:
  RFC5155:
  RFC8174:
  RFC9499:
  RFC9364:
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

  draft-ietf-dnsop-algorithm-update:
    author: 
      name: Hardaker, W.
      name: Kumari, W.
    target: https://datatracker.ietf.org/doc/html/draft-ietf-dnsop-algorithm-update
    title: Algorithm Implementation Requirements and Usage Guidance for DNSSEC

informative:


--- abstract

This document deprecates the use of the RSASHA1 and RSASHA1-NSEC3-SHA1
algorithms for the creation of DNS Public Key (DNSKEY) and Resource
Record Signature (RRSIG) records.

It updates RFC4034 and RFC5155 as it deprecates the use of these algorithms.

--- middle

# Introduction

The security of the protection provided by the SHA-1 algorithm {{RFC3174}} has been slowly diminishing
over time as various forms of attacks have weakened its cryptographic
underpinning.  DNSSEC {{RFC9364}} originally {{RFC3110}} made extensive use
of SHA-1 as a
cryptographic hash algorithm in RRSIG and Delegation Signer (DS)
records, for example.  Since then, multiple other algorithms with
stronger cryptographic strength have become widely available for DS records 
and for Resource Record Signature (DNSKEY) and DNS Public Key (RRSIG) records. 
Operators are encouraged to consider switching to one of the recommended algorithms 
listed in the {{DNSKEY-IANA}} and {{DS-IANA}} tables, respectively.
Further, support for validating SHA-1 based signatures has been
removed from some systems. As a result, SHA-1 is no longer fully interoperable
in the context of DNSSEC. As adequate alternatives exist, the use of SHA-1 is
no longer advisable.

This document thus further deprecates the use of RSASHA1 and
RSASHA1-NSEC3-SHA1 for DNS Security Algorithms.

## Requirements notation

   The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT",
   "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY",
   and "OPTIONAL" in this document are to be interpreted as described
   in BCP 14 {{RFC2119}} {{RFC8174}} when, and only when, they appear
   in all capitals, as shown here.

# Deprecating RSASHA1 and RSASHA1-NSEC3-SHA1 algorithms in DNSSEC

The RSASHA1 {{RFC4034}} and RSASHA1-NSEC3-SHA1 {{RFC5155}} algorithms
MUST NOT be used when creating DNSKEY and RRSIG records.

Validating resolver implementations ({{RFC9499}} section 10) 
MUST continue to support
validation using these algorithms as they are diminishing in use but
still actively in use for some domains as of this publication.
Because of RSASHA1 and RSASHA1-NSEC3-SHA1's non-zero use, deployed
validating resolvers MAY be configured to continue to validate RRSIG
records that use these algorithms.  Validating resolvers deployed in
more security strict environments MAY wish to treat these RRSIG
records as an unsupported algorithm.

# Security Considerations

This document deprecates the use of RSASHA1 and RSASHA1-NSEC3-SHA1
signatures since they are no longer considered to be secure.

# Operational Considerations

Zone owners currently making use of SHA-1 based algorithms should
immediately switch to algorithms with stronger cryptographic algorithms,
such as the recommended algorithms in the [DNSKEY-IANA] and [DS-IANA] tables.

# IANA Considerations

[Note to IANA, to be removed by the RFC Editor: the registry fields
listed above will be created by draft-ietf-dnsop-rfc8624-bis.]

IANA is requested to set the "Use for DNSSEC Delegation" field of the
"Digest Algorithms" registry {{DS-IANA}} {{draft-ietf-dnsop-algorithm-update}} 
for SHA-1 (1) to MUST NOT.

IANA is requested to set the "Use for DNSSEC Signing" column of the
DNS Security Algorithm Numbers registry {{DNSKEY-IANA}}
{{draft-ietf-dnsop-algorithm-update}} to MUST NOT
for the RSASHA1 (5) and RSASHA1-NSEC3-SHA1 (7) algorithms.

All other columns should remain as currently specified.

--- back

# Acknowledgments

The authors appreciate the comments and suggestions from the following
IETF participants in helping produce this document: Mark Andrews,
Steve Crocker, Peter Dickson, Thomas Graf, Paul Hoffman, Russ Housley, Shumon
Huque, Barry Leiba, S Moonesamy, Yoav Nir, Florian Obser, Peter
Thomassen, Stefan Ubbink, Paul Wouters, Tim Wicinski, and the many
members of the DNSOP working group that discussed this draft.


# Current algorithm usage levels

The DNSSEC scanning project by Viktor Dukhovni and Wes Hardaker
highlights the current deployment of various algorithms on the
https://stats.dnssec-tools.org/ website.

<RFC Editor: please delete this section upon publication>

# Github Version of this document

While this document is under development, it can be viewed, tracked,
fill here:

https://github.com/hardaker/draft-hardaker-dnsop-must-not-sha1

<RFC Editor: please delete this section upon publication>
