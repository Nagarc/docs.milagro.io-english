---
currentMenu: protocol-extensions
layout: markdeep
---
<style>h1:before, h2:before, h3:before { content: none; }</style>
<div id="generated-toc" class="generate_from_h2" class="generate_from_h3"></div>

Introduction
---
In this section we introduce the concept of Milagro Extensions, which are components of additional functionality that is enabled within the Milagro framework on the basis of base protocols and architecture exploiting pairing cryptography and zero knowledge proofs.

Some of this is complex; it involves novel interactions and pairing cryptography. Issues of who-owns-what arise, and the reader must become familiar with some new acronyms. Given these constraints we aim to be as clear and unambiguous in our description as we possibly can be.

## Multi-Factor Authentication

### Current State-of-the-Art

The M-Pin Protocol, which is one of two main protocols within the Milagro Framework, was written to replace the well-known Username/Password authentication mechanism, which is widely considered to be effectively broken.

The main problem is the existence of a **password file** on the server, which is commonly stolen and hacked, revealing most user passwords.

Many two-factor solutions are in fact often hierarchical and two-level. A key generated from one factor is used to unlock the other, the FIDO alliance protocol is one such solution.

Disjointed technologies are used by each factor. Typically a password (or a biometric) might be used to unlock an authentication key stored in a file.

Strictly speaking, this solution is only one factor, as it is only this authentication key that is required, and an attacker would be satisfied if they could obtain this without knowing the password.

However since this is probably not possible, we accept that the overall effect is two-factor authentication.

Software encryption might be used as the locking mechanism, but since a brute force attack will discover the authentication key, the password must become a large hard-to-remember pass-phrase.

The alternative is to lock the authentication key into a secure hardware vault. Now a short PIN can be used to unlock it.

However, secure hardware is expensive and may not be supported on all devices. Another downside of this approach is that the extension to multi-factor authentication is not at all obvious.

### Milagro Multi-Factor Authentication

The main concepts behind Milagro MFA are that each registered client is issued with a cryptographic identity based encryption key. They then prove to a server that they are in possession of this key using a zero-knowledge proof protocol, which can be extended to include authenticated key agreement.

This protocol design eliminates the need for any information related to clients, or their keys, to be kept on the authentication server.

The other cornerstone concept exploits bilinearity. Common to keys (issued for use in a Type 3 paring) is that the keys can be issued in fractions, not as whole keys, by Milagro Distributed Trust Authorities.

Only the clients, who receive the fractions from various D-TA's, will ever know the completed whole keys.

In the same way that Milagro keys can be issued in fractions, or shares, Milagro keys may also be safely split up into any number of independent factors.

Each of these factors has the same form; they are points on an elliptic curve. To recreate the original secret, they are simply added together again -- ***it's as simple as that***.

One factor might be derived from a short 4-digit PIN. Another might be a *token* conveniently stored in an authenticator app on a smartphone. Another factor might be geo-location.

This idea is that a PIN number α can be securely extracted by the client from their key, to create an inert 'token'. Our two factors of authentication are then this memorised PIN and the token.

To be explicit, for an individual Alice whose identity hashes to a point $A \in G1$, her full secret as issued by the D-TA's is the combined shares of keys from to create point $sA$.

This is split into the token $(s−\alpha)A$, and the chosen PIN number $a$. The token is created by calculating αA and subtracting it from sA. The full secret can be reconstructed from its two components by Alice as sA = (s − α)A + αA.

In order for a client to authenticate against a Milagro MFA server, its client key must be re-constructed to sA = (s − α)A + αA and in this simple example it is achieved by combining the token stored on the device (something the client has) with the input PIN (something the client knows).

### 3rd Factor using Geo-Location (Example)

Geo-location as an additional 3rd authentication factor can be advantageous to both the server and the client. It limits the locations from which a client can successfully authenticate to a server.

The server can be sure that even a valid client who is outside of the permitted area cannot successfully log in, and the client can be sure that if their device is stolen it cannot be used away from their place of work. It adds an extra factor to the authentication process.

However we should be aware that location can always be faked by the well equipped attacker. System calls to the GPS hardware can be intercepted, and false coordinates passed to the application. Therefore as an extra factor, location has limited value unless it is combined with other factors.

When the client registers they choose (or have chosen for them by one of the D-TA's) a location that will be at the centre of a square area outside of which they will not be able to authenticate. The size of this area (the length of the side of the square) is also chosen.

An offset to be added to the GPS coordinates in order to centre this location in a square, and also so that the longitude and latitude of the bottom left hand corner (BLHC) can be represented as whole numbers, is stored on the device, as is a scaling value depending on the length of the side of the square.

Loosely speaking the $(x, y)$ coordinates of the BLHC of the square can be subtracted from the client secret by the Customer DTA, before the secret is issued. Alternatively this can be done by the client themselves.

Then when the client authenticates the GPS on the device is accessed, the BLHC of the square the device is in is calculated, and added back to recreate the original secret.

Recall that the client secret is of the form $sA$, where $A$ is the identity of the client hashed to a point on an elliptic curve, and $s$ is the overall TA master secret (created from the three independent D-TA's).

We suggest that the location is embedded in this secret by replacing the stored client secret with $sA-(2^{32}x+2^{64}y)A$.

These offsets are chosen to ensure that there is no interaction with a PIN number which may also be subtracted from the client secret.

When the time comes to authenticate, the GPS hardware is accessed, and the $(X,Y)$ coordinates retrieved.

These are used to add back to the client secret $(2^{32}X + 2^{64}Y)A$ so it becomes $sA - (2^{32}x + 2^{64}y)A + (2^{32}X + 2^{64}Y )A$, which obviously becomes $sA$ only if $x = X$ and $y = Y$.

Assume that the client registers their device at latitude 13.06278, longitude 80.22946. Now a 0.01 difference in either longitude or latitude is roughly 1000 meters. Assume that the client is expected to be within a 1 kilometer square, which is centred on this initial point of registration.

We calculate the offset as (.00222,-.00446), which when added to the latitude/longitude centers the client in its square. This offset is stored and the $(x,y)$ coordinates are converted to integers by simple truncation as (1306,8022) and these values are used to modify the client secret as described above.

Now when for example the client authenticates from the location latitude 13.06567, longitude 80.23127, the offset is added to this to get latitude 13.06789 and longitude 80.22681.

This is truncated to the integer coordinates (1306,8022), and since these are the same as before, they will cancel out the modification to the secret, to restore the original secret $sA$, which can then be used to successfully authenticate.

The stored offset does not leak anything useful, as it represents a small shift relative to the registration location, which will not be known to an attacker who has stolen the device. In the Milagro MFA tradition nothing related to client location is stored on the server.

The registration location can either be enforced by the Customer via the D-TA under its control. Or it can be found from the client's device location at the moment of registration, by accessing its GPS hardware.

The latter is certainly simpler. There are lots of code examples out there on accessing the GPS hardware from IOS and Android for the developer to explore further.

## Real Time Revocation of Client Keys using ___Time Permits___

We introduce Time Permits to handle the revocation issue. Normally in Identity-Based Encryption the problem of client revocation is solved by date-stamping identities so that the private key issued for an identity becomes useless once the time period expires. Now a new private key must be issued, and we will simply not issue one to a revoked client.

Milagro achieves a much more immediate revocation capability through the use of Time Permits. The D-TA that is controlled by the application owner is envisioned to be the controlling D-TA to issue Time Permits at the point where a client needs to authenticate to a server, or create an authenticated key agreement between client and server or peer to peer.

The idea is that the server includes an explicitly described time slot in its construction of Alice's hashed identity. Unless Alice has a corresponding ``Time permit'' for the same time slot, she cannot complete the protocol.

In the protocol above we instead calculate $H(ID_a) + H_T(T_i|ID_a)$ on both sides of the protocol where $T_i$ is a textual description of the $i$-th time slot and $H_T(.)$ is a hash function distinct from $H(.)$.

For the protocol to work correctly Alice must be issued by the Trusted Authority with a permit $s.H_T(T_i|ID_a)$ which gets added to her combined PIN-plus-token secret $s.H(ID_a)$.

Observe that the permit is of no use to any other party, and hence can be issued publicly, or simply sent to Alice by email, or delivered via the server.

A proof of security for this idea in the context of Boneh and Franklin IBE can be found in \cite{tseng-tsai}.

## The Johnny Carson Protocol: Trustless Channels for the Blockchain

The Bitcoin network has been running at full capacity for the past six months (as of 20 June 2016) due to demand seemingly surpassing an artificial transaction cap of approximately 250,000 transactions a day or around 2-2.5 transactions a second.

Tens of thousands of transactions and hundreds of thousands of bitcoins continue to be stuck for hours or days. A large percentage of the transactions on the Blockchain occur between parties that have transacted more than once.

Creating Trustless Channels for the Blockchain that are widely accepted and enable any two or more parties to repeatedly transact together without adding to the transaction count of the Blockchain directly could dramatically reduce the transaction confirmation latency.

We define an acceptable Trustless Channel as a medium where one party can send bitcoins to any other party securely, with instant confirmation, without adding to the transaction count of the blockchain.

### Why Johnny Carson?

As the long time host of the Tonight in the USA, Johnny Carson often appeared in the spoof role of Carnac the Magnificent, a mentalist who could magically read the contents of a sealed envelope. This is in fact a well known stock-in-trade trick of the mentalist's craft, known as ``billet reading''.

Here we propose a cryptographic solution to the problem of billet reading, apparently allowing a ciphertext to be decrypted without direct knowledge of the ciphertext, and present both a compelling use case and a practical implementation to reduce the transaction delays on the Blockchain.

### The solution

Assume a BitCoin sender wants to carry BitCoin private keys around on his mobile phone, but stored in an encrypted form that is tied to his identity using a smartphone app built with Milagro MFA client SDKs. We call this the Ciphertext. However no encryption or decryption keys are available to the Bitcoin sender to decrypt their BitCoin private keys.

This smartphone app does not enable the BitCoin sender to either encrypt BitCoin private keys for anyone else, or indeed decrypt his own Ciphertext (BitCoin private keys). Further, we will show that the Ciphertext itself can be secured cryptographically against illegitimate or fraudulent transactions through the use of a simple 4 digit pin number that results in security to a 128-bit level.

In other words, in order to action a transaction cryptographically, both the Ciphertext (something the app / BitCoin sender has) and 4 digit pin (something the BitCoin sender knows) must be correct in order to create the transaction.

At some point the BitCoin sender decides to send BitCoin to another party. Let's use an online merchant as an example. The merchant knows nothing about the owner of the BitCoin, and has nothing stored locally related to the amount of the BitCoin .

The BitCoin sender wants to enter into a protocol with the merchant using the Ciphertext to send Bitcoin to the merchant. Ideally:

- (a) the BitCoin sender must correctly two-factor authenticate (having the right Ciphertext and PIN) to the merchant in order for the Bitcoin key to be revealed to the merchant, and
- b) the merchant learns nothing about the Ciphertext and PIN (lest a dishonest merchant should use the Ciphertext for their own purchases) during the authentication session, but nonetheless
- (c) the merchant is able to determine the BitCoin private key and the associated authenticated identity of its owner from a successful authentication session.

An immediate objection might be that in this scenario a stolen Ciphertext is as good as the Bitcoin private key, as it can clearly be used to make purchases from the merchant. Later we shall show how, in a practical implementation, the Ciphertext can be adequately protected just using a short PIN number. Using a PIN number to protect credit card transactions is a well known and trusted mechanism, and the same familiar PIN can be used here.

A trusted authority (TA) is involved, probably belonging to a Bitcoin exchange, to encrypt the BitCoin private key and create the Ciphertext. Assume that this TA is known to both the Bitcoin sender and the merchant. The TA has its own master key $s$.

The Bitcoin sender approaches the TA who encrypts the Bitcoin private key using the encryption key $s$ to create the Ciphertext $E_s(CCN)$, which is given to the Bitcoin sender. Note that it is not essential that the Bitcoin sendder actually knows their Bitcoin private key at all. The TA also issues to the merchant a value $D_s$, derived from $s$, but from which $s$ cannot be extracted.

The idea now is that the Bitcoin sender should be able to enter into a protocol with the merchant, using $E_s(CCN)$, such that the merchant ends up knowing the Bitcoin private key and the identity of its owner, but in the process learns nothing about
$E_s(CCN)$.

By analogy the merchant is able to magically determine Bitcoin private key without touching the ``sealed envelope'' that is $E_s(CCN)$. The trick is (and there has to be a trick!) is that the mentalist/merchant has in their possession the apparently unrelated secret $D_s$.

The mini private key format is a method of encoding a Bitcoin private key in as few as 30 characters so that it can be embedded in a small space. For the purposes of this proposal we assume that a Bitcoin mini private key consists of 8 blocks of 4 decimal digits each (32 characters).

To realise our solution, we will use pairing-based cryptography. To be concrete we assume the use of a BN elliptic curve \cite{barreto-naehrig} at the AES-128 level of security. This is (and for our purposes must be) a type-3 pairing \cite{galbraith-paterson-smart}, where $e: \G_1 \times \G_2 \rightarrow \G_T$.

The groups $\G_1$, $\G_2$ and $\G_T$ are all of the same prime order $q$. We make standard pairing-based security assumptions, including the XDH assumption that the decisional Diffie-Hellman problem is hard in $\G_1$.

First consider a simple protocol, in which a client tries to authenticate its identity to a server.

We assume that the server is authenticated to the client in a standard way, perhaps using the well known SSL protocol. Here $ID$ is the client identity and $H_1(.)$ is a hash function which hashes its input to a point on $\G_1$.

This protocol attempts to prove in zero knowledge to the server that the owner of the claimed identity $ID$ is in possession of the value $sA$ issued to it by the TA, where $A=H_1(ID)$. The same TA has issued the secret $sQ \in \G_2$ to the server, where $Q$ is a fixed public point in $\G_2$.

Correctness follows immediately from the well known bilinearity property of the pairing. See Fig. 1 below.

<figure>
  <caption><strong>Figure 1.</strong> A Simple Authentication Protocol</caption>
</figure>

|Client|Server|
|:----------------------:|:----------------------:|
|Generates random $x<q$||
|$A=H_1(ID)$||
|$U=x{A}$||
|$V=-x{sA}$||
|$ID$, $U$, $V \rightarrow$||
| |$A=H_1(ID)$|
| |$g=e(V,Q).e(U,sQ)$|
| |if $g \ne 1$, reject ~|

As an authentication protocol this has some obvious deficiencies (for example it is subject to a simple replay attack). These deficiencies are addressed in further sections, but for now this serves as a foundation to illustrate the solution. Next we introduce a small error $\epsilon$ into the client's secret $sA$. See Fig 2. below.

|Client|Server|
|:----------------------:|:----------------------:|
|Generates random $x<q$||
|$A=H_1(ID)$||
|$U=x{A}$||
|$V=-x{(s-\epsilon)A}$||
|$ID$, $U$, $V \rightarrow$||
| |$A=H_1(ID)$|
| |$g=e(V,Q).e(U,sQ)=e(U,Q)^\epsilon$|
| |Solve for $\epsilon$|

## Secure Bootstraping