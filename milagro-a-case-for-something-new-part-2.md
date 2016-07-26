---
currentMenu: milagro-a-case-for-something-new-part-2
layout: markdeep
---
<style>h1:before, h2:before, h3:before { content: none; }</style>
<div id="generated-toc" class="generate_from_h2" class="generate_from_h3"></div>

## Along Came the Blockchain

Banking is a great test-bed for the consideration of trust issues. The costs of (and rewards for) betrayal are high, and hence the need to evolve strategies to allow banking to flourish, as without banks and a trusted currency, commerce cannot flourish.

The traditional solution is a highly centralised hierarchical system, based on a per nation basis on a central bank which issues currency, and then the so-called pillar banks that look after day-to-day banking. So if we trust the central bank, all will be well. The wording on American bank notes ``In God we Trust'' surely sums up the apparent inevitability of the devolution of Trust to a single powerful entity.

But where there is money and the centralisation of power, there will be corruption and betrayal. Its not the Internet way.

In fact a partial alternative approach to solving trust issues in banking was always there, just never fully exploited. In Ireland we have what we call Credit Unions, as an alternative to the big centralised banks. They make a point of being based on the co-operative model. Trust is distributed amongst the customers of the credit union, who are also its owners.

What we are suggesting here is the extension of the co-operative trust model to the internet. Let us make the statement that ``we all own the internet'' a reality. In a co-operative environment things are organised so that trust flourishes because it is seen to work and betrayal is quickly detected and unlikely to result in any pay-off. That's the plan.

The block-chain provides an alternative distributed approach to managing a currency without the need for a central bank. Trust is distributed. ``In the block-chain we Trust'' may not have the same ring to it, but it works just fine.  And the block-chain cannot be subverted unless the majority of those involved betray trust and conspire together. So just how common are conspiracies?

Scott's law: No conspiracy can survive in a setting where anyone can join the conspiracy.

## The Future of Trust

So the block-chain represents a distributed trust solution for the E-Coin problem. But it doesn't end there. Other often simpler distributed trust solutions exist for other scenarios as well. The common thread is that trust should be distributed, although how it is done might vary in detail on a case-by-case basis.

A general approach to a solution suggests itself. Consider a setting where trust is distributed amongst multiple entities, and where any party can self-select as one of those entities, and where for a breach of trust to occur, all of the entities would need to conspire. Then apply Scott's law.

Starting from this ideal, let's work towards the practical. And to make it concrete let us consider the authentication scenario.

### Authentication Example

Let's say I need to be issued with a credential that would allow me to access a cloud-based service. The issuance of the credential should only occur if I can prove in some way that I am indeed entitled to it. The credential comes from adding together thirds delivered to me by three separate entities, (a) the service provider, (b) the cloud owner, and (c) an external provider.

One could even introduce the concept of an Identity Provider. An actor in the ecosystem that the issuers of the credential 'trust' to 'vouch' for the unique identity of the entity petitioning credential issuers for thirds of the credential after the entity seeking the credential has sufficiently proved the ownership of their unique identity. In fact, such systems exist already, operating at Internet scale. Login with Facebook, Google, Microsoft, etc. Application developers 'trust' these 'Identity Providers' (IdPs) and connect to their authentication systems via federation protocols like OpenID Connect.

One concern would be that my credential could in theory also be issued to some-one else should the Identity Provider be corrupted or simply get it wrong. Another concern is collusion of the credential issuers; However, unless all three entities conspire together to do this, or all three can be fooled into issuing my credential to the wrong person, then this cannot happen.

However, if each credential issuer trusts separate Identity Providers, and the chance of any single entity failing to do what they have been entrusted to do is 1 in 100, then the chance of an overall failure of trust is in this scenario could be 1 in 1,000,000. You get the idea.

So imagine a system whereby that CA-based PKI root of trust is replaced by a distribution of trust, which exhibits no single point of failure, and which is managed by a group of independent entities that do not necessarily trust one another, but at least one of which behaves honestly. At the same time we can take the opportunity to fix some of the other problems of classic PKI (no effective means of revocation, complex deployment for the individual user), and move to simpler identity-based methods, the mathematics of which naturally support this idea of distribution of trust.

## Distributed Trust Authorities

To make all this work a new type of Internet entity will be required -- a Distributed Trust Authority (D-TA).

They will be required to issue cryptographic part-secrets, and to protect their own part-secrets. They will be completely law abiding within their own individual jurisdictions. They will be expected to be open and transparent, and to have a reputation for honesty. But if they are villains it doesn't really matter, they can do no damage by themselves, and they will eventually be found out. As in all well designed co-operative systems, there is really no point in behaving badly.

Finally let us demonstrate that this is practical. Taking again authentication as an example consider a scenario in which a credential share is of the form $s_i.H(ID)$, where $s_i$ a large secret number randomly and independently generated by the Distributed Trust Authority $TA_i$, $ID$ is the recipients identity proven to the satisfaction of that $TA_i$, and $H(.)$ is a hash function which hashes identity to a point on an elliptic curve. The overall credential is $s_1.H(ID)+s_2.H(ID)+s_3.H(ID)+ ... + s_n.H(ID)$ if $n$ TAs are involved.

This is simple addition of points on an elliptic curve, and so the overall credential is $s.H(ID)$ where   $s=  s_0+s_1+s_2+ ... +s_n$. If just one of those shares is absent, its the same as having nothing. If $TA_i$ is hacked, then only $s_i$ is lost - the overall system remains secure. If some-one fools a TA or its chosen Identity Provider into issuing a secret for an undeserved identity, then that part-secret on its own is useless. No entity ever knows the master secret $s$. With new ideas from cryptography secret shares in this simple addable form are entirely possible (which is not the case for old-style crypto).

So let us move on and find more solutions based on the principal of Distributed Trust. The Blockchain has shown the way.

## A Summary of Distributed Trust

How do entities register their willingness to act as Distributed Trust Authorities, register what Identity Providers they will trust, and what is in it for them? Well they can do it for free, or for a fee. Probably the effort they put into carrying out their duties, and hence the amount of trust that can be assigned to their decisions, will be proportional to how much they are paid directly or indirectly.

So imagine a network of D-TAs that are available to support the distributed trust scenario outlined above. A practical question would be how to these D-TAs get established, where do I find one, and how do I establish its trustworthiness.

Here we outline a solution based on two ideas; the BlockChain and OpenID Connect federation.

Using [OpenID Connect Discovery][98], a person, app or thing could immediately find out OpenID Connect API URLs of Identity Providers that a Distributed Trust Authority has created a relationship with, and obtain other information required to securely identify a person, app or thing at its domain. The OpenID Connect Discovery spec is very simple. Just make an HTTPS GET request to https://<domain>/.well-known/openid-configuration.

This will return a JSON object with the URLs for the API’s of the IdP, and other information the client will need, like what kind of cypto is supported, and what kind of authentication is available. If you want to see an example of an OpenID Connect Discovery response, check out Gluu’s OpenID Connect discovery page: https://idp.gluu.org/.well-known/openid-configuration

Note that there is no reason, theoretically, a Distributed Trust Authority could not enlist the services of its own Identity Provider. In many cases, such as a D-TA operated by enterprise, this may be an ideal setup.

Once the person, app or thing has validated its identity to an IdP, it can be handed a cryptographically secured token, which it can submit to an Distributed Trust Authority over a secured channel. This token is exchanged for an OpenID Connect ID Token, which reveals to the D-TA the identity by which to issue its share of a credential.

A couple of other practical matters need to be resolved. First we need to establish a D-TA's URL and IP address so that it can be found on the internet, and secondly each D-TA, and indeed each Identity Provider, needs to have a universal mechanism by which it can support actors in the ecosystem (a person, app or thing) creating a secured connection to it.

Now a very hot topic of debate in the BlockChain community is its potential application to problem domains outside of supporting a cryptocurrency. One of the simplest ideas is to use a Blockchain as a simple Proof-of-Existence of certain data on a certain date. Simply pop the ECDSA digitally signed time-stamped data (or more correctly a hash of the data) into a Blockchain. Once accepted it becomes part of the ledger and cannot be changed.

Recently, Bitcoin's Blockchain has implemented the Segregated Witness upgrade, which enables a Bitcoin client to merely sign a transaction hash, index, and value (and told what public key was used), to safely sign the spending transaction, no matter how large or complicated the transaction being spent was. These capabilities, along with the fix for transaction malleability, enable a new generation of capability which Milagro will exploit.

Using the OP_RETURN scripts, it is possible for a Distributed Trust Authority to create a record of its birth by inserting data into the Blockchain including time of creation, its IP address, list of IdPs it relies on, even information that enable its service to be obtained via smart contracts.

Further, the digitally signed transaction can itself service as a cryptographic primitive that enables non-interactive or interactive key exchange against other actors in the ecosystem who have also created Proof-of-Existence records using ECDSA signatures. (site paper) This becomes the basis of a universal secure bootstrapping mechanism whereby any person, app or thing with a Bitcoin private key used to sign a transaction within the Blockchain can securely connect to any other actor who has made a similar Proof-of-Existence within the Blockchain.

As an example, a simple non-interactive Elliptic Curve Diffie-Hellman key agreement can be established to drive a TLS-PSK session between a client (person, app or thing) seeking to obtain a share of an identity based key from a Distributed Trust Authority after having verified its identity to an IdP.

Lastly, each Distributed Trust Authority should, as a matter of establishing its trustworthiness, create a record of its activity so that each person, app or thing that relies on this D-TA can easily audit and verify that the Distributed Trust Authority has not gone rouge and issued a key in its identity without its consent. Not that this is a far too often occurrence with Certificate Authorities, hence the establishment the Certificate Transparency project.

A solution to this issue can be achieved without having to overload the Blockchain with extraneous data. This is done through the use of Merkle Hash Trees and activity logs (cite Chainpoint paper). To record data in the blockchain, we start by using a standard hashing function such as SHA­256 to generate a unique hash of the target data, such as the ID that the key was issued in the ID of and date / time period for which it was issued.

Multiple hashes are assembled into a block, which is simply a list of hashes. Periodically (once per hour), these blocks are used to generate a cryptographic primitives known as a Merkle Trees [4], and the Tree's 'Merkle Root' is published in blockchain via a transaction using the OP_RETURN script. By collating multiple hashes into a Merkle Tree and publishing the Merkle Root, we can record large volumes of D-TA activity logs in the blockchain using a single transaction.

In the real world, a receipt provides proof of a transaction. A D-TA activity log provides proof that it was requested by a IdP to issue a share of a key in a specific identity at a specific time. It contains all the information needed to prove an individual hash was part of the Merkle Tree whose root was published in a transaction in the Blockchain.

By tracing a path from the Merkle root to the target hash, we can generate a Merkle Proof that proves any one of the elements is in the Merkle tree, without having to know the entire tree. These elements can be used to create a D-TA activity log that contains, at minimum, the Target Hash, Merkle Proof, Merkle Root, and Bitcoin Transaction ID.

This system enables a person, app or thing to verify a receipt by checking a Bitcoin transaction and using math to verify the data. At any point, any actor can peruse the Blockchain looking for evidence of a rouge issuance of a share of a key in its identity.

The Blockchain becomes a shared identity database in which multiple entities validate different aspects of a people, app or things identity. Although each such certification stands alone, the blockchain provides a useful way to bring everything together in a unified way that can add layers of trust and experience to each particular entity in the ecosystem.

These ideas and concepts are further explored in the following section.

Next section: [A Distributed Trust Proposal](milagro-distributed-trust-proposal.html)
