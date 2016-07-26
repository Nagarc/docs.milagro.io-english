---
currentMenu: milagro-distributed-trust-proposal
layout: markdeep
---
<style>h1:before, h2:before, h3:before { content: none; }</style>
<div id="generated-toc" class="generate_from_h2" class="generate_from_h3"></div>

## Establishing a Distributed Trust Ecosystem

## Milagro D-TA Software Stack

We begin with the establishment of a Distributed Trust Authority service. In order for a D-TA to take hold, its Proof-of-Existence must be evidenced within the Blockchain itself. To register a D-TA service, a 'Milagro D-TA Software Stack' that runs Distributed Trust Authority services should ideally consist of
* an OpenID Connect client
* a Blockchain client acting as a headless Enterprise Bitcoin Server, capable of performing OP_RETURN (TBD) transactions with enough Bitcoin that enables transaction fees to be paid to miners for validating blocks containing its Proof-of-Existence (i.e. Birth Record) and subsequent Merkle roots containing audit data, and capable of acting as a Bitcoin Proxy for PAT's registering transactions and quering the Blockchain for the IdP and D-TA signatures
* an D-TA Activity logger, which creates time bound Merkle roots encompassing D-TA activity; essentially, a log of all key shares issued to people, apps and things, secured with one-way hashes
* Psuedo-random number generator with sufficient entropy
* TLS library for creating certificate-less secured connections driven by authenticated key agreements based upon the existence of ECDSA signatures between client and server or peer to peer. At least one of the signatures should be resident in the Blockchain, with enough time passing so that a re-write of the block housing the signature(s) becomes unlikely
* Distributed Hash Table client to perform a lookup of all IdPs registered in the ecosystem

The D-TA software, upon installation, creates its own Master Secret $s$ and a random element $F_q$ in addition to Bitcoin ECDSA public / private key pair. The D-TA software registers its existence using a cryptographic digest of the D-TA's **Birth Record**, linked to the time in which it submitted the record, using the OP_RETURN designation, signed by its ECDSA key. In this way, the D-TA can publicly prove that it existed and was created at a starting point, with a decentralised certification based on the bitcoin network.

The D-TA, through its ECDSA signature now resident in the Blockchain, has also created the cryptographic primitive that any actor on the system can use to bootstrap a secured connection to it (covered in following section).

The Birth Records is certified via embedding its SHA256 digest in the bitcoin blockchain. This is done by generating a special bitcoin transaction that encodes/contains the hash via an OP_RETURN script and the special designation of (WHAT?) in the transaction (tx) ID. This is a bitcoin scripting opcode that marks the transaction output as provably unspendable and allows a small amount of data to be inserted, which in our case is the hash of the Birth Record, plus a marker to identify all of its future transaction.

Finding the hashes of Birth Records in the Blockchain is made easier by looking for specific transactions in the bitcoin blockchain containing an OP_RETURN output with the Birth Records's hash prepended by a universal Milagro D-TA marker bytes, which are 0x444f4350524f4f46 (WHAT IS IT?? - this is proof of existence's marker bytes so must change to match 'Milagro D-TA' in ascii) (or 'Milagro D-TA' in ascii).

Once the transaction is confirmed, the hash of the Birth Record is permanently certified and proven to exist at least as early as the time the transaction was confirmed. If the D-TA's Birth Record hadn't existed at the time the transaction entered the blockchain, it would have been impossible to embed its digest in the transaction (This is because of the hash function's property of being second pre-image resistant).

The full Birth Record /*CAN BE* publicly hosted on web by the D-TA, which /*SHOULD be discoverable as a normative URL at every D-TA, similar to the additional [OpenID Provider Metadata parameter](https://openid.net/specs/openid-connect-discovery-1_0.html) so that individual actors in the ecosystem can create their own comparison hash of the Birth Record of a D-TA to ascertain if any data has changed. As an example, if a Distributed Trust Authority is forced into giving up its Master Secret because of legal issues, it could issue a canary warning through the Birth Record by changing it to notify the world at large that the D-TA's circumstances have changed.

### D-TA Actions on install and configuration
- Creates its own Master Secret $s$ and a random element $F_q$
- Create Bitcoin public / private key pair
- Create Birth Record
- Embed Birth Record's SHA256 digest in the bitcoin blockchain via an OP_RETURN script
- Host Birth Record, it's SHA256 digest, and tx (transaction locator - to find the signature in the blockchain) publicly online in normative location

OPTION 1: Integrate a solution like [Open Asset Protocol](https://github.com/OpenAssets/open-assets-protocol/blob/master/specification.mediawiki) or [Coinspark](http://coinspark.org/) to attach messages to the Bitcoin transactions which would carry the additional Birth Record information.

OPTION 2: Also investigate DHTs...

// NEED BIRTH RECORD FORMAT (JSON?)

## Milagro IdP Software Stack

The D-TA /*CAN* be configured to use an independent Identity Provider (IdP) through the OpenId Connect protocol, or will use its own private IdP which is solely in service to the corresponding D-TA. However, all IdP's in service to a publicly available D-TA */MUST offer the use the OpenID Connect federation protocol to the D-TA's.

To do this, the D-TA software will contain an OpenID Connect client capable of connecting to an IdP as a Relying Party.

A 'Milagro IdP Software Stack' will contain an IdP server which */MUST conform to OpenID Connect standards and support the following OpenID Connect endpoints:

* WebFinger — Enables dynamic discovery of the OpenID Connect provider for a given user, based on their email address or some other information.
* Provider metadata — JSON document listing the OP endpoint URLs and the OpenID Connect / OAuth 2.0 server features that it supports. Client apps can use this information to configure their requests to the OP.
* Provider JWK set — JSON document containing the provider’s public keys (typically RSA) in JSON Web Key (JWK) format. These keys are used to secure the issued ID tokens and other artifacts.
* Client registration — RESTful web API for registering client apps with the OP. Registration may be protected (require pre-authorisation) or open (public).
* Session management — Enables client apps to check if a logged in user has still an active session with the OpenID Connect provider. Also to facilitate logout.

The 'Milagro IdP Software Stack' should be running the following software (developed by Milagro)
* an OpenID Connect Server (see above)
* a Blockchain client, (which could also be a lightweight lightning client) capable of performing OP_RETURN (TBD) transactions with enough Bitcoin that enables transaction fees to be paid to miners for validating blocks containing its Proof-of-Existence (i.e. Birth Record) and subsequent Merkle roots containing audit data
* an IdP Activity logger, which creates time bound Merkle roots encompassing IdP activity; essentially, a log of all key shares issued to people, apps and things, secured with one-way hashes
* Psuedo-random number generator with sufficient entropy
* TLS library for creating certificate-less secured connections driven by authenticated key agreements based upon the existence of ECDSA signatures between client and server or peer to peer. At least one of the signatures should be resident in the Blockchain, with enough time passing so that a re-write of the block housing the signature(s) becomes unlikely

Whether the IdP offers protected registration (meaning a D-TA must register and be authorised to use its services) or the D-TA supports open registration, meaning any D-TA can connect, is beyond the scope of this document.

The IdP during its initial setup and configuration, will have performed some of the same actions as the D-TA setup. These are:

### IdP actions on install and configuration

- Create Bitcoin public / private key pair
- Create Birth Record
- Embed Birth Record's SHA256 digest in the bitcoin blockchain via an OP_RETURN script
- Host Birth Record, it's SHA256 digest, and tx (transaction locator - to find the signature in the blockchain) publicly online in normative location

Note that for the IdP, the additional [OpenID Provider Metadata parameter](https://openid.net/specs/openid-connect-discovery-1_0.html) */MUST be hosted online and discoverable as additional metadata through the OpenID Connect protocol.

### People / Apps / Things actions on initialisation

Any PAT with Milagro client code */MUST contain a 'thin' Bitcoin client which is a program that connects to the Bitcoin peer-to-peer (P2P) network but which doesn't fully validate all transactions or blocks. That is, it's a client to the full Bitcoin nodes on the network such as those running in the D-TA software stack.

Because Milagro is intended to solve issues for the IoT ecosystem, loading full Bitcoin clients on constrained device environments will not work.

Thus the 'thin' Bitcoin client */MUST be configured to use some service, pre-selected in advance by the application developer, as a "Trusted Bitcoin Server" in order to relay the PAT's ECDSA Bitcoin signature to the Bitcoin network, again created using OP_RETURN. This can be hosted by the application developer, an IdP, Cloud Provider or D-TA either for 'free' or 'paid' service.

The PATs will query the D-TAs and IdPs directly for the locations to the signature of the hash of the Birth Records in the Blockchain. The PATs will find these locations by interrogating the OpenID Connect metadata served by the D-TA's and IdP's.  As Satoshi writes, "[the thin client] can't check the transaction for himself, but by linking it to a place in the chain, he can see that a network node has accepted it, and blocks added after it further confirm the network has accepted it." If we take "X" to be the "number of blocks added after it", then SPV essentially trusts that a transaction X blocks deep will be costly to forge."

As an example, a thin client could get the 'live' ECDSA signature of the hash of the Birth Record hosted online, and validate its signature with the D-TA's public key, as well as getting the location of the same signature stored in the Blockchain. Assuming the signature of the hash verifies in both instances, and that the thin client can see that a network node has accepted the signature into the Blockchain, with several blocks added after it, this further confirm the network has accepted it and that the signature has not changed.
