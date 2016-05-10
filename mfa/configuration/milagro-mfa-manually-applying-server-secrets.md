---
currentMenu: milagro-mfa-manually-applying-server-secrets
---

##Server secret configuration for clusters
<!-- MsoSubtitle -->

<h2>Introduction</h2>

<p>To install a server to be part of a cluster, it&nbsp;must&nbsp;have the same server secret as the original one.</p>

<h2>Description</h2>
<!-- Standard Paragraph -->

<p class="Body">You can find the secret on the original server in&nbsp;/&lt;install directory&gt;/credentials.json.</p>


<p>To apply the server secret from the first instance to a subsequent instance:</p>

<ul>
	<li>Copy credentials.json to the installation directory of the subsequent installation</li>
	<li>Update the following configuration file:</li>
</ul>

<p style="margin-left: 40px;"><em>/&lt;installation directory/config_rps.py</em></p>

<ul>
	<li>Change the following line:</li>
</ul>

<pre style="margin-left: 40px;">
<span class="CVXCodeinText" style="font-family:&quot;Courier New&quot;">​# certivoxServerSecret = &#39;dta&#39; # Default</span></pre>

<p style="margin-left: 40px;">to:</p>

<pre style="margin-left: 40px;">
certivoxServerSecret = &#39;credentials.json&#39;</pre>


<p>The servers must have external internet access to work properly. </p>
