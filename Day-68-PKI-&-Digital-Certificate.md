# Day 68 - PKI & Digital Certificates

## What It Is
PKI (Public Key Infrastructure) is the system of policies, processes, and technologies that manages digital certificates and public keys — enabling trusted, verified encrypted communication across the internet. A digital certificate is a digitally signed document that binds a public key to an identity (a website, organization, or person), verified by a trusted third party called a Certificate Authority (CA). PKI is what makes HTTPS work — when your browser shows a padlock, it's because a CA has verified that the server's public key genuinely belongs to the website you're visiting. Without PKI, asymmetric encryption (day 67) would be vulnerable to man-in-the-middle attacks since anyone could claim to be anyone.
