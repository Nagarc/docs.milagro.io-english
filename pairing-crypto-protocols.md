---
currentMenu: pairing-crypto-protocols
layout: markdeep
---
<div id="generated-toc" class="generate_from_h2"></div>
<style>h1:before, h2:before, h3:before { content: none; }</style>

<!--- <div class="abstract">
<span class="footnote">
Note: This document uses sections from the MIRACL Labs M-Pin Full Paper, published in 2015.<p></p>MIRACL Ltd, along with NTT Labs and NTTi3, are the originators of the Milagro Project. The original LaTex authored PDF version is available for download <a href="docs.milagro.io/mpinfull.pdf">here</a>.</span></p>
</div>
--->

## M-Pin Protocol - Introduction

The genesis of the M-Pin Protocol was first put forward in a research paper by [Dr. Michael Scott](https://scholar.google.com/citations?user=GsM-aeEAAAAJ&hl=en) in 2002 <a href="#Scott1">2</a>.

The M-Pin Protocol has been iterated on several times over the years since, to develop three distinct modes, which will be explored in the following sections.

The M-Pin Protocol is intended to replace the well-known Username/Password authentication mechanism which is widely considered to be effectively broken.

The main problem is the existence of a **password file** on the server, which is commonly stolen and hacked, revealing most user passwords.

The idea behind M-Pin is that each registered client is issued with a cryptographic identity based encryption key. They then prove to a server that they are in possession of this key using a zero-knowledge proof protocol, which can be extended to include authenticated key agreement.

This protocol design eliminates the need for any information related to clients, or their keys, to be kept on the authentication server.

Common to both Chow-Choo and M-Pin is that the keys are issued in fractions, not as whole keys, by the Distributed Trust Authorities. Only the clients, who receive the fractions from various D-TA's, will ever know the completed whole keys.

Industry commentators have long advocated a multi-factor solution. The novel feature of M-Pin and Chow-Choo is that the cryptographic secrets issued to clients or peers may be safely split up into any number of independent factors.

Each of these factors has the same form; they are points on an elliptic curve. To recreate the original secret, they are simply added together again -- ***it's as simple as that***.

One factor might be derived from a short 4-digit PIN. Another might be a *token* conveniently stored in an authenticator app on a smartphone.

Classic two-factor solutions are in fact often hierarchical and two-level. A key generated from one factor is used to unlock the other.

Disjointed technologies are used by each factor. Typically a password (or a biometric) might be used to unlock an authentication key stored in a file.

Software encryption might be used as the locking mechanism, but since a brute force attack will discover the authentication key, the password must become a large hard-to-remember pass-phrase.

The alternative (which achieves the same functionality as two-factor M-Pin) is to lock the authentication key into a secure hardware vault. Now a short PIN can be used to unlock it.

However, secure hardware is expensive and may not be supported on all devices. Another downside of this classic approach is that the extension to multi-factor authentication is not at all obvious.

 As noted in [Milagro Crypto Concepts](milagro-concepts.html), the M-Pin Protocol is of these classifications and exploits the features of:
* Elliptic Curve Cryptography
* Pairing Based Cryptography
* Identity Based Encryption
* Zero Knowledge Proof

Because of the characteristics that M-Pin inherits from the four techniques above, the M-Pin Protocol and its variants are able to deliver:
* Multi-factor authentication (MFA) using Zero Knowledge Proof
* Authenticated Key Agreement
* Distribution, or splitting, of Trust Authorities
* [Subliminal Channel Communication](https://en.wikipedia.org/wiki/Subliminal_channel)<a href="#scott-spector">3</a>

The three modes of operation of the M-Pin Protocol are as follows:
* **M-Pin 1-pass**: Client to server authentication via digital signature, this mode implements a *non-interactive* zero knowledge proof and is resistant to [MITM (man in the middle)](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) attacks.
* **M-Pin 2-pass**: Client to server authentication via a *interactive* zero knowledge proof, resistant to [MITM](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) and [KCI (Key Compromise Impersonation)](https://kcitls.org) attacks.
* **M-Pin FULL**: Mutual client to server authentication via a *interactive* zero knowledge proof, resistant to MITM and KCI attacks and able to drive an Authenticated [Key Agreement](https://en.wikipedia.org/wiki/Key-agreement_protocol) between client and server, resulting in 128 bit shared secret key.

Note that the M-Pin Full Authenticated Key Agreement possesses the quality of [perfect forward secrecy (PFS)](https://en.wikipedia.org/wiki/Forward_secrecy), meaning, even if the client and server long term keys are compromised, the past session keys (used to encrypt TLS traffic, for example) are not compromised.

## Chow-Choo Protocol - Introduction

The Chow-Choo Protocol was developed by Sherman S.M. Chow and Kim-Kwang Raymond Choo and published in 2007 via a research paper titled Strongly-Secure Identity-based Key Agreement <a href="#chow-choo">4</a>.  The Chow-Choo Protocol can be technically described as an identity-based key agreement protocol.

The Chow-Choo Protocol is of these classifications and exploits the features of:
* Elliptic Curve Cryptography
* Pairing Based Cryptography
* Identity Based Encryption

Because of the characteristics that Chow-Choo inherits from the three techniques above, the Chow-Choo Protocol can deliver:
* Multi-factor authentication (MFA) using Zero Knowledge Proof
* Authenticated Key Agreement
* Distribution, or splitting, of Trust Authorities

Note that the Chow-Choo Protocol is not a Zero Knowledge Proof protocol, and is not able to deliver a Subliminal Channel capability.

---

<figure>
  <caption><strong>Table 1.</strong> PROTOCOL RECOMMENDATIONS</caption>
</figure>
<markdeep>
Protocols | Use Cases
-------|-------
M-Pin 1-Pass | Digital signature authentication in battery or bandwidth constrained environments such as IoT devices, embedded applications and mobile apps. <br>This should be considered the default implementation for client to server authentication suitable for almost all use cases.
M-Pin 1-Pass + <br>M-Pin 2-Pass | Digital signature and client to server authentication in smartphones apps, desktop browsers and software applications.
M-Pin 2-Pass | Client to server authentication in smartphone apps, desktop browsers and software applications.
M-Pin FULL | Mutual client and server authentication with authenticated key agreement for use in smartphone apps, hardware and software applications. <br>Authenticated Key Agreement with PFS can be used as key exchange algorithm in TLS-Handshake sessions between clients and servers.
Chow-Choo | Mutual peer to peer authentication with authenticated key agreement for use in smartphone apps, hardware and software applications. <br>Authenticated Key Agreement with PFS can be used as key exchange algorithm in TLS-Handshake sessions between clients and servers and peer to peer.
</markdeep>

---

## Protocols In Depth

The Milagro framework protocols rely on Distributed Trust Authorities to issue shares, or fractions, of Type-3 Pairing keys to Milagro Crypto Apps, such as the Milagro MFA server and clients, or to software or hardware applications that have embedded Milagro code in order derive the functional capabilities.

These clients or peers become the only entities that know the completed whole keys assembled from shares (fractions) issued by different Distributed Trust Authorities.

As outlined in the previous section, Type-3 pairings were selected as they are the most efficient pairing and will work with non-supersingular pairing-friendly curves.

These curves can be constructed to be a near perfect fit at any required level of security <a href="#freeman-scott-teske">1</a>.

One of the novel aspects of pairing-based cryptography is that deployed secrets are commonly represented as points on an elliptic curve, which are the result of multiplying a known point by a master secret $s$.

So for example a secret might be of the form $sP$, where $P$ is known.

There are a number of interesting things we can do with secrets that have this form, that are not possible with the secrets that arise when using other cryptographic technologies.

For example they can be split into two, into $s_1P$ and $s_2P$ where $s=s_1+s_2$ and $sP = s_1P +s_2P$.

In fact they can be just as easily split into multiple parts, just like <a href="url" target="_blank">chopping up a cucumber</a>.

We can also add extra components to create a secret of the form $s(P_1+P_2) = sP_1+sP_2$.

It is the flexibility that arises from this form of the secret that allows us to introduce the idea of chopping off a tiny sliver of the secret to support a PIN number.

It also facilitates the concept of *Time Permits* as discussed in a later section.

Lastly, it enables Distributed Trust.

### Distributed Trust Authorities

A Trusted Authority will be in possession of a master secret $s$, a random element of $F_q$.

A client secret is of the form $s.H(ID)$, where ID is the client identity and $H(.)$ a hash function which maps to a point on $G_1$.

From prior art, we assume that $H$ is modelled as a random oracle where $H(ID) = r_{ID}.P$

where $r_{ID} \in F_q$ is random and $P$ is a fixed generator of $G_1$.<a href="#smart-vercauteren">6</a>

The server will be issued with $sQ$, where $Q$ is a fixed generator of $G_2$.

Note that this will be the only multiple of $s$ in $G_2$ ever provided by the TA. Servers will always be associated with their own unique master secrets.

Note that the TA functionality can be trivially distributed using a secret sharing scheme, to remove from the overall system a single point of compromise or coercion.

In the simplest possible case there may be two Distributed Trusted Authorities (D-TAs), each of which independently maintains their own share of the master key.

So $s=s_1+s_2$, and each D-TA issues a part-client key to the client $s_1 H(ID)$ and $s_2 H(ID)$, which the client, after receiving the shares, adds together to form their full key.

Now even if one D-TA is compromised, the client key is still safe.

NOTE: As discussed in the <a href="url" target="_blank">Distributed Trust Ecosystem Proposal</a>, the Milagro Project has put forward a proposal to create an ecosystem whereby any participant can run independent Distributed Trust Authority services.

### M-Pin 1-Pass

As opposed to Chow-Choo, which can be used in a client to server as well as a peer to peer setting, M-Pin is strictly a client-server protocol.

To embellish the security of the client-server protocol, it is important that client and server secrets should be kept distinct.

A simple way to do this is to exploit the structure of a Type-3 pairing and put client secrets in $G_1$ and the server secret in $G_2$.

For a Type-3 pairing there is assumed to be no computable isomorphism between these groups, even though both are of the same order.

In the original implementation, the client was supplied with a challenge by the server as part of the second step within the protocol, after the first step whereby the client announced her identity to the server.

In a later proposal, it was realised that an M-Pin 1-Pass Protocol could be obtained if the client itself derived the challenge as $y$ as $y=H(U|T)$ where $T$ is a time-stamp transmitted by the Client along her claimed identity, $U$ and $V$.<a href="#m-pin-ietf">5</a>.

The protocol could then be reduced in an obvious way to a secure 1-pass protocol. However, this assumes that the Server checks the accuracy of the time-stamp before completing the protocol.

This all works thanks to the pairing function $e(.,.)$ and its remarkable bilinearity property $e(aP,Q) = e(P,aQ) = e(P,Q)^{a}$.
<br></br>

---

<figure>
  <caption><strong>Figure 1.</strong> M-Pin 1-Pass</caption>
</figure>

|Alice - identity $ID_a$|Server|
|:----------------------:|:----------------------:|
|Generates random $x<q$||
|$A=H(ID_a)$||
|$U=x{A}$||
|$ID_a$, $U~~ $||
|$y=H(U\|T)$ ||
|$V=-(x+y){((s-\alpha)A+\alpha A)} \rightarrow$||
| |$A=H(ID_a)$|
| |$g=e(V,Q).e(U+yA,sQ)$|
| |if $g \ne 1$, reject the connection|

---

### M-Pin 2-Pass

As you can see below in Fig 2., M-Pin in the two pass operation operates in a challenge (from the Server) to client, who responds to challenge. This implementation obviates the any risk of Key Compromise Impersonation attack vector, at the cost of of a full roundtrip.

---

<figure>
  <caption><strong>Figure 2.</strong> M-Pin 2-Pass</caption>
</figure>
|Alice - identity $ID_a$|Server|
|:----------------------:|:----------------------:|
|Generates random $x<q$|Generates random $y<q$|
|$A=H(ID_a)$||
|$U=x{A}$||
|$ID_a$, $U~~ \rightarrow  $||
| |$\leftarrow y$|
|$V=-(x+y){((s-\alpha)A+\alpha A)} \rightarrow$||
| |$A=H(ID_a)$|
| |$g=e(V,Q).e(U+yA,sQ)$|
| |if $g \ne 1$, reject the connection|

---

### M-Pin FULL

This more elaborate protocol not only replaces Username/Password, but replaces the functionality of digital certificates being utilised to drive key agreement for TLS or VPN protocols as well.

Our starting point is the M-Pin protocol as described above.

The idea is to run it first (to authenticate the client to the server), and then proceed to authenticate the server to the client via an authenticated key exchange, which also establishes the agreed key of 128 bits.

The first thing to note is that both the client and the server can already calculate a mutual authenticated encryption key!

This protocol requires another general hash function $H_g(.)$ which serializes, and hashes its input to a 256-bit value. Both sides can then extract a key from this value $K$.

Note that since the first part of the protocol is just the original M-Pin protocol, all of its features and extensions still apply.

---

<figure>
  <caption><strong>Figure 3.</strong> M-Pin FULL</caption>
</figure>
|Alice - identity $ID_a$|Server|
|:----------------------:|:----------------------:|
|Generates random $x<q$|Generates random $y<q$|
|$A=H(ID_a)$||
|$U=x{A}$||
|$ID_a$, $U~~ \rightarrow  $||
| |$\leftarrow y$|
|$V=-(x+y){((s-\alpha)A+\alpha A)} \rightarrow$||
| |$A=H(ID_a)$|
| |$g=e(V,Q).e(U+yA,sQ)$|
| |if $g \ne 1$, reject the connection|
| $R=r{A} \rightarrow $ | $\leftarrow W=w{A}$ |
| $h=H(A,U,y,V,R,W)$ | $h=H(A,U,y,V,R,W)$ |
| $K=H_g((g_1.{g_2}^\alpha)^{r+h} \| x{W})$ | $K=H_g(e(R+hA,sQ) \| w{U})$ |

---

### Chow-Choo Protocol

As initially proposed, the Chow-Choo Protocol was based on a type-1 pairing. A type-1 pairing operates as $G_1 \times G_1 \rightarrow G_T$, where $G_1$ is a group of points of prime order $q$ on the curve, and $G_T$ is a finite extension field of the same order, whose extension is the so-called embedding degree $k$ associated with the curve.

In the Milagro framework, the Chow-Choo Protocol is made to work in a Type-3 setting.

Pairings are usually written as functions of the form $g=e(A,B)$, where $A \in G_1$, $g \in G_T$, and for a Type-1 pairing $B \in G_1$ and for Type-3 $B \in G_2$.

Consider now an application of this protocol to an imagined Internet of Things (IoT) setting.

Each Thing is issued with a serial number and its own Chow-Choo key (which can double as an M-Pin Key) based on that serial number as an identity.

These keys may be embedded at the time of manufacture, by the manufacturer acting as a naturally trusted authority.

When a Thing needs to communicate with another Thing, an action which requires knowing only the identity of the other, both parties can activate the Chow-Choo Protocol to calculate the same key to encrypt their communication.

Let's make an example. Let Alice and Bob be two communicating Things both sending and receiving. Alice is issued with $sA_1$ and $sA_2$, where $A_1=H_1(ID)$ and $A_2=H_2(ID)$ (where ID is its identity), as this describes where they can appear in the pairing (i.e. $A_1$ is in $G_1$, $A_2$ is in $G_2$). Similarly Bob is issued with $sB_1$ and $sB_2$. 

Based on the fact if they are *sending* or *receiving*, Alice and Bob use one of those two secret to agree a common key. By convention the initiator uses their *sender* key and the responder uses their *receiver* key.

An obvious advantage is to issue each Thing with two keys, one in $G_1$ and the other in $G_2$, **if** the Thing is approved to send and receive.

Another thing we can exploit in any communication context is that there is an initiator and a responder, or a *sender* and *receiver*, if you will.

However, the capability exists to cryptographically bound Things to only receiving information, or only sending information, based upon whether or not a Thing has been issued a sender and / or a receiver key.

This capability is exploited in the Milagro framework to enable peer to peer authenticated key agreement.

---

<!--- This is the Chow Choo protocol in a Mathml table / frame because redering in Math LaTex equations exposes a bug in MathJax. It's just one equation that has this bug!  --->

<figure>
  <caption><strong>Figure 4.</strong> Chow-Choo Protocol</caption>
</figure>
<figure>
	<html>
	<math xmlns="http://www.w3.org/1998/Math/MathML" display='block'>
			<mtable frame="solid" rowlines="solid" rowalign="center" mathbackground="white">
			<mstyle mathsize='.85em'>
		<mtr>
			<mtd>
				<mspace width="0.1em" />
			</mtd>
			<mtd columnalign="left">
				<mtable class="m-matrix">
					<mtr>
						<mtd>
							<mtext>SENDER</mtext>
						</mtd>
						<mtd>
							<mtext>RECEIVER</mtext>
						</mtd>
					</mtr>
					<mtr>
						<mtd>
							<mi>x</mi>
							<mo>&#x02208;</mo>
							<msubsup>
								<mi>&#x02124;</mi>
								<mi>q</mi>
								<mo>*</mo>
							</msubsup>
						</mtd>
						<mtd>
						</mtd>
					</mtr>
					<mtr>
						<mtd>
							<mi>A</mi>
							<mi>G</mi>
							<mn>1</mn>
							<mo>:</mo>
							<mo>=</mo>
							<msub>
								<mi>H</mi>
								<mn>1</mn>
							</msub>
							<mrow>
								<mo form="prefix">(</mo>
								<mi>I</mi>
								<mo>&#x02146;</mo>
								<mi>A</mi>
								<mo form="postfix">)</mo>
							</mrow>
						</mtd>
						<mtd>
						</mtd>
					</mtr>
					<mtr>
						<mtd>
							<mi>P</mi>
							<mi>a</mi>
							<msub>
								<mi>G</mi>
								<mn>1</mn>
							</msub>
							<mo>:</mo>
							<mo>=</mo>
							<mi>x</mi>
							<mo>&#x022C5;</mo>
							<mi>A</mi>
							<msub>
								<mi>G</mi>
								<mn>1</mn>
							</msub>
						</mtd>
						<mtd>
						</mtd>
					</mtr>
					<mtr>
						<mtd>
							<mi>I</mi>
							<mo>&#x02146;</mo>
							<mi>A</mi>
							<mo>,</mo>
							<mi>P</mi>
							<mi>a</mi>
							<msub>
								<mi>G</mi>
								<mn>1</mn>
							</msub>
							<mo>&#x027F6;</mo>
						</mtd>
						<mtd>
						</mtd>
					</mtr>
					<mtr>
						<mtd>
						</mtd>
						<mtd>
							<mi>y</mi>
							<mo>,</mo>
							<mi>w</mi>
							<mo>&#x02208;</mo>
							<msubsup>
								<mi>&#x02124;</mi>
								<mi>q</mi>
								<mo>*</mo>
							</msubsup>
						</mtd>
					</mtr>
					<mtr>
						<mtd>
						</mtd>
						<mtd>
							<mi>A</mi>
							<msub>
								<mi>G</mi>
								<mn>1</mn>
							</msub>
							<mo>:</mo>
							<mo>=</mo>
							<msub>
								<mi>H</mi>
								<mn>1</mn>
							</msub>
							<mrow>
								<mo form="prefix">(</mo>
								<mi>I</mi>
								<mo>&#x02146;</mo>
								<mi>A</mi>
								<mo form="postfix">)</mo>
							</mrow>
						</mtd>
					</mtr>
					<mtr>
						<mtd>
						</mtd>
						<mtd>
							<mi>B</mi>
							<msub>
								<mi>G</mi>
								<mn>2</mn>
							</msub>
							<mo>:</mo>
							<mo>=</mo>
							<msub>
								<mi>H</mi>
								<mn>2</mn>
							</msub>
							<mrow>
								<mo form="prefix">(</mo>
								<mi>I</mi>
								<mo>&#x02146;</mo>
								<mi>B</mi>
								<mo form="postfix">)</mo>
							</mrow>
						</mtd>
					</mtr>
					<mtr>
						<mtd>
						</mtd>
						<mtd>
							<mi>P</mi>
							<mi>b</mi>
							<msub>
								<mi>G</mi>
								<mn>2</mn>
							</msub>
							<mo>:</mo>
							<mo>=</mo>
							<mi>y</mi>
							<mo>&#x022C5;</mo>
							<mi>B</mi>
							<msub>
								<mi>G</mi>
								<mn>2</mn>
							</msub>
						</mtd>
					</mtr>
					<mtr>
						<mtd>
						</mtd>
						<mtd>
							<mi>P</mi>
							<mi>g</mi>
							<msub>
								<mi>G</mi>
								<mn>1</mn>
							</msub>
							<mo>:</mo>
							<mo>=</mo>
							<mi>w</mi>
							<mo>&#x022C5;</mo>
							<mi>A</mi>
							<msub>
								<mi>G</mi>
								<mn>1</mn>
							</msub>
						</mtd>
					</mtr>
					<mtr>
						<mtd>
						</mtd>
						<mtd>
							<mtext>pia</mtext>
							<mo>:</mo>
							<mo>=</mo>
							<msub>
								<mi>H</mi>
								<mi>q</mi>
							</msub>
							<mrow>
								<mo form="prefix">(</mo>
								<mi>P</mi>
								<mi>a</mi>
								<msub>
									<mi>G</mi>
									<mn>1</mn>
								</msub>
								<mo>&#x02016;</mo>
								<mi>P</mi>
								<mi>b</mi>
								<msub>
									<mi>G</mi>
									<mn>2</mn>
								</msub>
								<mo>&#x02016;</mo>
								<mi>P</mi>
								<mi>g</mi>
								<msub>
									<mi>G</mi>
									<mn>1</mn>
								</msub>
								<mo>&#x02016;</mo>
								<mi>I</mi>
								<mo>&#x02146;</mo>
								<mi>B</mi>
								<mo form="postfix">)</mo>
							</mrow>
						</mtd>
					</mtr>
					<mtr>
						<mtd>
						</mtd>
						<mtd>
							<mtext>pib</mtext>
							<mo>:</mo>
							<mo>=</mo>
							<msub>
								<mi>H</mi>
								<mi>q</mi>
							</msub>
							<mrow>
								<mo form="prefix">(</mo>
								<mi>P</mi>
								<mi>b</mi>
								<msub>
									<mi>G</mi>
									<mn>2</mn>
								</msub>
								<mo>&#x02016;</mo>
								<mi>P</mi>
								<mi>a</mi>
								<msub>
									<mi>G</mi>
									<mn>1</mn>
								</msub>
								<mo>&#x02016;</mo>
								<mi>P</mi>
								<mi>g</mi>
								<msub>
									<mi>G</mi>
									<mn>1</mn>
								</msub>
								<mo>&#x02016;</mo>
								<mi>I</mi>
								<mo>&#x02146;</mo>
								<mi>A</mi>
								<mo form="postfix">)</mo>
							</mrow>
						</mtd>
					</mtr>
					<mtr>
						<mtd>
						</mtd>
						<mtd>
							<mi>k</mi>
							<mo>:</mo>
							<mo>=</mo>
							<mi>e</mi>
							<mrow>
								<mo form="prefix">(</mo>
								<mtext>pia</mtext>
								<mo>&#x022C5;</mo>
								<mi>A</mi>
								<msub>
									<mi>G</mi>
									<mn>1</mn>
								</msub>
								<mo>+</mo>
								<mi>P</mi>
								<mi>a</mi>
								<msub>
									<mi>G</mi>
									<mn>1</mn>
								</msub>
								<mo>,</mo>
								<mo form="prefix">(</mo>
								<mi>y</mi>
								<mo>+</mo>
								<mtext>pib</mtext>
								<mo form="postfix">)</mo>
								<mo>&#x022EF;</mo>
								<mo>&#x022C5;</mo>
								<mi>B</mi>
								<msub>
									<mi>G</mi>
									<mn>2</mn>
								</msub>
								<mo form="postfix">)</mo>
							</mrow>
						</mtd>
					</mtr>
					<mtr>
						<mtd>
						</mtd>
						<mtd>
							<mi>K</mi>
							<mo>:</mo>
							<mo>=</mo>
							<mi>H</mi>
							<mrow>
								<mo form="prefix">(</mo>
								<mi>k</mi>
								<mo>,</mo>
								<mi>w</mi>
								<mo>&#x022C5;</mo>
								<mi>P</mi>
								<mi>a</mi>
								<msub>
									<mi>G</mi>
									<mn>1</mn>
								</msub>
								<mo form="postfix">)</mo>
							</mrow>
						</mtd>
					</mtr>
					<mtr>
						<mtd>
						</mtd>
						<mtd>
							<mo>&#x027F5;</mo>
							<mi>I</mi>
							<mo>&#x02146;</mo>
							<mi>B</mi>
							<mo>,</mo>
							<mi>P</mi>
							<mi>g</mi>
							<msub>
								<mi>G</mi>
								<mn>1</mn>
							</msub>
							<mo>,</mo>
							<mi>P</mi>
							<mi>b</mi>
							<msub>
								<mi>G</mi>
								<mn>2</mn>
							</msub>
						</mtd>
					</mtr>
					<mtr>
						<mtd>
							<mi>B</mi>
							<msub>
								<mi>G</mi>
								<mn>2</mn>
							</msub>
							<mo>:</mo>
							<mo>=</mo>
							<msub>
								<mi>H</mi>
								<mn>2</mn>
							</msub>
							<mrow>
								<mo form="prefix">(</mo>
								<mi>I</mi>
								<mo>&#x02146;</mo>
								<mi>B</mi>
								<mo form="postfix">)</mo>
							</mrow>
						</mtd>
						<mtd>
						</mtd>
					</mtr>
					<mtr>
						<mtd>
							<mtext>pia</mtext>
							<mo>:</mo>
							<mo>=</mo>
							<msub>
								<mi>H</mi>
								<mi>q</mi>
							</msub>
							<mrow>
								<mo form="prefix">(</mo>
								<mi>P</mi>
								<mi>a</mi>
								<msub>
									<mi>G</mi>
									<mn>1</mn>
								</msub>
								<mo>&#x02016;</mo>
								<mi>P</mi>
								<mi>b</mi>
								<msub>
									<mi>G</mi>
									<mn>2</mn>
								</msub>
								<mo>&#x02016;</mo>
								<mi>P</mi>
								<mi>g</mi>
								<msub>
									<mi>G</mi>
									<mn>1</mn>
								</msub>
								<mo>&#x02016;</mo>
								<mi>I</mi>
								<mo>&#x02146;</mo>
								<mi>B</mi>
								<mo form="postfix">)</mo>
							</mrow>
						</mtd>
						<mtd>
						</mtd>
					</mtr>
					<mtr>
						<mtd>
							<mtext>pib</mtext>
							<mo>:</mo>
							<mo>=</mo>
							<msub>
								<mi>H</mi>
								<mi>q</mi>
							</msub>
							<mrow>
								<mo form="prefix">(</mo>
								<mi>P</mi>
								<mi>b</mi>
								<msub>
									<mi>G</mi>
									<mn>2</mn>
								</msub>
								<mo>&#x02016;</mo>
								<mi>P</mi>
								<mi>a</mi>
								<msub>
									<mi>G</mi>
									<mn>1</mn>
								</msub>
								<mo>&#x02016;</mo>
								<mi>P</mi>
								<mi>g</mi>
								<msub>
									<mi>G</mi>
									<mn>1</mn>
								</msub>
								<mo>&#x02016;</mo>
								<mi>I</mi>
								<mo>&#x02146;</mo>
								<mi>A</mi>
								<mo form="postfix">)</mo>
							</mrow>
						</mtd>
						<mtd>
						</mtd>
					</mtr>
					<mtr>
						<mtd>
							<mi>k</mi>
							<mo>:</mo>
							<mo>=</mo>
							<mi>e</mi>
							<mrow>
								<mo form="prefix">(</mo>
								<mo form="prefix">(</mo>
								<mi>x</mi>
								<mo>+</mo>
								<mi>p</mi>
								<mi>i</mi>
								<mi>a</mi>
								<mo form="postfix">)</mo>
								<mo>&#x022EF;</mo>
								<mo>&#x022C5;</mo>
								<mi>A</mi>
								<msub>
									<mi>G</mi>
									<mn>1</mn>
								</msub>
								<mo>,</mo>
								<mtext>pib</mtext>
								<mo>&#x022C5;</mo>
								<mi>B</mi>
								<msub>
									<mi>G</mi>
									<mn>2</mn>
								</msub>
								<mo>+</mo>
								<mi>P</mi>
								<mi>b</mi>
								<msub>
									<mi>G</mi>
									<mn>2</mn>
								</msub>
								<mo form="postfix">)</mo>
							</mrow>
						</mtd>
						<mtd>
						</mtd>
					</mtr>
					<mtr>
						<mtd>
							<mi>K</mi>
							<mo>:</mo>
							<mo>=</mo>
							<mi>H</mi>
							<mrow>
								<mo form="prefix">(</mo>
								<mi>k</mi>
								<mo>,</mo>
								<mi>x</mi>
								<mo>&#x022C5;</mo>
								<mi>P</mi>
								<mi>g</mi>
								<msub>
									<mi>G</mi>
									<mn>1</mn>
								</msub>
								<mo form="postfix">)</mo>
							</mrow>
						</mtd>
						<mtd>
						</mtd>
					</mtr>
				</mtable>
			</mtd>
		</mtr>
	</mtable>
	</math>
	</html>
</figure>
---

**Notes on Chow-Choo Protocol:**
<markdeep>
* $G_1$: a $r$-order cyclic subgroup of $E(F_p)$.
* $G_2$: a subgroup of$E(F_{p^k})$, where $k$ is the embedding degree of the Curve.
* $H1$: Maps string value to a point on the curve in $G_1$.
* $H2$: Maps string value to a point on the curve in $G_2$.
* $Hq$: Hashes inputs to an integer modulo the curve order $q$.
* H(): Hash function.
* $||$: denotes the concatenation of messages.
</markdeep>

---

For additional information, the reader is encouraged to download the following research papers from MIRACL LABS (LINK TO PAPERS).
<!---
The M-Pin Protocol has been iterated on several times over the years since, and has been shown to be proven secure under the computational BDH (Bilinear Diffie-Hellman) assumption, and in the Canetti-Krawczyk (CK) security model <a href="#boyd">3</a>.

Furthermore Gorantla, Boyd and Nieto extend this protocol again to the M-Pin 'one-pass' setting, and provide a proof in a modified extended Canetti-Krawczyk (eCK) setting <a href="#gorantla">4</a>.

Furthermore Gorantla, Boyd and Nieto extend this protocol again to the M-Pin 'one-pass' setting, and provide a proof in a modified extended Canetti-Krawczyk (eCK) setting <a href="#gorantla">4</a>.

--->

<markdeep>
<style>h1:before, h2:before { content: none; }</style>
## REFERENCES
</markdeep>
<p></p>
<div class="references">
	<cite id="freeman-scott-teske">D. Freeman and M. Scott and E. Teske. A taxonomy of pairing-friendly elliptic curves. Journal of Cryptography. 2010. Pages 224 -- 280. Volume 23.</cite>
	<cite id="Scott1">M. Scott. Authenticated ID-based Key Exchange and remote log-in with simple token and PIN number. Cryptology ePrint Archive, Report 2002/164. http://eprint.iacr.org.</cite>
	<cite id="boyd">C. Boyd and A. Mathuria, Protocols for Authentication and Key Establishment, Springer-Verlag, 2003.</cite>
  <cite id="chow-choo">Chow, S.S.M., Choo, K.-K.R.: Strongly-Secure Identity-based Key Agreement and Anonymous Extension. Cryptology ePrint Archive, Report 2007/018.</cite>
  <cite id="m-pin-ietf">Chow, S.S.M., Choo, K.-K.R.: Strongly-Secure Identity-based Key Agreement and Anonymous Extension. Cryptology ePrint Archive, Report 2007/018.</cite>
  <cite id="smart-vercauteren">N. Smart and F. Vercauteren. On Computable Isomorphisms in Efficient Pairing-based Systems. Discrete Applied Mathematics. Volume 155. Pages 538--547. 2007.</cite>
</div>
