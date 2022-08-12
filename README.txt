



Network Working Group                                        W. Hardaker
Internet-Draft                                                   USC/ISI
Intended status: Standards Track                          12 August 2022
Expires: 13 February 2023


               Remove SHA-1 from active use within DNSSEC
                 draft-hardaker-dnsop-must-not-sha1-00

Abstract

   This document retires the use of SHA-1 within DNSSEC

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

   This Internet-Draft will expire on 13 February 2023.

Copyright Notice

   Copyright (c) 2022 IETF Trust and the persons identified as the
   document authors.  All rights reserved.

   This document is subject to BCP 78 and the IETF Trust's Legal
   Provisions Relating to IETF Documents (https://trustee.ietf.org/
   license-info) in effect on the date of publication of this document.
   Please review these documents carefully, as they describe your rights
   and restrictions with respect to this document.  Code Components
   extracted from this document must include Simplified BSD License text
   as described in Section 4.e of the Trust Legal Provisions and are
   provided without warranty as described in the Simplified BSD License.








Hardaker                Expires 13 February 2023                [Page 1]

Internet-Draft         MUST NOT DNSSEC with SHA-1            August 2022


Table of Contents

   1.  Introduction  . . . . . . . . . . . . . . . . . . . . . . . .   2
     1.1.  Requirements notation . . . . . . . . . . . . . . . . . .   2
   2.  Deprecating SHA-1 algorithms in DNSSEC  . . . . . . . . . . .   2
   3.  Security Considerations . . . . . . . . . . . . . . . . . . .   3
   4.  Operational Considerations  . . . . . . . . . . . . . . . . .   3
   5.  IANA Considerations . . . . . . . . . . . . . . . . . . . . .   3
   6.  References  . . . . . . . . . . . . . . . . . . . . . . . . .   3
     6.1.  Normative References  . . . . . . . . . . . . . . . . . .   3
     6.2.  Informative References  . . . . . . . . . . . . . . . . .   4
   Appendix A.  Acknowledgments  . . . . . . . . . . . . . . . . . .   5
   Appendix B.  Github Version of this document  . . . . . . . . . .   5
   Author's Address  . . . . . . . . . . . . . . . . . . . . . . . .   5

1.  Introduction

   The security of the SHA-1 algorithm [RFC3174] has been slowly
   diminishing over time as various forms of attacks have weakened its
   cryptographic underpinning.  DNSSEC [RFC4033] [RFC4034] [RFC4035]
   originally made extensive use of SHA-1 as a cryptographic
   verification algorithm in RRSIG and Delegation Signer (DS) records,
   for example.  Since then, multiple other signing algorithms with
   stronger cryptographic strength are now widely available for DS
   records (such as SHA-256 [RFC4509], SHA-384 ([RFC6605])) and for
   DNSKEY and RRSIG records (such as RSASHA256 ([RFC5702]), RSASHA512
   ([RFC5702]), ECDSAP256SHA256 [RFC6605], ECDSAP384SHA384 [RFC6605],
   ED25519 [RFC8080], and ED448 [RFC8080]), the use of SHA-1 is no
   longer needed.

   This document retires the use of SHA-1 within DNSSEC.

1.1.  Requirements notation

   The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT",
   "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and
   "OPTIONAL" in this document are to be interpreted as described in BCP
   14 [RFC2119] [RFC8174] when, and only when, they appear in all
   capitals, as shown here.

2.  Deprecating SHA-1 algorithms in DNSSEC

   The SHA-1 [RFC3685] algorithm MUST NOT be used when creating DS
   records.

   The RSASHA1 [RFC4034], DSA-NSEC3-SHA1 [RFC5155], and
   RSASHA1-NSEC3-SHA1 [RFC5155] algorithms MUST NOT be used when
   creating DNSKEY and RRSIG records.



Hardaker                Expires 13 February 2023                [Page 2]

Internet-Draft         MUST NOT DNSSEC with SHA-1            August 2022


3.  Security Considerations

   This document increases the security of the DNSSEC ecosystem by
   deprecating algorithms that make use of older algorithms with SHA-1
   derived uses.

4.  Operational Considerations

   Zone owners currently making use of SHA-1 based algorithms should
   immediate switch to algorithms with stronger cryptographic strengths,
   such as those listed in the introduction.  DNS registries [RFC8499]
   should prohibit their clients to upload and publish SHA-1 based DS
   records.

5.  IANA Considerations

   IANA is requested to mark the following Delegation Signer (DS)
   Resource Record (RR) digest type algorithms as deprecated:

   *  SHA-1

   IANA is requested to mark the following DNS Security Algorithm
   Numbers as deprecated:

   *  RSASHA1

   *  DSA-NSEC3-SHA1

   *  RSASHA1-NSEC3-SHA1

6.  References

6.1.  Normative References

   [RFC2119]  Bradner, S., "Key words for use in RFCs to Indicate
              Requirement Levels", BCP 14, RFC 2119,
              DOI 10.17487/RFC2119, March 1997,
              <https://www.rfc-editor.org/info/rfc2119>.

   [RFC3174]  Eastlake 3rd, D. and P. Jones, "US Secure Hash Algorithm 1
              (SHA1)", RFC 3174, DOI 10.17487/RFC3174, September 2001,
              <https://www.rfc-editor.org/info/rfc3174>.

   [RFC3685]  Daboo, C., "SIEVE Email Filtering: Spamtest and VirusTest
              Extensions", RFC 3685, DOI 10.17487/RFC3685, February
              2004, <https://www.rfc-editor.org/info/rfc3685>.





Hardaker                Expires 13 February 2023                [Page 3]

Internet-Draft         MUST NOT DNSSEC with SHA-1            August 2022


   [RFC4033]  Arends, R., Austein, R., Larson, M., Massey, D., and S.
              Rose, "DNS Security Introduction and Requirements",
              RFC 4033, DOI 10.17487/RFC4033, March 2005,
              <https://www.rfc-editor.org/info/rfc4033>.

   [RFC4034]  Arends, R., Austein, R., Larson, M., Massey, D., and S.
              Rose, "Resource Records for the DNS Security Extensions",
              RFC 4034, DOI 10.17487/RFC4034, March 2005,
              <https://www.rfc-editor.org/info/rfc4034>.

   [RFC4035]  Arends, R., Austein, R., Larson, M., Massey, D., and S.
              Rose, "Protocol Modifications for the DNS Security
              Extensions", RFC 4035, DOI 10.17487/RFC4035, March 2005,
              <https://www.rfc-editor.org/info/rfc4035>.

   [RFC4509]  Hardaker, W., "Use of SHA-256 in DNSSEC Delegation Signer
              (DS) Resource Records (RRs)", RFC 4509,
              DOI 10.17487/RFC4509, May 2006,
              <https://www.rfc-editor.org/info/rfc4509>.

   [RFC5155]  Laurie, B., Sisson, G., Arends, R., and D. Blacka, "DNS
              Security (DNSSEC) Hashed Authenticated Denial of
              Existence", RFC 5155, DOI 10.17487/RFC5155, March 2008,
              <https://www.rfc-editor.org/info/rfc5155>.

   [RFC5702]  Jansen, J., "Use of SHA-2 Algorithms with RSA in DNSKEY
              and RRSIG Resource Records for DNSSEC", RFC 5702,
              DOI 10.17487/RFC5702, October 2009,
              <https://www.rfc-editor.org/info/rfc5702>.

   [RFC6605]  Hoffman, P. and W.C.A. Wijngaards, "Elliptic Curve Digital
              Signature Algorithm (DSA) for DNSSEC", RFC 6605,
              DOI 10.17487/RFC6605, April 2012,
              <https://www.rfc-editor.org/info/rfc6605>.

   [RFC8080]  Sury, O. and R. Edmonds, "Edwards-Curve Digital Security
              Algorithm (EdDSA) for DNSSEC", RFC 8080,
              DOI 10.17487/RFC8080, February 2017,
              <https://www.rfc-editor.org/info/rfc8080>.

6.2.  Informative References

   [RFC8174]  Leiba, B., "Ambiguity of Uppercase vs Lowercase in RFC
              2119 Key Words", BCP 14, RFC 8174, DOI 10.17487/RFC8174,
              May 2017, <https://www.rfc-editor.org/info/rfc8174>.






Hardaker                Expires 13 February 2023                [Page 4]

Internet-Draft         MUST NOT DNSSEC with SHA-1            August 2022


   [RFC8499]  Hoffman, P., Sullivan, A., and K. Fujiwara, "DNS
              Terminology", BCP 219, RFC 8499, DOI 10.17487/RFC8499,
              January 2019, <https://www.rfc-editor.org/info/rfc8499>.

Appendix A.  Acknowledgments

   TBD

Appendix B.  Github Version of this document

   While this document is under development, it can be viewed, tracked,
   fill here:

   https://github.com/hardaker/...

Author's Address

   Wes Hardaker
   USC/ISI

   Email: ietf@hardakers.net






























Hardaker                Expires 13 February 2023                [Page 5]
