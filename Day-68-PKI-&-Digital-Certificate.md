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

## Real-World Example
In 2017, Google's Chrome team discovered that Symantec (one of the world's largest CAs) had been improperly issuing thousands of certificates — including test certificates for Google domains — without following CA/Browser Forum rules. Google announced it would distrust all Symantec-issued certificates in Chrome, affecting hundreds of millions of websites. Symantec's CA business was ultimately sold to DigiCert. This incident highlighted how critical CA trustworthiness is — a compromised or misbehaving CA can issue fraudulent certificates for any domain, enabling MitM attacks against any HTTPS site.

## Why It Matters
From an attacker's side, PKI attacks target the chain of trust — a compromised CA can issue fraudulent certificates for any domain, making MitM attacks (day 01-03) against HTTPS sites possible. Certificate transparency logs (public records of all issued certificates) were introduced specifically to detect fraudulent certificate issuance. Stolen private keys allow impersonating a legitimate server. Expired certificates cause service outages and browser warnings that users click through.

From a defender's side, keeping certificates current, using short validity periods, implementing Certificate Transparency monitoring, and pinning certificates in mobile apps (certificate pinning) are the core PKI security practices. Let's Encrypt democratized free automated DV certificates, eliminating the cost barrier for HTTPS adoption.

## Key Terms
- PKI (Public Key Infrastructure): the system of CAs, certificates, policies, and procedures enabling trusted encrypted communication
- CA (Certificate Authority): a trusted organization that issues and signs digital certificates after verifying the requester's identity
- X.509: the standard format for digital certificates used across the internet
- Certificate Chain: the path from an end-entity certificate up through intermediate CAs to a trusted root CA
- Certificate Revocation: the process of invalidating a certificate before its expiry — via CRL (Certificate Revocation List) or OCSP

## One Tip / Tool

Tool: `OpenSSL` for certificate inspection and `Let's Encrypt / Certbot` for free certificate issuance

```bash
# inspect a website's certificate
openssl s_client -connect example.com:443 -showcerts

# view certificate details from a file
openssl x509 -in certificate.pem -text -noout
