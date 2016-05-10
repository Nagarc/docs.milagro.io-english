---
currentMenu: milagro-mfa-overview
---

<div id="generated-toc" class="generate_from_h2"></div>

<h1>Milagro Authentication Overview</h1>
<!-- MsoSubtitle -->


## Zero-Knowledge Proof Protocol Concept Overview

A <a href="http://en.wikipedia.org/wiki/Zero-knowledge_proof" target="_blank">zero-knowledge proof </a>protocol is a method by which one party (the prover) can prove to another party (the verifier) that a given statement is true, without conveying any additional information apart from the fact that the statement is indeed true. Proving that one possesses certain knowledge is, in most cases, trivial if one is allowed to simply reveal that knowledge; the challenge is proving that one has such knowledge without revealing it or without revealing anything else.

## Milagro Authentication Background

Milagro authentication is the Apache licensed version of the M-Pin Protocol. It was first introduced in academic circles over a decade ago by Dr. Michael Scott, MIRACL's chief cryptographer, and has been cited over three thousand times in cryptographic research since initial publication. To date, no known theoretical or practical attacks exist against it.

**For more information on the M-Pin Protocol in general, refer to the M-Pin cryptographic white papers available on the <a href="http://www.MIRACL.com/" target="_blank">MIRACL website</a> in the <a href="http://cdn2.hubspot.net/hubfs/230906/miracl/white_papers/MIRACL_M-Pin_ZeroFactor.pdf?t=1454680982288" target="_blank">MIRACL Labs</a> section.**

## Protocol Overview ##

Milagro Authentication is based on a zero-knowledge proof authentication protocol using proven, strong, standards-based elliptic curve cryptography:

<ul style="margin: 5px 0px 0px 20px; padding: 0px 0px 0px 12px; font-family: Verdana, Arial, Helvetica, sans-serif; font-size: 12px;">
	<li>Server Keys and Client Keys are issued according to elliptic curve cryptography principles, and the server can tell whether a client key comes from the right elliptic curve set.</li>
	<li>The server can prove who a user is without having to store client credentials, or in a database with its&nbsp;current set up of&nbsp;passwords.</li>
	<li>Credentials (Client Keys) are NEVER exchanged (encrypted or unencrypted) between a user and the server.</li>
	<li>Server Key compromise does not reveal anything about users or their credentials, eliminating scenarios like password database breaches.</li>
	<li>The code that manipulates the Client Key (a user&#39;s credential) runs in the user&#39;s browser or app, therefore no separate hardware tokens or software installations are required.</li>
</ul>

<p>The picture below represents schematically the operation of the M-Pin Authentication Protocol:</p>

<p><img alt="1-m-pin-authentication-overlay" src="http://cdn2.hubspot.net/hub/230906/file-2034175627-jpg/Images-cos/diagrams/1-m-pin-authentication-overlay.jpg" style="font-size: 12px; line-height: 19.2px; margin-right: auto; margin-left: auto; display: block;" /></p>
