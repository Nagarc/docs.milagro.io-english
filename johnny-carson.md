---
currentMenu: johnny-carson
layout: markdeep
---
<style>h1:before, h2:before, h3:before { content: none; }</style>
<div id="generated-toc" class="generate_from_h2" class="generate_from_h3"></div>

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

To realise our solution, we will use pairing-based cryptography. To be concrete we assume the use of a BN elliptic curve \cite{barreto-naehrig} at the AES-128 level of security. This is (and for our purposes must be) a type-3 pairing \cite{galbraith-paterson-smart}, where $e$: $G_1$ $\times$ $G_2$ $\rightarrow$ $G_T$.

The groups $G_1$, $G_2$ and $G_T$ are all of the same prime order $q$. We make standard pairing-based security assumptions, including the XDH assumption that the decisional Diffie-Hellman problem is hard in $G_1$.

First consider a simple protocol, in which a client tries to authenticate its identity to a server.

We assume that the server is authenticated to the client in a standard way, perhaps using the well known SSL protocol. Here $ID$ is the client identity and $H_1(.)$ is a hash function which hashes its input to a point on $G_1$.

This protocol attempts to prove in zero knowledge to the server that the owner of the claimed identity $ID$ is in possession of the value $sA$ issued to it by the TA, where $A=H_1(ID)$. The same TA has issued the secret $sQ \in G_2$ to the server, where $Q$ is a fixed public point in $G_2$.

Correctness follows immediately from the well known bilinearity property of the pairing. See Fig. 1 below.

<figure>
  <caption><strong>Figure 1.</strong> A Simple Authentication Protocol</caption>
</figure>

|Bitcoin sender|Merchant|
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

<figure>
  <caption><strong>Figure 2.</strong> The subliminal channel</caption>
</figure>
|Bitcoin sender|Merchant|
|:----------------------:|:----------------------:|
|Generates random $x<q$||
|$A=H_1(ID)$||
|$U=x{A}$||
|$V=-x{(s-\epsilon)A}$||
|$ID$, $U$, $V \rightarrow$||
| |$A=H_1(ID)$|
| |$g=e(V,Q).e(U,sQ)=e(U,Q)^\epsilon$|
| |Solve for $\epsilon$|

The way forward is now quite straightforward. The TA running at the Bitcoin exchange issues to the customer whose identity is proven to be $ID$ the secrets ($s-\epsilon_n$)$H_1(ID|n)$ where $\epsilon_n$ is $n$-th block of 4 digits of the CCN. This is done
for each of the 5 blocks of the CCN, for $n=$ 1 to 5. This now constitutes our ciphertext $E_s(CCN)$. On the server side $D_s=sQ$. To communicate the CCN to the merchant's server, we run the above protocol
5 times. In practice the 5 client to server communications can all be batched into a single blob of data, sharing the same time-stamp.
