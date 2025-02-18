---
title: "Deprecating the use of SHA-1 in DNSSEC signature algorithms"
abbrev: MUST NOT DNSSEC with SHA-1
docname: draft-ietf-dnsop-must-not-sha1-02
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
  RFC3174:
  RFC4033:
  RFC4034:
  RFC4035:
  RFC4509:
  RFC5155:
  RFC5702:
  RFC6605:
  RFC8080:
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

informative:



--- abstract

This document deprecates the use of the RSASHA1 and RSASHA1-NSEC3-SHA1
algorithms for the creation of DNSKEY and RRSIG records.

It updates RFC4034 and RFC5155 as it deprecates the use of these algorithms.

--- middle

# Introduction

The security of the SHA-1 algorithm {{RFC3174}} has been slowly diminishing
over time as various forms of attacks have weakened its cryptographic
underpinning.  DNSSEC {{RFC9364}} originally made extensive use of SHA-1 as a
cryptographic verification algorithm in RRSIG and Delegation Signer (DS)
records, for example.  Since then, multiple other signing algorithms with
stronger cryptographic strength are now widely available for DS records (such
as SHA-256 {{RFC4509}}, SHA-384 ({{RFC6605}})) and for DNSKEY and RRSIG records
(such as RSASHA256 ({{RFC5702}}), RSASHA512 ({{RFC5702}}), ECDSAP256SHA256
{{RFC6605}}, ECDSAP384SHA384 {{RFC6605}}, ED25519 {{RFC8080}}, and ED448
{{RFC8080}}). Further, support for validating SHA-1 based signatures has been
removed from some systems. As a result, SHA-1 is no longer fully interoperable
in the context of DNSSEC. As adequate alternatives exist, the use of SHA-1 is
no longer advisable.

This document thus further deprecates the use of RSASHA1 and
RSASHA1-NSEC3-SHA1 for DNS Security Algorithms.

## Requirements notation

   The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT",
   "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY",
   and "OPTIONAL" in this document are to be interpreted as described
   in BCP 14 {{RFC2119}} {{?RFC8174}} when, and only when, they appear
   in all capitals, as shown here.

# Deprecating RSASHA1 and RSASHA1-NSEC3-SHA1 algorithms in DNSSEC

The RSASHA1 {{RFC4034}} and RSASHA1-NSEC3-SHA1 {{RFC5155}} algorithms
MUST NOT be used when creating DNSKEY and RRSIG records.

Validating resolvers MUST continue to support validation using these
algorithms as they are diminishing in use but still actively in use
for some domains as of this publication.  Validating resolvers MAY
treat RRSIG records created from DNSKEY records using these algorithms
as an unsupported algorithm.

# Security Considerations

This document reduces the risk that a zone cannot be validated due
to lack of SHA-1 support in a validator, by guiding signers to choose
a more interoperable signing algorithm.

# Operational Considerations

Zone owners currently making use of SHA-1 based algorithms should
immediately switch to algorithms with stronger cryptographic strengths,
such as those listed in the introduction.

# IANA Considerations

IANA is requested to set the "Use for DNSSEC Delegation" field of the
"Digest Algorithms" registry {{DS-IANA}} for SHA-1 (1) to MUST NOT.

IANA is requested to set the "Use for DNSSEC Signing" column of the
DNS Security Algorithm Numbers registry {{DNSKEY-IANA}} to MUST NOT
for the RSASHA1 (5) and RSASHA1-NSEC3-SHA1 (7) algorithms.

All other columns should remain as currently specified.

--- back

# Acknowledgments

The authors appreciate the comments and suggestions from the following IETF
participants in helping produce this document: Mark Andrews, Steve Crocker,
Russ Housely, Shumon Huque, Paul Hoffman, S Moonesamy, Peter Dickson, Peter
Thomassen, Stefan Ubbink, Paul Wouters, Tim Wicinski,  and the many members of
the DNSOP working group that discussed this draft.


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
