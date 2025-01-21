



Network Working Group                                        W. Hardaker
Internet-Draft                                                   USC/ISI
Intended status: Standards Track                               W. Kumari
Expires: 25 July 2025                                             Google
                                                         21 January 2025


      Deprecating the use of SHA-1 in DNSSEC signature algorithms
                   draft-ietf-dnsop-must-not-sha1-02

Abstract

   This document deprecates the use of the RSASHA1 and
   RSASHA1-NSEC3-SHA1 algorithms for the creation of DNSKEY and RRSIG
   records.

Status of This Memo

   This Internet-Draft is submitted in full conformance with the
   provisions of BCP 78 and BCP 79.

   Internet-Drafts are working documents of the Internet Engineering
   Task Force (IETF).  Note that other groups may also distribute
   working documents as Internet-Drafts.  The list of current Internet-
   Drafts is at https://datatracker.ietf.org/drafts/current/.

   Internet-Drafts are draft documents valid for a maximum of six months
   and may be updated, replaced, or obsoleted by other documents at any
   time.  It is inappropriate to use Internet-Drafts as reference
   material or to cite them other than as "work in progress."

   This Internet-Draft will expire on 25 July 2025.

Copyright Notice

   Copyright (c) 2025 IETF Trust and the persons identified as the
   document authors.  All rights reserved.

   This document is subject to BCP 78 and the IETF Trust's Legal
   Provisions Relating to IETF Documents (https://trustee.ietf.org/
   license-info) in effect on the date of publication of this document.
   Please review these documents carefully, as they describe your rights
   and restrictions with respect to this document.  Code Components
   extracted from this document must include Revised BSD License text as
   described in Section 4.e of the Trust Legal Provisions and are
   provided without warranty as described in the Revised BSD License.





Hardaker & Kumari         Expires 25 July 2025                  [Page 1]

Internet-Draft         MUST NOT DNSSEC with SHA-1           January 2025


Table of Contents

   1.  Introduction  . . . . . . . . . . . . . . . . . . . . . . . .   2
     1.1.  Requirements notation . . . . . . . . . . . . . . . . . .   2
   2.  Deprecating RSASHA1 and RSASHA1-NSEC3-SHA1 algorithms in
           DNSSEC  . . . . . . . . . . . . . . . . . . . . . . . . .   3
   3.  Security Considerations . . . . . . . . . . . . . . . . . . .   3
   4.  Operational Considerations  . . . . . . . . . . . . . . . . .   3
   5.  IANA Considerations . . . . . . . . . . . . . . . . . . . . .   3
   6.  References  . . . . . . . . . . . . . . . . . . . . . . . . .   3
     6.1.  Normative References  . . . . . . . . . . . . . . . . . .   3
     6.2.  Informative References  . . . . . . . . . . . . . . . . .   5
   Appendix A.  Acknowledgments  . . . . . . . . . . . . . . . . . .   5
   Appendix B.  Current algorithm usage levels . . . . . . . . . . .   5
   Appendix C.  Github Version of this document  . . . . . . . . . .   5
   Authors' Addresses  . . . . . . . . . . . . . . . . . . . . . . .   5

1.  Introduction

   The security of the SHA-1 algorithm [RFC3174] has been slowly
   diminishing over time as various forms of attacks have weakened its
   cryptographic underpinning.  DNSSEC [RFC9364] originally made
   extensive use of SHA-1 as a cryptographic verification algorithm in
   RRSIG and Delegation Signer (DS) records, for example.  Since then,
   multiple other signing algorithms with stronger cryptographic
   strength are now widely available for DS records (such as SHA-256
   [RFC4509], SHA-384 ([RFC6605])) and for DNSKEY and RRSIG records
   (such as RSASHA256 ([RFC5702]), RSASHA512 ([RFC5702]),
   ECDSAP256SHA256 [RFC6605], ECDSAP384SHA384 [RFC6605], ED25519
   [RFC8080], and ED448 [RFC8080]).  Further, support for validating
   SHA-1 based signatures has been removed from some systems.  As a
   result, SHA-1 is no longer fully interoperable in the context of
   DNSSEC.  As adequate alternatives exist, the use of SHA-1 is no
   longer advisable.

   This document thus further deprecates the use of RSASHA1 and
   RSASHA1-NSEC3-SHA1 for DNS Security Algorithms.

1.1.  Requirements notation

   The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT",
   "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and
   "OPTIONAL" in this document are to be interpreted as described in BCP
   14 [RFC2119] [RFC8174] when, and only when, they appear in all
   capitals, as shown here.






Hardaker & Kumari         Expires 25 July 2025                  [Page 2]

Internet-Draft         MUST NOT DNSSEC with SHA-1           January 2025


2.  Deprecating RSASHA1 and RSASHA1-NSEC3-SHA1 algorithms in DNSSEC

   The RSASHA1 [RFC4034] and RSASHA1-NSEC3-SHA1 [RFC5155] algorithms
   MUST NOT be used when creating DNSKEY and RRSIG records.

   Validating resolvers MUST continue to support validation using these
   algorithms as they are diminishing in use but still actively in use
   for some domains as of this publication.  Validating resolvers MAY
   treat RRSIG records created from DNSKEY records using these
   algorithms as an unsupported algorithm.

3.  Security Considerations

   This document reduces the risk that a zone cannot be validated due to
   lack of SHA-1 support in a validator, by guiding signers to choose a
   more interoperable signing algorithm.

4.  Operational Considerations

   Zone owners currently making use of SHA-1 based algorithms should
   immediately switch to algorithms with stronger cryptographic
   strengths, such as those listed in the introduction.

5.  IANA Considerations

   IANA is requested to set the "Use for DNSSEC Delegation" field of the
   "Digest Algorithms" registry [DS-IANA] for SHA-1 (1) to MUST NOT.

   IANA is requested to set the "Use for DNSSEC Signing" column of the
   DNS Security Algorithm Numbers registry [DNSKEY-IANA] to MUST NOT for
   the RSASHA1 (5) and RSASHA1-NSEC3-SHA1 (7) algorithms.

   All other columns should remain as currently specified.

6.  References

6.1.  Normative References

   [DNSKEY-IANA]
              IANA, "Domain Name System Security (DNSSEC) Algorithm
              Numbers", n.d., <https://www.iana.org/assignments/dns-sec-
              alg-numbers/dns-sec-alg-numbers.xhtml>.

   [DS-IANA]  IANA, "Delegation Signer (DS) Resource Record (RR) Type
              Digest Algorithms", n.d.,
              <http://www.iana.org/assignments/ds-rr-types>.





Hardaker & Kumari         Expires 25 July 2025                  [Page 3]

Internet-Draft         MUST NOT DNSSEC with SHA-1           January 2025


   [RFC2119]  Bradner, S., "Key words for use in RFCs to Indicate
              Requirement Levels", BCP 14, RFC 2119,
              DOI 10.17487/RFC2119, March 1997,
              <https://www.rfc-editor.org/rfc/rfc2119>.

   [RFC3174]  Eastlake 3rd, D. and P. Jones, "US Secure Hash Algorithm 1
              (SHA1)", RFC 3174, DOI 10.17487/RFC3174, September 2001,
              <https://www.rfc-editor.org/rfc/rfc3174>.

   [RFC4033]  Arends, R., Austein, R., Larson, M., Massey, D., and S.
              Rose, "DNS Security Introduction and Requirements",
              RFC 4033, DOI 10.17487/RFC4033, March 2005,
              <https://www.rfc-editor.org/rfc/rfc4033>.

   [RFC4034]  Arends, R., Austein, R., Larson, M., Massey, D., and S.
              Rose, "Resource Records for the DNS Security Extensions",
              RFC 4034, DOI 10.17487/RFC4034, March 2005,
              <https://www.rfc-editor.org/rfc/rfc4034>.

   [RFC4035]  Arends, R., Austein, R., Larson, M., Massey, D., and S.
              Rose, "Protocol Modifications for the DNS Security
              Extensions", RFC 4035, DOI 10.17487/RFC4035, March 2005,
              <https://www.rfc-editor.org/rfc/rfc4035>.

   [RFC4509]  Hardaker, W., "Use of SHA-256 in DNSSEC Delegation Signer
              (DS) Resource Records (RRs)", RFC 4509,
              DOI 10.17487/RFC4509, May 2006,
              <https://www.rfc-editor.org/rfc/rfc4509>.

   [RFC5155]  Laurie, B., Sisson, G., Arends, R., and D. Blacka, "DNS
              Security (DNSSEC) Hashed Authenticated Denial of
              Existence", RFC 5155, DOI 10.17487/RFC5155, March 2008,
              <https://www.rfc-editor.org/rfc/rfc5155>.

   [RFC5702]  Jansen, J., "Use of SHA-2 Algorithms with RSA in DNSKEY
              and RRSIG Resource Records for DNSSEC", RFC 5702,
              DOI 10.17487/RFC5702, October 2009,
              <https://www.rfc-editor.org/rfc/rfc5702>.

   [RFC6605]  Hoffman, P. and W.C.A. Wijngaards, "Elliptic Curve Digital
              Signature Algorithm (DSA) for DNSSEC", RFC 6605,
              DOI 10.17487/RFC6605, April 2012,
              <https://www.rfc-editor.org/rfc/rfc6605>.

   [RFC8080]  Sury, O. and R. Edmonds, "Edwards-Curve Digital Security
              Algorithm (EdDSA) for DNSSEC", RFC 8080,
              DOI 10.17487/RFC8080, February 2017,
              <https://www.rfc-editor.org/rfc/rfc8080>.



Hardaker & Kumari         Expires 25 July 2025                  [Page 4]

Internet-Draft         MUST NOT DNSSEC with SHA-1           January 2025


   [RFC9364]  Hoffman, P., "DNS Security Extensions (DNSSEC)", BCP 237,
              RFC 9364, DOI 10.17487/RFC9364, February 2023,
              <https://www.rfc-editor.org/rfc/rfc9364>.

6.2.  Informative References

   [RFC8174]  Leiba, B., "Ambiguity of Uppercase vs Lowercase in RFC
              2119 Key Words", BCP 14, RFC 8174, DOI 10.17487/RFC8174,
              May 2017, <https://www.rfc-editor.org/rfc/rfc8174>.

Appendix A.  Acknowledgments

   The authors appreciate the comments and suggestions from the
   following IETF participants in helping produce this document: Mark
   Andrews, Steve Crocker, Russ Housely, Shumon Huque, Paul Hoffman, S
   Moonesamy, Peter Dickson, Peter Thomassen, Stefan Ubbink, Paul
   Wouters, Tim Wicinski, and the many members of the DNSOP working
   group that discussed this draft.

Appendix B.  Current algorithm usage levels

   The DNSSEC scanning project by Viktor Dukhovni and Wes Hardaker
   highlights the current deployment of various algorithms on the
   https://stats.dnssec-tools.org/ website.

   <RFC Editor: please delete this section upon publication>

Appendix C.  Github Version of this document

   While this document is under development, it can be viewed, tracked,
   fill here:

   https://github.com/hardaker/draft-hardaker-dnsop-must-not-sha1

   <RFC Editor: please delete this section upon publication>

Authors' Addresses

   Wes Hardaker
   USC/ISI
   Email: ietf@hardakers.net


   Warren Kumari
   Google
   Email: warren@kumari.net





Hardaker & Kumari         Expires 25 July 2025                  [Page 5]
