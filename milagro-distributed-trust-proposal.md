---
currentMenu: milagro-distributed-trust-proposal
layout: markdeep
---
<style>h1:before, h2:before, h3:before { content: none; }</style>
<div id="generated-toc" class="generate_from_h2" class="generate_from_h3"></div>

## Distributed Trust Ecosystem components

The components consist of
- People, Apps or Things (PATs)
- Distributed Trust Authorities (D-TAs)
- Identity Providers (IdPs)
- Trusted Bitcoin Server proxy (TBS) - most likely run as a service for customer's Internet scale deployments, and also available as an open source Apache Milagro server component

Commonalities:
Each component on the system, when it comes online and registers itself into the Blockchain (whether assisted by the TBS or not) does so through the creation of a Birth Certificate document. This document is hashed and the hash is stored using the 40byte field available in OP_RETURN transactions on the Blockchain. The hash can be used to locate transaction identifiers.

## Milagro D-TA Software Stack

We begin with the establishment of a Distributed Trust Authority service. In order for a D-TA to take hold, its Proof-of-Existence must be evidenced within the Blockchain itself in order to boostrap secure connections to other participants in the ecosystem. To register a D-TA service, a 'Milagro D-TA Software Stack' that runs Distributed Trust Authority services should ideally consist of
* an OpenID Connect client
* a Blockchain client acting as a headless Enterprise Bitcoin Server, capable of performing OP_RETURN (TBD) transactions with enough Bitcoin that enables transaction fees to be paid to miners for validating blocks containing its Proof-of-Existence (i.e. Birth Certificate), transaction identifier (txid), and subsequent Merkle roots containing audit data
* an D-TA Activity logger, which creates time bound Merkle roots encompassing D-TA activity; essentially, a log of all key shares issued to people, apps and things
* Psuedo-random number generator with sufficient entropy
* TLS library for creating certificate-less secured connections driven by authenticated key agreements based upon the existence of ECDSA signatures between client and server or peer to peer. At least one of the signatures should be resident in the Blockchain, with enough time passing so that a re-write of the block housing the signature(s) becomes unlikely. These ciphersuites in Milagro TLS would be 'ECDH over Bitcoin' and 'YAK over Bitcoin'.

The D-TA software, upon installation, creates its own Master Secret $s$ and a random element $F_q$ in addition to Bitcoin ECDSA public / private key pair. The D-TA software registers its existence using a cryptographic digest of the D-TA's **Birth Certificate**, linked to the time in which it submitted the record, using the OP_RETURN designation, signed by its ECDSA private key. In this way, the D-TA can publicly prove that it existed and was created at a starting point, with a decentralised certification based on the bitcoin network.

The D-TA, through its ECDSA signature now resident in the Blockchain, has also created the cryptographic primitive that any actor on the system can use to bootstrap a secured connection to it. Knowledge of the discrete log k from a single digital signature in a transaction provides the primitives necessary to drive the authenticated key agreement (covered in following section) as long as both parties have each created a signature in the Blockchain.

The Birth Certificate is certified via embedding its SHA256 digest in the bitcoin blockchain. This is done by generating a special bitcoin transaction that encodes/contains the hash of the Birth Certificate document via an OP_RETURN script and a special designation (TBC) in the transaction identifier (txid). This is a bitcoin scripting opcode that marks the transaction output as provably unspendable and allows a small amount of data to be inserted, which in our case is the hash of the Birth Certificate, plus a marker to identify all of its future transaction.

Finding the hashes of Birth Certificates in the Blockchain is made easier by looking for specific transactions in the bitcoin blockchain containing an OP_RETURN output with the Birth Certificates's hash prepended by a universal Milagro D-TA marker bytes, which would resemble something like 0x444f4350524f4f46 (NEED TO CREATE MILAGRO VERSION OF THIS - written is a 'proof of existence's' marker bytes / must change to match 'Milagro D-TA' in ascii).

Once the transaction is confirmed, the hash of the Birth Certificate is permanently certified and proven to exist at least as early as the time the transaction was confirmed. If the D-TA's Birth Certificate hadn't existed at the time the transaction entered the blockchain, it would have been impossible to embed its digest in the transaction (This is because of the hash function's property of being second pre-image resistant).

The full Birth Certificate /*CAN BE* publicly hosted on web by the D-TA, which /*SHOULD be discoverable as a normative URL at every D-TA, similar to the additional [OpenID Provider Metadata parameter](https://openid.net/specs/openid-connect-discovery-1_0.html) so that individual actors in the ecosystem can create their own comparison hash of the Birth Certificate of a D-TA to ascertain if any data has changed. As an example, if a Distributed Trust Authority is forced into giving up its Master Secret because of legal issues, it could issue a canary warning through the Birth Certificate by changing it to notify the world at large that the D-TA's circumstances have changed.

### D-TA Actions on install and configuration
- Creates its own Master Secret $s$ and a random element $F_q$
- Create Bitcoin public / private key pair
- Create Birth Certificate
- Embed Birth Certificate's SHA256 digest in the bitcoin blockchain via an OP_RETURN script and sign the transaction with ECDSA key
- Host Birth Certificate, it's SHA256 digest, its ECDSA public key and transaction identifier (txid) - to find the signature in the blockchain) publicly online in normative location

// NEED Birth Certificate FORMAT (JSON?)

## Milagro IdP Software Stack

The D-TA /*CAN* be configured to use an independent Identity Provider (IdP) through the OpenId Connect protocol, or will use its own private IdP which is solely in service to the corresponding D-TA. However, all IdP's in service to a publicly available D-TA */MUST offer the use the OpenID Connect federation protocol to the D-TA's.

To do this, the D-TA software will contain an OpenID Connect client capable of connecting to an IdP as a Relying Party.

A 'Milagro IdP Software Stack' will contain an IdP server which */MUST conform to OpenID Connect standards and support the following OpenID Connect endpoints:

* WebFinger — Enables dynamic discovery of the OpenID Connect provider for a given user, based on their email address or some other information.
* Provider metadata — JSON document listing the OP endpoint URLs and the OpenID Connect / OAuth 2.0 server features that it supports. Client apps can use this information to configure their requests to the OP.
* Provider JWK set — JSON document containing the provider’s public keys (typically RSA) in JSON Web Key (JWK) format. These keys are used to secure the issued ID tokens and other artifacts.
* Client registration — RESTful web API for registering client apps with the OP. Registration may be protected (require pre-authorisation) or open (public).

The 'Milagro IdP Software Stack' should be running the following software (developed by Milagro)
* an OpenID Connect Server (see above)
* a Blockchain client acting as a headless Enterprise Bitcoin Server, capable of performing OP_RETURN (TBD) transactions with enough Bitcoin that enables transaction fees to be paid to miners for validating blocks containing its Proof-of-Existence (i.e. Birth Certificate) and subsequent Merkle roots containing audit data
* an IdP Activity logger, which creates time bound Merkle roots encompassing IdP activity; essentially, a log of all successful authentication attempts from people, apps and things, secured Identities with one-way hashes (which should be concatenated of ID + Time Period)
* Psuedo-random number generator with sufficient entropy
* TLS library for creating certificate-less secured connections driven by authenticated key agreements based upon the existence of ECDSA signatures between client and server or peer to peer. At least one of the signatures should be resident in the Blockchain, with enough time passing so that a re-write of the block housing the signature(s) becomes unlikely. These ciphersuites in Milagro TLS would be 'ECDH over Bitcoin' and 'YAK over Bitcoin'.

Whether the IdP offers protected registration (meaning a D-TA must register and be authorised to use its services) or the D-TA supports open registration, meaning any D-TA can connect, is beyond the scope of this document.

The IdP during its initial setup and configuration, will have performed some of the same actions as the D-TA setup. These are:

### IdP actions on install and configuration

- Create Bitcoin public / private key pair
- Create Birth Certificate
- Embed Birth Certificate's SHA256 digest in the bitcoin blockchain via an OP_RETURN script and sign the transaction with ECDSA key
- Host Birth Certificate, it's SHA256 digest, ECDSA public key and transaction identifier (txid) - to find the signature in the blockchain)) publicly online in normative location

Note that for the IdP, the additional data in the last line above [OpenID Provider Metadata parameter](https://openid.net/specs/openid-connect-discovery-1_0.html) */MUST be hosted online and discoverable as additional metadata through the OpenID Connect protocol.

## People / Apps / Things (PATs) Software Stack

Milagro client code */MUST contain a 'thin' Bitcoin client which is a program that generates Bitcoin public / private key pair, creates Birth Certificate and associated date, performs the ECIES protocol and connects to a Trusted Bitcoin Server proxy (more below) using Milagro TLS.

Why? Because Milagro is intended to solve issues for the IoT ecosystem, loading full Bitcoin clients on constrained device environments will not work.

Thus the 'thin' Bitcoin client */MUST be configured to use some service, pre-selected in advance by the application developer, as a "Trusted Bitcoin Server" proxy in order to relay the PATs ECDSA Bitcoin signature to the Bitcoin network, again created using OP_RETURN. This can be hosted by the application developer, an IdP, Cloud Provider, IoT manufacturer or D-TA service provider -  either for 'free' or 'paid' service, depending on use case.

As for PATs finding the transaction identifier (txid) of the IdP or D-TA containing the signature of the hash of its Birth Certificate, I believe there are two choices:

1. The PATs, if constrained in memory or on iOS, will have to use the services of a Trusted Bitcoin Server proxy (running a full Bitcoin client) to obtain the transaction signature of the D-TA or IdP that is registered in the Blockchain, OR
2. Assuming size / memory permits - PATs will query the D-TAs and IdPs directly for the locations to the signature of the hash of the Birth Certificates in the Blockchain. The PATs will find these locations by interrogating the OpenID Connect metadata served by the D-TA's and IdP's.  As Satoshi writes, "[the thin client] can't check the transaction for himself, but by linking it to a place in the chain, he can see that a network node has accepted it, and blocks added after it further confirm the network has accepted it." If we take "X" to be the "number of blocks added after it", then SPV essentially trusts that a transaction X blocks deep will be costly to forge."

As an example, a thin client could get the 'live' ECDSA signature of the hash of the Birth Certificate hosted online, and validate its signature with the D-TA's public key, as well as getting the location of the same signature stored in the Blockchain. Assuming the signature of the hash verifies in both instances, and that the thin client can see that a network node has accepted the signature into the Blockchain, with several blocks added after it, this further confirms the network has accepted it and that the signature has not changed.

The 'Milagro PATs Software Stack' should be running the following software (developed by Milagro)
* very thin client capable of generating raw TX data and sending to Trusted Bitcoin Server proxy secured using some ECC scheme and capable of receiving Blockchain Birth Certificate signature data of IdP and D-TA from Bitcoin Server Proxy
* Milagro TLS with TLS 1.2 ciphersuites which include Milagro 'ECDH over Bitcoin / YAK over Bitcoin' ciphersuites

### PATs actions on install, initialisation
- Connect to Trusted Bitcoin Server proxy
- Obtain Trusted Bitcoin Server proxy's ECC public key to encrypt data being sent to it (which scheme? ECIES? ElGamal?)
- Create Bitcoin public / private key pair
- Create Birth Certificate, SHA256 digest of Birth Certificate and ECDSA signature of OP_RETURN transaction to be input into the Blockchain
- Generate AES 128 bit key
- Send all of the above (minus ECDSA private key) to the Trusted Bitcoin Server proxy (which will write it into Blockchain on behalf of PAT) secured using ECC scheme
- Receive instructions from Trusted Bitcoin Server proxy, encrypted with AES key received from PAT

NOTE: The Trusted Bitcoin Server proxy will monitor for the acceptance of the hash of PAT's Birth Certificate and ECDSA signature of the OP_RETURN transaction into the Blockchain. Once verified, the Trusted Bitcoin Server proxy will relay AES encrypted 'instructions' to the PAT. These instructions include:
- URLs of the D-TAs to obtain shares of keys from
- The D-TA's Birth Certificate ECDSA signatures from the Blockchain
- The IdP's (that serve the D-TA's) Birth Certificate ECDSA signatures from the Blockchain
- The Bitcoin transaction identifier (txid) where the PAT's ECDSA OP_RETURN transaction signature resides within the Blockchain

## Trusted Bitcoin Server proxy Software Stack (most likely run "as a Service" by MIRACL)
The Trusted Bitcoin Server (TBS) proxy is arguably the most important component within the ecosystem.  The TBS proxy is configured and administered by the application developer or device manufacturer. It is responsible for registering new devices onto the Blockchain, but also informing the new device which D-TA's and by extension IdP's it will be interacting with.

* a Server-side headless Blockchain client, capable of performing OP_RETURN (TBD) transactions on behalf of PATs - must have enough Bitcoin that enables transaction fees to be paid to miners for validating blocks containing its Proof-of-Existence (i.e. Birth Certificate), all PATs registering through it and subsequent Merkle roots containing audit data of who it registered, and in what time period
* Additionally, the Blockchain client will need to take input from an application developer or device manufacturer for the following parameters:
- URLs of the D-TAs to obtain shares of keys from
- The D-TA's Birth Certificate ECDSA signatures from the Blockchain
- The IdP's (that serve the D-TA's) Birth Certificate ECDSA signatures from the Blockchain
- The Bitcoin Transaction Locator (TX Record) where the PAT's ECDSA OP_RETURN transaction signature resides within the Blockchain
and must relay these securely to the PAT during its enrolment process
Additionally the TBS should be able to update the PAT in the field with instructions to:
- obtain new shares of keys from the same or different D-TAs

### TBSs actions on install, initialisation
- Connect to Bitcoin Network, download Blockchain
- Generate ECC key pair (as noted for operations above)
- Take input from admin (as noted above) for specific devices / regions, etc. through a web interface or API
- Find the D-TA's, IdP's and their transaction identifier (txid) on the Blockchain in order to copy their ECDSA signatures and relay these to PATs based on instruction set

# Secure Bootstraping

The Milagro ecosystem is intended to deliver to all participants the ability to securely bootstrap from a single ECDSA key generated on a device or application into a uniquely identified endpoint with cryptographic keys that exploit the feature set of Milagro's distributed cryptosystem.

Secure Bootstrapping in the Milagro ecosystem is achieved through clever exploitation of Bitcoin ECDSA digital signatures residing in the Blockchain, created from apps or things, as part of the initial setup of an app or initialisation of device.

In the IoT space, Milagro's secure bootstrapping aims to reduce the friction and cost of implementing security in devices by removing the need to build "secure key distribution" centres at the factory, replacing this process with a secure, streamlined process that enables secure key distribution at any point in a device's lifecycle.

These symmetric keys are burned-in to the device at manufacture. Each key is specific to each device and is shared in advance with the service. This is relatively simple and cheap, but it does require generating or storing keys securely, and holding them centrally.
With pre-shared keys, compromising one device only breaks security on that one device, which is good. But if some part of the manufacturing or key-storage chain is compromised (e.g. the factory) then all devices become compromised - often a concern for foreign cheap contract manufacturing.

This is achieved (site paper: Authenticated Key Agreement over Blockchain).
