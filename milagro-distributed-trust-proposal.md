---
currentMenu: milagro-distributed-trust-proposal
layout: markdeep
---
<style>h1:before, h2:before, h3:before { content: none; }</style>
<div id="generated-toc" class="generate_from_h2" class="generate_from_h3"></div>

## Establishing a Distributed Trust Ecosystem

## D-TA Software and Setup

We begin with the establishment of a Distributed Trust Authority service. In order for a D-TA to take hold, its Proof-of-Existence must be evidenced within the Blockchain itself. To register a D-TA service, software that provides Distributed Trust Authority services should ideally consist of
* an OpenID Connect client
* a Blockchain client, capable of performing Op_RETURN (TBD) transactions with enough Bitcoin that enables transaction fees to be paid to miners for validating blocks containing its Proof-of-Existence and subsequent Merkle roots containing audit data
* an D-TA Activity logger, which creates time bound Merkle roots ecompassing D-TA activity; essentially, a log of all key shares issued to people, apps and things, secured with one-way hashes
* Psuedo-random number generator with sufficient entropy
* TLS library for creating certificate-less secured connections driven by authenticated key agreements based upon the existence of ECDSA signatures between client and server or peer to peer. At least one of the signatures should be resident in the Blockchain, with enough time passing so that a re-write of the block housing the signature(s) becomes unlikely

The D-TA software, upon installation, creates its own Master Secret $s$ and a random element $F_q$. The D-TA software registers its existence using a cryptographic digest of the D-TA's **Birth Record**, linked to the time in which it submitted the record. In this way, the D-TA can publicly prove that it existed and was created without revealing the data, with a decentralized certification based on the bitcoin network.

The Birth Records is certified via embedding its SHA256 digest in the bitcoin blockchain. This is done by generating a special bitcoin transaction that encodes/contains the hash via an OP_RETURN script. This is a bitcoin scripting opcode that marks the transaction output as provably unspendable and allows a small amount of data to be inserted, which in our case is the Birth Record, plus a marker to identify all of its future transaction.

Once the transaction is confirmed, the document is permanently certified and proven to exist at least as early as the time the transaction was confirmed. If the document hadn't existed at the time the transaction entered the blockchain, it would have been impossible to embed its digest in the transaction (This is because of the hash function's property of being second pre-image resistant).
