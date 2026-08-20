# Day 68 - PKI & Digital Certificates

## What It Is
PKI (Public Key Infrastructure) is the system of policies, processes, and technologies that manages digital certificates and public keys — enabling trusted, verified encrypted communication across the internet. A digital certificate is a digitally signed document that binds a public key to an identity (a website, organization, or person), verified by a trusted third party called a Certificate Authority (CA). PKI is what makes HTTPS work — when your browser shows a padlock, it's because a CA has verified that the server's public key genuinely belongs to the website you're visiting. Without PKI, asymmetric encryption (day 67) would be vulnerable to man-in-the-middle attacks since anyone could claim to be anyone.

## How It Works
```
PKI chain of trust:

Root CA (self-signed, trusted by operating systems and browsers)
    ↓ signs
Intermediate CA (issued by Root CA)
    ↓ signs
End-entity Certificate (issued to a website or organization)

When you visit https://example.com:
1. Server presents its certificate (contains its public key + CA signature)
2. Browser verifies the CA's signature using the CA's public key
3. Browser checks the CA is in its trusted root store
4. Browser checks certificate hasn't expired or been revoked
5. Browser uses the verified public key to establish secure session

Certificate contents (X.509 format):
- Subject: who the certificate belongs to (domain name, org)
- Issuer: which CA signed it
- Public Key: the key being certified as belonging to the subject
- Validity Period: not before / not after dates
- Subject Alternative Names (SANs): other domains this cert covers
- Serial Number: unique identifier
- Digital Signature: CA's signature proving authenticity
```

Certificate types by validation level:
```
DV (Domain Validation)    - CA verifies domain ownership only
                            fastest to get, cheapest, used by most sites
OV (Organization Validation) - CA verifies domain + organization identity
EV (Extended Validation)  - most thorough verification, green bar (legacy)
                            expensive, used by banks and financial sites
Wildcard Certificate      - *.example.com covers all subdomains
SAN Certificate           - covers multiple different domains in one cert
```
