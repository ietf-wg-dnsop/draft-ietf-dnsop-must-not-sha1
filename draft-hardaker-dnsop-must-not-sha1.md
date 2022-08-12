---
title: "Remove SHA-1 from active use within DNSSEC"
abbrev: MUST NOT DNSSEC with SHA-1
docname: draft-hardaker-dnsop-must-not-sha1-00
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

informative:
  RFC8499:


--- abstract

This document retires the use of SHA-1 within DNSSEC

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

This document retires the use of SHA-1 within DNSSEC.

## Requirements notation

   The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT",
   "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY",
   and "OPTIONAL" in this document are to be interpreted as described
   in BCP 14 {{RFC2119}} {{?RFC8174}} when, and only when, they appear
   in all capitals, as shown here.

# Deprecating SHA-1 algorithms in DNSSEC

The SHA-1 {{RFC3685}} algorithm MUST NOT be used when creating DS records.

The RSASHA1 {{RFC4034}}, DSA-NSEC3-SHA1 {{RFC5155}},
and RSASHA1-NSEC3-SHA1 {{RFC5155}} algorithms MUST NOT be used when
creating DNSKEY and RRSIG records. 

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

IANA is requested to mark the following Delegation Signer (DS)
Resource Record (RR) digest type algorithms as deprecated:

- SHA-1

IANA is requested to mark the following DNS Security Algorithm Numbers
as deprecated:

- RSASHA1
- DSA-NSEC3-SHA1
- RSASHA1-NSEC3-SHA1

--- back

# Acknowledgments

TBD

# Current algorithm usage levels

The DNSSEC scanning project by Viktor Dukhovni and Wes Hardaker
highlights the current deployment of various algorithms on the
https://stats.dnssec-tools.org/ website.

[RFC Editor: please delete this section upon publication]

# Github Version of this document

While this document is under development, it can be viewed, tracked,
fill here:

https://github.com/hardaker/draft-hardaker-dnsop-must-not-sha1

