---
currentMenu: home
---

# Milagro Introduction

Apache Milagro (incubating) establishes a new internet security framework purpose-built for cloud-connected app-centric software and IoT devices that require Internet scale. Milagro's purpose is to provide a secure, free, and positive open source alternative to centralised and proprietary monolithic trust providers such as commercial certificate authorities and the certificate backed cryptosystems that rely on them.
<br></br>
### Pairing-based Cryptography
Milagro leverages [pairing-based cryptography](https://en.wikipedia.org/wiki/Pairing-based_cryptography) to distribute cryptographic operations and split cryptographic parameters, providing a level of security and functionality that is a step forward in when compared to the certificate backed cryptosystems in service today. With pairing cryptography, security systems such as multi-factor authentication using zero knowledge protocols and certificate-less authenticated key agreement with perfect forward secrecy can be deployed in real world scenarios.
<br></br>
### Distributed Cryptosystem and Architecture
Consider BitCoin's Blockchain, which provides an alternative distributed approach to managing a currency without the need for a central bank. With BitCoin, the ledger is distributed, not centralised. Milagro's distributed cryptosystem is decentralised to create the same advantages as a distributed ledger. While architecturally different to the Blockchain, Milagro's distributed cryptosystem is compatible with Blockchain technology, sharing many of the same cryptographic building blocks.
<br></br>
### Distributed vs. Monolithic Trust Authorities
Milagro envisions a new class of cryptographic service providers called Distributed Trust Authorities, or D-TAs for short. The purpose of a D-TA is to independently issue shares, or fractions, of cryptographic keys to Milagro clients and servers and application endpoints which have embedded Milagro cryptographic libraries. D-TAs operate independently from each other, are isolated in totality, and completely unaware of the existence of other D-TAs.
<br></br>
### No Single Points of Comprosmise
Milagro clients and servers receive the issued shares cryptographic keys and combine them to create the whole completed key, thus becoming the only audience who possess knowledge of the entire key. Since key generation services are under separate organisational controls, current root key compromises and key escrow threats inherent in PKI systems are an order of magnitude harder to exploit.  An attacker would need to subvert all three (or more) independent parties, as a compromise of one D-TA in a three D-TA framework does not yield an attacker any cryptographic advantage.

In other words, all D-TAs used to generate shares, or fractions, of keys for Milagro clients and servers must be compromised to create the equivalent of a PKI root key compromise.
<br></br>
### No Mandated Authority
In practice, a Distributed Trust Authority (D-TA) framework would split the functions of a pairing-based key generation server into three services, each D-TA issuing thirds of private keys to distinct identities. The shares of the three cryptographic keys, as an example, could be generated by cloud computing providers, their customers, and dedicated trust providers. In this way, trust distribution can be more aligned to the participants with stakes in protecting the framework vs. the implicit trust model in use today with monolithic trust authorities such as PKI. Anyone actor can become a Distributed Trust Authority.
_________________________
<figure>
  <img src="/en/img2/D-TA.png">
  <figcaption>Distributed Trust Authorities</figcaption>
</figure>

______________________

__Initially started as a joint development effort by MIRACL, NTTi3 and NTT Labs, the results of this joint development are contributed to Apache Milagro (incubating).__

## Components
#### Milagro Crypto Library
These contributions consist of the baseline Milagro Crypto Library (MCL) that enables developers to build distributed trust systems and select from a choice of secure, proven, pairing based protocols that deliver certificate-less key encapsulation, zero knowledge proof authentication, authenticated key agreement and digital signing functionality.

Using MCL, application developers can embed multi-factor authentication, secure communications, and data protection methods that are robust enough to meet most requirements required by distributed ledger services, general on-line financial services, government and healthcare industries.
<br></br>
#### Milagro TLS
Apache Milagro (incubating) also contains a pairing-based TLS library, Milagro TLS, that enables encrypted connections with perfect forward secrecy between mobile applications or IoT devices and backend service infrastructures, without the need for certificates or PKI.

Milagro TLS delivers two new cipher suites that provides perfectly forward secure authenticated key agreement, without the need for certificate processing, for each session between client and server or peer to peer. Milagro TLS is a standalone library that uses MCL as its cryptographic service provider, resulting in an implementation that is lean, yet performant enough to run in constrained environments found in many IoT devices.
<br></br>
#### Milagro MFA
Also included is Milagro MFA, a higher level 'Crypto App' ready for the cloud, mobile or enterprise deployments. Milagro MFA is a complete multi-factor authentication platform that uses [zero-knowledge proof protocols](https://en.wikipedia.org/wiki/Zero-knowledge_proof) to eliminate the password and hence the threat of password database breach. Milagro MFA includes client SDKs in JavaScript, C, iOS, Android and Windows Phone, as well as the Authentication Server for Linux. Delivering 128-bit security but lean enough to even run in JavaScript, Milagro MFA allows developers and security engineers to integrate easy-to-use multi-factor authentication capabilities into their mobile and web properties and applications in hours or less.
<br></br>
## To Learn More

* To learn about Milagro components and concepts, [click here](milagro-concepts.html)
* To learn about the Pairing Crypto Protocols used in the Milagro framework, [click here](pairing-crypto-protocols.html)
* To learn about 'The Case for Something New', [click here](milagro-a-case-for-something-new-part-1.html)
* To read the 'Distributed Trust Ecosystem' proposal, [click here](distributed-trust.html)