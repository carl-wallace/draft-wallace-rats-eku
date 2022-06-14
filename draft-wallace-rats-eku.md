---
v: 3

title: Extended Key Usage (EKU) Values for Remote Attestation Procedures (RATS)
abbrev: EKU for RATS
category: std
ipr: trust200902
submissionType: IETF

docname: draft-wallace-rats-eku-latest
area: "Security"
workgroup: "Remote ATtestation ProcedureS"
keyword: Internet-Draft
venue:
  mail: "rats@ietf.org"

author:
- ins: C. Wallace
  name: Carl Wallace
  org: Red Hound Software
  abbrev: Red Hound
  email: carl@redhoundsoftware.com
  country: USA
- ins: R. Housley
  name: Russ Housley
  org: Vigil Security, LLC
  abbrev: Vigil Security
  email: housley@vigilsec.com
  street: 516 Dranesville Road
  code: "20170"
  city: Herndon
  region: VA
  country: USA

normative:
  RFC5280:
  RFC7299: PKIX OIDs
  RFC5912:

informative:
  I-D.draft-birkholz-rats-corim:
  I-D.draft-ietf-rats-eat: EAT
  I-D.draft-ietf-sacm-coswid:
  I-D.draft-ietf-rats-architecture:

  COTS:
      title: "Concise TA Stores (CoTS)"
      author:
        -
          fullname: "Carl Wallace"
          organization: Red Hound Software
        -
          fullname: "Russ Housley"
          organization: Vigil Security, LLC
      date: June, 2022

--- abstract

X.509 certificates may be used for several different purposes in the Remote Attestation Procedures (RATS) architecture including verifying endorsements, reference values, digital letters of approval, attestations, or public key certificates. This document defines a set of extended key usage values that align with these purposes to facilitate enforcement of constraints on certificate usage.

--- middle

# Introduction

{{RFC5280}} defined the extended key usage extension to indicate "one or more purposes for which the certified public key may be used, in addition to or in place of the basic purposes indicated in the key usage extension." It included definition of several basic extended key values. Section 3.6 of {{RFC7299}} provides a registry for extended key usage values and has been used be several specifications to define additional extended key usage values.

This document defines extended key usage values that may be used when verifying artifacts in the context of the RATS architecture [I-D.draft-ietf-rats-architecture]. The extended key usage values defined here mirror the purpose values defined in {{COTS}}. The certificate purpose from {{COTS}} is not included here because the basicConstraints extensions serves that purpose.

# Conventions and Definitions

{::boilerplate bcp14-tagged}

# Extended Key Usage Values for RATS

{{COTS}} defines the extensible $tas-list-purpose mechanism to express verification actions that are applicable to a give trust anchor or set of trust anchors. Seven initial values are defined: cots, corim, coswid, eat, key-attestation, certificate, dloa. An extended key usage value is defined below for each of these purposes.

~~~~~~
id-kp-cots OBJECT IDENTIFIER ::=  { id-kp TBD1 }
id-kp-corim OBJECT IDENTIFIER ::=  { id-kp TBD2 }
id-kp-coswid OBJECT IDENTIFIER ::=  { id-kp TBD3 }
id-kp-eat OBJECT IDENTIFIER ::=  { id-kp TBD4 }
id-kp-key-attestation OBJECT IDENTIFIER ::=  { id-kp TBD5 }
id-kp-dloa OBJECT IDENTIFIER ::=  { id-kp TBD6 }
~~~~~~

Entities verifying one of the indicated artifacts MAY require presence of an extendedKeyUsage extension with appropriate value corresponding to the type of artifact being verified for the certificate to be acceptable for the given verification action.

# Security Considerations

The extended key usage values defined in this document are intended to provide a lightweight means of constraining use of certificates when verifying various types of artifacts associated with verification of attestations as described in {{I-D.draft-ietf-rats-architecture}}. Use of extended key usage in practice has been complicated by disparate enforcement of the extension. Some implementations only enforce values presented in end entity certificates, consistent with {{RFC5280}}. Others require EKU values to be present in intermediate CA certificates. These differences can result in different adjudications for the same certification path by different implementations.

# IANA Considerations

IANA is requested to allocate seven values from the "SMI Security for PKIX Extended Key Purpose" Registry {{RFC7299}}, preferably with the specific values requested:

| Decimal | Description| References |
| 31 | id-kp-cots | RFCTBD |
| 32 | id-kp-corim | RFCTBD |
| 33 | id-kp-coswid | RFCTBD |
| 34 | id-kp-eat | RFCTBD |
| 35 | id-kp-key-attestation | RFCTBD |
| 36 | id-kp-dloa | RFCTBD |

# ASN.1 Module

The following ASN.1 module makes use of the conventions from {{RFC5912}}.

~~~~~~
RatsEku-2022
{ iso(1) identified-organization(3) dod(6)
  internet(1) security(5) mechanisms(5) pkix(7) id-mod(0)
  id-mod-rats-eku(TBD7) }

DEFINITIONS IMPLICIT TAGS ::=
BEGIN

IMPORTS

id-kp
FROM PKIX1Explicit-2009 -- from [RFC5912]
  { iso(1) identified-organization(3) dod(6) internet(1) security(5)
    mechanisms(5) pkix(7) id-mod(0) id-mod-pkix1-explicit-02(51) }

;

-- EXPORT ALL --

id-kp-cots OBJECT IDENTIFIER ::=  { id-kp TBD1 }
id-kp-corim OBJECT IDENTIFIER ::=  { id-kp TBD2 }
id-kp-coswid OBJECT IDENTIFIER ::=  { id-kp TBD3 }
id-kp-eat OBJECT IDENTIFIER ::=  { id-kp TBD4 }
id-kp-key-attestation OBJECT IDENTIFIER ::=  { id-kp TBD5 }
id-kp-dloa OBJECT IDENTIFIER ::=  { id-kp TBD6 }

END
~~~~~~

--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.
