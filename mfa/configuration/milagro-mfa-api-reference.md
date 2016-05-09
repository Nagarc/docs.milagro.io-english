<h1 abp="2677">M-Pin Core 4.0 API Reference</h1>


<h2 abp="2761">Acronyms</h2>

<table abp="2763" class="confluenceTable tablesorter">
	<thead abp="2764">
		<tr abp="2765" class="sortableHeader">
			<th abp="2766" class="confluenceTh sortableHeader" data-column="0">
			<div abp="2767" class="tablesorter-header-inner">Acronym</div>
			</th>
			<th abp="2768" class="confluenceTh sortableHeader" data-column="1">
			<div abp="2769" class="tablesorter-header-inner">Description</div>
			</th>
		</tr>
	</thead>
	<tbody abp="2770">
		<tr abp="2771">
			<td abp="2772" class="confluenceTd">RPS</td>
			<td abp="2773" class="confluenceTd">Relying Party Service</td>
		</tr>
		<tr abp="2774">
			<td abp="2775" class="confluenceTd">RPA</td>
			<td abp="2776" class="confluenceTd">Relying Party Application</td>
		</tr>
		<tr abp="2777">
			<td abp="2778" class="confluenceTd">D-TA</td>
			<td abp="2779" class="confluenceTd">Distributed Trust Authority</td>
		</tr>
		<tr abp="2780">
			<td abp="2781" class="confluenceTd">ACL</td>
			<td abp="2782" class="confluenceTd">Access Control List</td>
		</tr>
		<tr abp="2783">
			<td abp="2784" class="confluenceTd">OTP</td>
			<td abp="2785" class="confluenceTd">One-Time Password</td>
		</tr>
		<tr abp="2786">
			<td abp="2787" class="confluenceTd" colspan="1">OTT</td>
			<td abp="2788" class="confluenceTd" colspan="1">One-Time Token</td>
		</tr>
	</tbody>
</table>

<h2 abp="2789">System Overview</h2>

<p abp="2791"><span abp="2792">The platform consists of two groups of Services - local services running on a server and cloud hosted services. Hosted by MIRACL.</span></p>

<h3 abp="2793"><span abp="2794">Local Services</span></h3>

<ul abp="2796">
	<li abp="2797"><strong abp="2798">RPS/Milagro MFA Server</strong>&nbsp;- Relying Party Service. Implements the authentication protocol and Workflows. &nbsp;The RPS serves as an abstraction layer between the specific implementation of the protocol and the RPA.&nbsp; RPS also serves as an authentication server.</li>
	<li abp="2799"><strong abp="2800">D-TA</strong>&nbsp;- Distributed Trust&nbsp;Authority Service, managed by the Customer. Responsible to generate Client and Server Secret Shares as well as Time Permit Shares</li>
	<li abp="2803"><strong abp="2804">RPA</strong>&nbsp;- Relying Party Application. This is the Application to which end-users are authenticated through the Milagro MFA Platform.</li>
</ul>

<h3 abp="2805">Could hosted Services</h3>

<ul abp="2807">
	<li abp="2808"><strong abp="2809">D-TA</strong>&nbsp;- Distributed Trust&nbsp;Authority Service, managed by the Customer.&nbsp;Responsible for generating Client and Server Secret Shares as well as Time Permit Shares.</li>
	<li abp="2810"><strong abp="2811">D-TA Proxy</strong>&nbsp;- Proxies request to the D-TA, validating RPS signatures. The D-TA Proxy is public-facing, while the D-TA should not be publicly accessible.</li>
	<li abp="2812"><strong abp="2813" style="font-size: inherit;">Time Permits Service</strong>&nbsp;- A service responsible to publish Time Permits to an online storage (CDN), such as AWS S3.</li>
	<li abp="2814"><strong abp="2815" style="font-size: inherit;">Registration Service</strong>&nbsp;- A service that handles new Customer registration.</li>
</ul>

<h2 abp="2816">RPS</h2>

<p abp="2818">The RPS resides on the server. The RPS serves as an abstraction layer between the authentication protocol, workflow and crypto, and the RPA. The RPS provides an API to the RPA, for the operations that the RPA is responsible for, and which cannot be performed by the RPS itself.</p>


<div abp="2821">
<h2 abp="2822" id="TechSpec-M-Pinv0.3RelyingPartyService-SystemArchitecture">System Architecture</h2>

<p abp="2824">The RPS is a Python written service, based on the Tornado framework, i.e. it serves requests in a single thread utilizing non-blocking IO operations.</p>

<p abp="2825">The RPS should not be exposed to the public Internet, but it should be accessible by the Client either through the RPA or through a dedicated public facing proxy (e.g. Nginx). For this reason, all the &quot;public&quot; RPS API requests start with a predefined prefix, which is set by default to&nbsp;<em abp="2826">/rps</em>.&nbsp;<span abp="2827">Any request that starts with that prefix should be redirected to the RPS by the&nbsp;</span>public<span abp="2828">&nbsp;facing&nbsp;</span>service<span abp="2829">&nbsp;- the RPA or a proxy. RPS API requests that do not start with the prefix should be accessible only from the Customer&#39;s private network, and more specifically, by the RPA.</span></p>

<p abp="2830"><span abp="2831">Additionally, the RPS will implement an ACL, so only authorized machines will be able to make requests to its API</span></p>

<h3 abp="2832" id="TechSpec-M-Pinv0.3RelyingPartyService-RPSScalabilityandHighAvailability"><span abp="2833">RPS Scalability&nbsp;and High Availability</span></h3>

<p abp="2835">By default, the RPS will store all of its work data in its memory storage. This approach, although simpler and more secure, introduces a problem when the RPS needs to be scaled or made highly available. For this reason the RPS supports an option to use Redis as a work storage and have several RPS instances work together, behind a load balancer. Since the actual state is stored on Redis, the RPS instances become stateless and mutually replaceable. For more information regarding the configuration for Redis storage, see&nbsp;<a abp="2837" hqid="1662952" href="../configuration/milagro-mfa-configuration.html">Configuration</a>.</p>

<h3 abp="2838" id="TechSpec-M-Pinv0.3RelyingPartyService-RPSAPI"><span abp="2839">RPS API</span></h3>

<h4 abp="2841" id="TechSpec-M-Pinv0.3RelyingPartyService-ClientInitialization"><span abp="2842">Client Initialization</span></h4>

<h5 abp="2844" id="TechSpec-M-Pinv0.3RelyingPartyService-GET/rps/clientSettings">GET /rps/clientSettings</h5>

<p abp="2846">Called by the Client (PIN Pad), through a proxy, to obtain the setting it should use. Most of the settings are Service Endpoints and Customer details.</p>

<p abp="2847"><strong abp="2848">Parameters:</strong>&nbsp;&lt;none&gt;</p>

<p abp="2849"><strong abp="2850">Data:</strong>&nbsp;&lt;none&gt;</p>

<p abp="2851"><strong abp="2852">Response:</strong>&nbsp;200 OK on success, 4xx otherwise</p>

<p abp="2853"><strong abp="3134" style="line-height: 1.6em;">Response Data:</strong></p>
</div>

<div abp="2855">
<div>
<div abp="3135" class="code panel pdl">
<div abp="3136" class="codeContent panelContent pdl">
<div abp="3137">
<div abp="3138" class="syntaxhighlighter nogutter java" id="highlighter_320352">
<table abp="3139" border="0" cellpadding="0" cellspacing="0">
	<tbody abp="3140">
		<tr abp="3141">
			<td abp="3142" class="code">
			<div abp="3143" class="container" title="Hint: double-click to select code">
			<div abp="3144" class="line number1 index0 alt2"><span style="font-family: monospace;">{</span><br style="font-family: monospace; color: rgb(102, 102, 102); line-height: 20.4px; background-color: rgb(249, 249, 249);" />
			<span style="font-family: monospace;">&nbsp;&nbsp;&nbsp; &quot;mpinAuthServerURL&quot;: &lt;mpin-auth-endpoint&gt;,</span><br style="font-family: monospace; color: rgb(102, 102, 102); line-height: 20.4px; background-color: rgb(249, 249, 249);" />
			<span style="font-family: monospace;">&nbsp;&nbsp;&nbsp; &quot;timePermitsURL&quot;: &lt;customer-time-permit-endpoint&gt;,</span><br style="font-family: monospace; color: rgb(102, 102, 102); line-height: 20.4px; background-color: rgb(249, 249, 249);" />
			<span style="font-family: monospace;">&nbsp;&nbsp;&nbsp; &quot;timePermitsStorageURL&quot;: &lt;certivox-time-permit-cache-url&gt;,</span><br style="font-family: monospace; color: rgb(102, 102, 102); line-height: 20.4px; background-color: rgb(249, 249, 249);" />
			<span style="font-family: monospace;">&nbsp;&nbsp;&nbsp; &quot;authenticateURL&quot;: &lt;auth-validation-endpoint&gt;,</span><br style="font-family: monospace; color: rgb(102, 102, 102); line-height: 20.4px; background-color: rgb(249, 249, 249);" />
			<span style="font-family: monospace;">&nbsp;&nbsp;&nbsp; &quot;timePermitsStorageURL&quot;: &lt;tp-storage-url&gt;,</span><br style="font-family: monospace; color: rgb(102, 102, 102); line-height: 20.4px; background-color: rgb(249, 249, 249);" />
			<span style="font-family: monospace;">&nbsp;&nbsp;&nbsp; &quot;certivoxURL&quot;: &lt;certivox-services-url&gt;,</span><br style="font-family: monospace; color: rgb(102, 102, 102); line-height: 20.4px; background-color: rgb(249, 249, 249);" />
			<span style="font-family: monospace;">&nbsp;&nbsp;&nbsp; &quot;mobileAuthenticateURL&quot;: &lt;mobile-auth-validation-endpoint&gt;,</span><br style="font-family: monospace; color: rgb(102, 102, 102); line-height: 20.4px; background-color: rgb(249, 249, 249);" />
			<span style="font-family: monospace;">&nbsp;&nbsp;&nbsp; &quot;signatureURL&quot;: &lt;signature-endpoint&gt;,</span><br style="font-family: monospace; color: rgb(102, 102, 102); line-height: 20.4px; background-color: rgb(249, 249, 249);" />
			<span style="font-family: monospace;">&nbsp;&nbsp;&nbsp; &quot;requestOTP&quot;: &lt;request-otp&gt;,</span><br style="font-family: monospace; color: rgb(102, 102, 102); line-height: 20.4px; background-color: rgb(249, 249, 249);" />
			<span style="font-family: monospace;">&nbsp;&nbsp;&nbsp; &quot;setupDoneURL&quot;: &lt;setup-done-endpoint&gt;,</span><br style="font-family: monospace; color: rgb(102, 102, 102); line-height: 20.4px; background-color: rgb(249, 249, 249);" />
			<span style="font-family: monospace;">&nbsp;&nbsp;&nbsp; &quot;successLoginURL&quot;: &lt;successful-login-url&gt;,</span><br style="font-family: monospace; color: rgb(102, 102, 102); line-height: 20.4px; background-color: rgb(249, 249, 249);" />
			<span style="font-family: monospace;">&nbsp;&nbsp;&nbsp; &quot;accessNumberURL&quot;: &lt;access-number-endpoint&gt;,</span><br style="font-family: monospace; color: rgb(102, 102, 102); line-height: 20.4px; background-color: rgb(249, 249, 249);" />
			<span style="font-family: monospace;">&nbsp;&nbsp;&nbsp; &quot;getAccessNumberURL&quot;: &lt;get-access-number-endpoint&gt;,</span><br style="font-family: monospace; color: rgb(102, 102, 102); line-height: 20.4px; background-color: rgb(249, 249, 249);" />
			<span style="font-family: monospace;">&nbsp;&nbsp;&nbsp; &quot;accessNumberDigits&quot;: &lt;access-number-digits&gt;,</span><br style="font-family: monospace; color: rgb(102, 102, 102); line-height: 20.4px; background-color: rgb(249, 249, 249);" />
			<span style="font-family: monospace;">&nbsp;&nbsp;&nbsp; &quot;accessNumberUseCheckSum&quot;: &lt;access-number-use-checksum&gt;,</span><br style="font-family: monospace; color: rgb(102, 102, 102); line-height: 20.4px; background-color: rgb(249, 249, 249);" />
			<span style="font-family: monospace;">&nbsp;&nbsp;&nbsp; &quot;cSum&quot;: &lt;access-number-checksum-method&gt;,</span><br style="font-family: monospace; color: rgb(102, 102, 102); line-height: 20.4px; background-color: rgb(249, 249, 249);" />
			<span style="font-family: monospace;">&nbsp;&nbsp;&nbsp; &quot;seedValue&quot;: &lt;seed-value&gt;,</span><br style="font-family: monospace; color: rgb(102, 102, 102); line-height: 20.4px; background-color: rgb(249, 249, 249);" />
			<span style="font-family: monospace;">&nbsp;&nbsp;&nbsp; &quot;registerURL&quot;: &lt;user-register-endpoint&gt;,</span><br style="font-family: monospace; color: rgb(102, 102, 102); line-height: 20.4px; background-color: rgb(249, 249, 249);" />
			<span style="font-family: monospace;">&nbsp;&nbsp;&nbsp; &quot;identityCheckRegex&quot;: &lt;identity-check-regex&gt;,</span><br style="font-family: monospace; color: rgb(102, 102, 102); line-height: 20.4px; background-color: rgb(249, 249, 249);" />
			<span style="font-family: monospace;">&nbsp;&nbsp;&nbsp; &quot;useWebSocket&quot;: &lt;use-web-sockets&gt;,</span><br style="font-family: monospace; color: rgb(102, 102, 102); line-height: 20.4px; background-color: rgb(249, 249, 249);" />
			<span style="font-family: monospace;">&nbsp;&nbsp;&nbsp; &quot;setDeviceName&quot;: &lt;set-device-name&gt;,</span><br style="font-family: monospace; color: rgb(102, 102, 102); line-height: 20.4px; background-color: rgb(249, 249, 249);" />
			<span style="font-family: monospace;">&nbsp;&nbsp;&nbsp; &quot;appID&quot;: &lt;app-id&gt;</span><br style="font-family: monospace; color: rgb(102, 102, 102); line-height: 20.4px; background-color: rgb(249, 249, 249);" />
			<span style="font-family: monospace;">}</span></div>
			</div>
			</td>
		</tr>
	</tbody>
</table>
</div>
</div>
</div>
</div>
</div>

<div><em abp="2942">&lt;mpin-auth-endpoint&gt;</em>&nbsp;- M-Pin Server URL&nbsp;for end-user authentication.&nbsp;On this URL the client will&nbsp;open a WebSocket or make the &quot;/pass1&quot; and &quot;/pass2&quot; requests.&nbsp;Example: &quot;/rps&quot;</div>

<p abp="2943"><em abp="2944">&lt;customer-time-permit-endpoint&gt;</em>&nbsp;- Endpoint on which requests for Customer Time Permit Share should be done. Example: &quot; <span abp="2945">rps/timePermit&quot;</span></p>

<p abp="2946"><em abp="2947">&lt;MIRACL-time-permit-cache-url&gt;</em>&nbsp;- Base URL of cache storage for&nbsp;MIRACL Time Permit Share.</p>

<p abp="2948"><em abp="2949">&lt;auth-validation-endpoint&gt;</em><span abp="2950">&nbsp;- Endpoint implemented by the RPA for&nbsp;</span>authentication<span abp="2951">&nbsp;validation.&nbsp;</span><span abp="2952">Example: &quot;/mpinAuthenticate&quot;.</span></p>

<p abp="2953"><span abp="2954">&nbsp;</span><span abp="2955"><em abp="2956">&lt;tp-storage-url&gt;</em>&nbsp;- Base URL for the Time Permit Storage. This is the storage where MIRACL API publishes its pre-generated shares of Time Permits. Example: &quot;</span>https://s3-eu-west-1.amazonaws.com/freetier-timeperbit-bucket-qa-v3<span abp="2955">&quot;</span></p>

<p abp="2958"><em abp="2959">&lt;MIRACL-services-url&gt;</em>&nbsp;- Base&nbsp;<span abp="2960">URL for the MIRACL-hosted Services. Example: &quot;https://m-pinapi-qa-v03.MIRACL.org/v0.3&quot;</span><span abp="2961">&nbsp;</span></p>

<p abp="2962"><em abp="2963">&lt;mobile-auth-validation-endpoint&gt;</em>&nbsp;- Endpoint for Mobile Authentication. Example<span abp="2964">: &quot; rps/authenticate&quot;</span></p>

<p abp="2965"><span abp="2966"><em abp="2967">&lt;signature-endpoint&gt;</em>&nbsp;- Endpoint for requesting Relying Party Signature, further used to get Client Secret Share. Example: &quot; rps/signature&quot;</span><span abp="2968">&nbsp;</span></p>

<p abp="2969"><em abp="2970">&lt;request-otp&gt;</em>&nbsp;- Indicates (true or false) whether One-Time Password should be generated on successful&nbsp;authentication. Used for the SSO&nbsp;Server.</p>

<p abp="2971"><span abp="2972"><em abp="2973">&lt;setup-done-endpoint&gt;</em>&nbsp;- Endpoint for the setupDone request. Example: &quot; rps/setupDone&quot;</span></p>

<p abp="2974"><span abp="2975"><em abp="2976">&lt;successful-login-url&gt;</em>&nbsp;-&nbsp;URL that the PIN Pad should load after a successful end-user authentication.</span></p>

<p abp="2977"><span abp="2978"><em abp="2979">&lt;access-number-endpoint&gt;</em>&nbsp;- Endpoint for Access Number polling&nbsp;request. Example: &quot; rps/accessnumber&quot;</span></p>

<p abp="2977"><span abp="2978">&lt;<em>get-access-number-endpoint</em>&gt; - Endpoint for Access Number generating request. Example:&quot; rps/getAccessNumber&quot;</span></p>

<p abp="2981"><em abp="2982">&lt;access-number-digits&gt;</em>&nbsp;- Number of digits for the requested Access Number. Example (and Default):&nbsp;<span abp="2983">7</span></p>

<p abp="2981"><span abp="2983"><em>&lt;access-number-use-checksum&gt;</em> - Indicates (true or false) whether the client should validate the Access Number checksum or not. The default is &#39;true&#39;.</span></p>

<p abp="2981"><em>&lt;access-number-checksum-method&gt;</em> - It is a constant set to 1.</p>

<p abp="2985"><em abp="2986">&lt;seed-value&gt;</em>&nbsp;- Ephemeral hex-encoded value, used as a seed for further random number generation.<span abp="2987">&nbsp;</span></p>

<p abp="2988"><em abp="2989">&lt;user-register-endpoint&gt;</em>&nbsp;- Endpoint for initiating end-user registration flow.&nbsp;<span abp="2990">Example: &quot;&nbsp;rps/user&quot;</span></p>

<p abp="2991"><span abp="2992"><em abp="2993">&lt;identity-check-regex&gt;</em>&nbsp;-&nbsp;A regular expression used to verify the format of a new end-user identity. Example: &quot;[0-9a-zA-Z]+&quot;</span></p>

<p abp="2994"><em abp="2995">&lt;use-web-sockets&gt;</em><span abp="2996">&nbsp;-&nbsp;Indicates (true or false) whether the PIN Pad should make an&nbsp;</span>attempt<span abp="2997">&nbsp;to use WebSockets when authenticating an end-user against the M-Pin Server. If not specified, the default is&nbsp;<em abp="2998">true</em>.</span></p>

<p abp="2999"><span abp="3000"><em abp="3001">&lt;set-device-name&gt;</em>&nbsp;-&nbsp;Indicates (true or false) whether the client should display to and enable the user to set a friendly name for the device. If so, the client should send the device name with the&nbsp;</span>PUT /rps/user&nbsp;request.</p>

<p abp="3003"><span abp="3004"><em abp="3005">&lt;app-id&gt;</em>&nbsp;- Customer specific Application ID, received upon Customer/Application registration for the M-Pin Service.</span></p>

<p abp="3003"><span abp="3004"><em>&lt;registration-ott&gt; -&nbsp;</em>The registration reference number (OTT) provided in the response of PUT/rps/user[/&lt;mpin-id&gt;]</span></p>

<h4 abp="3006" id="TechSpec-M-Pinv0.3RelyingPartyService-Setup"><span abp="3007">Setup</span></h4>

<p abp="3009"><span abp="3010">The purpose of the Setup process is as follows:</span></p>

<ol abp="3011">
	<li abp="3012"><span abp="3013">Verify the user identity</span></li>
	<li abp="3014"><span abp="3015">Get the two Shares of the Client Secret and combine them.</span></li>
	<li abp="3016"><span abp="3017">Extract the user PIN Code from the Client Secret to form the M-Pin Token.</span></li>
	<li abp="3018"><span abp="3019">Store the M-Pin Token on the Client machine.</span></li>
</ol>
</div>

<h5 abp="3020">PUT /rps/user[/&lt;mpin-id&gt;]</h5>

<div abp="3022">
<p abp="3023">This request is made by the Client (through a proxy) to initiate the Setup flow for an end-user, or to re-start it. When the flow is initially started, the request is made without the optional&nbsp;<em abp="3024">/&lt;mpin-id&gt;</em>. In this case the RPS generates a new &lt;mpin-id&gt; which is returned in the response data. The &lt;mpin-id&gt; is a hex-encoded JSON structure of the following form:</p>

<div abp="3025" class="code panel pdl">
<div abp="3026" class="codeContent panelContent pdl">
<div abp="3027">
<div abp="3028" class="syntaxhighlighter nogutter java" id="highlighter_838770">
<table abp="3029" border="0" cellpadding="0" cellspacing="0">
	<tbody abp="3030">
		<tr abp="3031">
			<td abp="3032" class="code">
			<div abp="3033" class="container" title="Hint: double-click to select code">
			<div abp="3034" class="line number1 index0 alt2" style="text-align: left;"><code abp="3035" class="java plain">{</code></div>

			<div abp="3036" class="line number2 index1 alt1" style="text-align: left;"><code abp="3037" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3038" class="java string">&quot;issued&quot;</code><code abp="3039" class="java plain">: &lt;date-time&gt;,</code></div>

			<div abp="3040" class="line number3 index2 alt2" style="text-align: left;"><code abp="3041" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3042" class="java string">&quot;userID&quot;</code><code abp="3043" class="java plain">: &lt;user-identity&gt;,</code></div>

			<div abp="3044" class="line number4 index3 alt1" style="text-align: left;"><code abp="3045" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3046" class="java string">&quot;mobile&quot;</code><code abp="3047" class="java plain">: &lt;</code><code abp="3048" class="java value">1</code><code abp="3049" class="java plain">|</code><code abp="3050" class="java value">0</code><code abp="3051" class="java plain">&gt;,</code></div>

			<div abp="3052" class="line number5 index4 alt2" style="text-align: left;"><code abp="3053" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3054" class="java string">&quot;salt&quot;</code><code abp="3055" class="java plain">: &lt;</code><code abp="3056" class="java value">64</code><code abp="3057" class="java plain">-bit-hex-encoded-random-number&gt;</code></div>

			<div abp="3058" class="line number6 index5 alt1" style="text-align: left;"><code abp="3059" class="java plain">}</code></div>
			</div>
			</td>
		</tr>
	</tbody>
</table>
</div>
</div>
</div>
</div>

<p abp="3060">In certain cases, the Setup flow might need to be re-started for an already generated &lt;mpin-id&gt;. In this case the optional&nbsp;<em abp="3061">/&lt;mpin-id&gt;</em>&nbsp;in the request is appended, as well as the&nbsp;<em abp="3062">regOTT</em>&nbsp;parameter in the request data.</p>

<p abp="3063">During this request, the RPS makes a&nbsp;POST /verify&nbsp;request to the RPA, sending to it an&nbsp;<em abp="3065">activateKey</em><span abp="3066">. During the&nbsp;POST /verify&nbsp;request the RPA could validate whether the provided &lt;user-id&gt; is a valid system user, could initiate a user verification procedure (e.g. sending verification e-mail) or use the optional &lt;user-data&gt; for additional operations that are required to validate the end-user. As a result, the RPA might indicate to the RPS whether the user should be made active immediately, or the RPS should wait for the user identity verification to be completed. When the identity verification is completed, the RPA should make a&nbsp;</span>POST /user/&lt;mpin-id&gt;<span abp="3069">&nbsp;request, providing the&nbsp;<em abp="3070">activateKey</em>, to be able to&nbsp;</span><span abp="3071">proceed</span><span abp="3072">&nbsp;further with the flow (see&nbsp;<a abp="3073" href="#workflows">M-Pin Setup</a>&nbsp;flow).</span></p>

<p abp="3074"><span abp="3075">The actual RPA endpoint for the&nbsp;POST /verify&nbsp;request is configurable (see&nbsp;<a abp="3077" hqid="1662952" href="#">Configuration</a>).</span></p>

<p abp="3078"><strong abp="3079">Parameters:</strong><span abp="3080">&nbsp;&lt;none&gt;</span></p>

<p abp="3081"><strong abp="3082">Data:</strong></p>

<div abp="3083" class="code panel pdl">
<div abp="3084" class="codeContent panelContent pdl">
<div abp="3085">
<div abp="3086" class="syntaxhighlighter nogutter java" id="highlighter_861888">
<table abp="3087" border="0" cellpadding="0" cellspacing="0">
	<tbody abp="3088">
		<tr abp="3089">
			<td abp="3090" class="code">
			<div abp="3091" class="container" title="Hint: double-click to select code">
			<div abp="3092" class="line number1 index0 alt2" style="text-align: left;"><code abp="3093" class="java plain">{</code></div>

			<div abp="3094" class="line number2 index1 alt1" style="text-align: left;"><code abp="3095" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3096" class="java string">&quot;userId&quot;</code><code abp="3097" class="java plain">: &lt;user-id&gt;,</code></div>

			<div abp="3098" class="line number3 index2 alt2" style="text-align: left;"><code abp="3099" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3100" class="java string">&quot;deviceId&quot;</code><code abp="3101" class="java plain">: &lt;device-id&gt;,</code></div>

			<div abp="3102" class="line number4 index3 alt1" style="text-align: left;"><code abp="3103" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3104" class="java string">&quot;mobile&quot;</code><code abp="3105" class="java plain">: &lt;</code><code abp="3106" class="java value">0</code><code abp="3107" class="java plain">|</code><code abp="3108" class="java value">1</code><code abp="3109" class="java plain">&gt;,</code></div>

			<div abp="3110" class="line number5 index4 alt2" style="text-align: left;"><code abp="3111" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3112" class="java string">&quot;regOTT&quot;</code><code abp="3113" class="java plain">: &lt;registration-ott&gt;,</code></div>

			<div abp="3114" class="line number6 index5 alt1" style="text-align: left;"><code abp="3115" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3116" class="java plain">&lt;user-data&gt;</code></div>

			<div abp="3117" class="line number7 index6 alt2" style="text-align: left;"><code abp="3118" class="java plain">}</code></div>
			</div>
			</td>
		</tr>
	</tbody>
</table>
</div>
</div>
</div>
</div>

<p abp="3119"><em abp="3120">&lt;user-id&gt;</em>&nbsp;- The string identifying the end-user. It might be the end-user e-mail address or any other system-unique string.</p>

<p abp="3121"><em abp="3122">&lt;device-id&gt;</em>&nbsp;- (Optional) Depending on the Customer&#39; preferences, the Client might provide a friendly name describing the device from which the request is coming. This name will be further forwarded to the RPA so it can attach it to the end-user information that it stores.</p>

<p abp="3123"><em abp="3124">&lt;mobile&gt;</em>&nbsp;- Indicates (1 or 0) whether the flow is carried out by the mobile client (1), or not (0).</p>

<p abp="3125"><em abp="3126">&lt;registration-ott&gt;</em>&nbsp;- (Optional) In case an already started setup flow should be re-started, this should be the original&nbsp;&lt;registration-ott&gt; that was returned in the initial response.</p>

<p abp="3127"><em abp="3128">&lt;user-data&gt;</em>&nbsp;- (Optional) The Customer might pass to the PIN Pad Client some customer-specific data that would help to verify the end-user in the RPA. This data is an opaque, passed to the RPA in the&nbsp;POST /verify&nbsp;request.</p>

<p abp="3130"><strong abp="3131">Response:</strong><span abp="3132">&nbsp;200 OK on success, 4xx otherwise</span></p>

<p abp="3133"><strong abp="3134">Response Data:</strong></p>

<div abp="3135" class="code panel pdl">
<div abp="3136" class="codeContent panelContent pdl">
<div abp="3137">
<div abp="3138" class="syntaxhighlighter nogutter java" id="highlighter_320352">
<table abp="3139" border="0" cellpadding="0" cellspacing="0">
	<tbody abp="3140">
		<tr abp="3141">
			<td abp="3142" class="code">
			<div abp="3143" class="container" title="Hint: double-click to select code">
			<div abp="3144" class="line number1 index0 alt2" style="text-align: left;"><code abp="3145" class="java plain">{</code></div>

			<div abp="3146" class="line number2 index1 alt1" style="text-align: left;"><code abp="3147" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3148" class="java string">&quot;expireTime&quot;</code><code abp="3149" class="java plain">: &lt;utc-formatted-expiration-time&gt;,</code></div>

			<div abp="3150" class="line number3 index2 alt2" style="text-align: left;"><code abp="3151" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3152" class="java string">&quot;active&quot;</code><code abp="3153" class="java plain">: &lt;</code><code abp="3154" class="java keyword">true</code><code abp="3155" class="java plain">|</code><code abp="3156" class="java keyword">false</code><code abp="3157" class="java plain">&gt;,</code></div>

			<div abp="3158" class="line number4 index3 alt1" style="text-align: left;"><code abp="3159" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3160" class="java string">&quot;regOTT&quot;</code><code abp="3161" class="java plain">: &lt;registration-ott&gt;,</code></div>

			<div abp="3162" class="line number5 index4 alt2" style="text-align: left;"><code abp="3163" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3164" class="java string">&quot;nowTime&quot;</code><code abp="3165" class="java plain">: &lt;utc-formatted-current-time&gt;,</code></div>

			<div abp="3166" class="line number6 index5 alt1" style="text-align: left;"><code abp="3167" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3168" class="java string">&quot;mpinId&quot;</code><code abp="3169" class="java plain">: &lt;mpin-id&gt;</code></div>

			<div abp="3170" class="line number7 index6 alt2" style="text-align: left;"><code abp="3171" class="java plain">}</code></div>
			</div>
			</td>
		</tr>
	</tbody>
</table>
</div>
</div>
</div>
</div>

<p abp="3172"><em abp="3173">&lt;utc-formatted-expiration-time&gt;</em>&nbsp;- Expiration time for the user setup flow in case the RPS should wait for the user verification to be completed.</p>

<p abp="3174"><em abp="3175">&lt;active&gt;</em>&nbsp;- Indicates (true or false) whether the user has been made active already, and no&nbsp;further&nbsp;user verification is required.</p>

<p abp="3176"><em abp="3177">&lt;registration-ott&gt;</em>&nbsp;- A reference number identifying the setup process for the given &lt;mpin-id&gt;. This number is valid only until the flow is complete or expired, and serves as a type of OTT.</p>

<p abp="3178"><em abp="3179">&lt;utc-formatted-current-time&gt;</em>&nbsp;- The current system time.</p>

<p abp="3180"><em abp="3181">&lt;mpin-id&gt;</em>&nbsp;- The formed hex-encoded M-Pin ID for the end-user identified by &lt;user-id&gt;. If&nbsp;<em abp="3182">/&lt;mpin-id&gt;</em>&nbsp;is appended in the request, the same &lt;mpin-id&gt; will be returned here. Otherwise the RPS generates a new &lt;mpin-id&gt;.</p>

<h5 abp="3183" id="TechSpec-M-Pinv0.3RelyingPartyService-POST/user/&lt;mpin-id&gt;">POST /user/&lt;mpin-id&gt;</h5>

<p abp="3185">This request is made by the RPA when the end-user identity verification is complete.</p>

<p abp="3186">&lt;mpin-id&gt; is the hex-encoded M-Pin ID</p>

<p abp="3187"><strong abp="3188">Parameters:</strong>&nbsp;&lt;none&gt;</p>

<p abp="3189"><strong abp="3190">Data:</strong></p>

<div abp="3191" class="code panel pdl">
<div abp="3192" class="codeContent panelContent pdl">
<div abp="3193">
<div abp="3194" class="syntaxhighlighter nogutter java" id="highlighter_868282">
<table abp="3195" border="0" cellpadding="0" cellspacing="0">
	<tbody abp="3196">
		<tr abp="3197">
			<td abp="3198" class="code">
			<div abp="3199" class="container" title="Hint: double-click to select code">
			<div abp="3200" class="line number1 index0 alt2" style="text-align: left;"><code abp="3201" class="java plain">{</code></div>

			<div abp="3202" class="line number2 index1 alt1" style="text-align: left;"><code abp="3203" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3204" class="java string">&quot;activateKey&quot;</code><code abp="3205" class="java plain">: &lt;activation-key&gt;</code></div>

			<div abp="3206" class="line number3 index2 alt2" style="text-align: left;"><code abp="3207" class="java plain">}</code></div>
			</div>
			</td>
		</tr>
	</tbody>
</table>
</div>
</div>
</div>
</div>

<p abp="3208"><em abp="3209">&lt;activation-key&gt;</em>&nbsp;- The activation key provided by the RPS during the&nbsp;POST /verify&nbsp;request to the RPA.</p>

<p abp="3211"><strong abp="3212">Response:</strong><span abp="3213">&nbsp;200 OK on success, 4xx otherwise</span></p>

<p abp="3214"><strong abp="3215">Response Data:</strong>&nbsp;&lt;none&gt;</p>

<h5 abp="3216" id="TechSpec-M-Pinv0.3RelyingPartyService-GET/rps/signature/&lt;mpin-id&gt;?regOTT=&lt;registration-ott&gt;">GET /rps/signature/&lt;mpin-id&gt;?regOTT=&lt;registration-ott&gt;</h5>

<p abp="3218">This request is made by the Client (through a proxy) and serves several purposes:</p>

<ul abp="3219">
	<li abp="3220">To obtain the Customer share of the Time Permit. As part of this request the RPS will get the Time Permit share from the Customer D-TA and will return it in the response.</li>
	<li abp="3221">To&nbsp;obtain the parameters that should be used to request the MIRACL share of the Time Permit. Those parameters include a unique signature without which the MIRACL D-TA will not fulfill the request.</li>
	<li abp="3222">To generate obfuscated (hashed) M-Pin ID, which is further used by the MIRACL-hosted Services to identify the end-user.</li>
</ul>

<p abp="3223">&lt;mpin-id&gt; is the hex-encoded M-Pin ID.</p>

<p abp="3224"><strong abp="3225">Parameters:&nbsp;</strong>regOTT=&lt;registration-ott&gt;</p>

<p abp="3226"><em abp="3227">&lt;registration-ott&gt;</em>&nbsp;- The registration reference number (OTT) provided in the response of&nbsp;<span abp="3228">PUT /rps/user[/&lt;mpin-id&gt;]</span></p>

<p abp="3230"><strong abp="3231">Data:</strong>&nbsp;&lt;none&gt;</p>

<p abp="3232"><strong abp="3233">Response:</strong>&nbsp;200 OK on success, 4xx otherwise</p>

<p abp="3234"><strong abp="3235">Response Data:</strong><span abp="3236">&nbsp;</span></p>

<div abp="3237" class="code panel pdl">
<div abp="3238" class="codeContent panelContent pdl">
<div abp="3239">
<div abp="3240" class="syntaxhighlighter nogutter java" id="highlighter_2999">
<table abp="3241" border="0" cellpadding="0" cellspacing="0">
	<tbody abp="3242">
		<tr abp="3243">
			<td abp="3244" class="code">
			<div abp="3245" class="container" title="Hint: double-click to select code">
			<div abp="3246" class="line number1 index0 alt2" style="text-align: left;"><code abp="3247" class="java plain">{</code></div>

			<div abp="3248" class="line number2 index1 alt1" style="text-align: left;"><code abp="3249" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3250" class="java string">&quot;clientSecretShare&quot;</code><code abp="3251" class="java plain">: &lt;client-secret-share&gt;,</code></div>

			<div abp="3252" class="line number3 index2 alt2" style="text-align: left;"><code abp="3253" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3254" class="java string">&quot;params&quot;</code><code abp="3255" class="java plain">: &lt;client-secret-request-params&gt;</code></div>

			<div abp="3256" class="line number4 index3 alt1" style="text-align: left;"><code abp="3257" class="java plain">}</code></div>
			</div>
			</td>
		</tr>
	</tbody>
</table>
</div>
</div>
</div>
</div>

<p abp="3258"><em abp="3259">&lt;client-secret-share&gt;</em>&nbsp;- Client Secret Share from the Customer-hosted D-TA Service.</p>

<p abp="3260"><em abp="3261">&lt;client-secret-request-params&gt;</em>&nbsp;- Parameters (including signature) that should be used to request the other Client Secret Share from the MIRACL-hosted D-TA Service. Those parameters are formatted as request query parameters in the form:&nbsp;<code abp="3262">app_id=&lt;app_id&gt;&amp;hash_mpin_id=&lt;hash_mpin_id&gt;&amp;\nexpires=&lt;expires&gt;&amp;mobile=&lt;mobile&gt;&amp;signature=&lt;signature&gt;</code></p>

<h5 abp="3263" id="TechSpec-M-Pinv0.3RelyingPartyService-POST/rps/setupDone/&lt;mpin-id&gt;">POST /rps/setupDone/&lt;mpin-id&gt;</h5>

<p abp="3265">This request is made by the Client (through a proxy) to announce that the end-user has finalized the setup process, providing his/her PIN Number. Currently no action is taken by the RPS during this request.</p>

<p abp="3266"><em abp="3267">&lt;mpin-id&gt;</em>&nbsp;is the hex-encoded M-Pin ID</p>

<p abp="3268"><strong abp="3269">Parameters:&nbsp;</strong>&lt;none&gt;</p>

<p abp="3270"><strong abp="3271">Data:</strong>&nbsp;&lt;none&gt;</p>

<p abp="3272"><strong abp="3273">Response:</strong>&nbsp;200 OK on success, 4xx otherwise</p>

<p abp="3274"><strong abp="3275">Response Data:</strong><span abp="3276">&nbsp;&lt;none&gt;</span></p>

<h4 abp="3277" id="TechSpec-M-Pinv0.3RelyingPartyService-Authentication"><span abp="3278">Authentication</span></h4>

<p abp="3280"><span abp="3281">The Authentication of a user starts with getting a Time Permit for that user identity for the current date. The Time Permit is combined from two shares - one from the Customer D-TA and one from MIRACL D-TA. For efficiency, MIRACL&#39;s share of the Time Permit is cached in two levels - on the Client side (1) and/or on a dedicated cache storage (2). The Client should first of all check whether there is a TP for the current date cached on the local machine. If so, it should use it. Otherwise, it should make a request to the second cache level - the TP storage. If the TP is retrieved from there, it should be cached locally and used until the end of the day. If there&#39;s no TP on the cache storage, a request should be made to MIRACL&#39;s D-TA, which will serve the TP, will generate new TP&#39;s for the next few days and will store them to the cache storage.</span></p>

<h5 abp="3282" id="TechSpec-M-Pinv0.3RelyingPartyService-GET/rps/timePermit/&lt;mpin-id&gt;"><span abp="3283">GET /rps/timePermit/&lt;mpin-id&gt;</span></h5>

<p abp="3285">This request is made by the Client (through a proxy) to obtain the Customer Share of the Time Permit for the given&nbsp;<em abp="3286">&lt;mpin-id&gt;</em>. The RPS makes a request to the Customer-hosted D-TA Service to obtain the Time Permit Share and returns the result to the Client. Prior to sending the request to the D-TA, the RPS will make&nbsp;<a hqid="226290" href="#enduserpermission">GET /permitUser?mpin_id=&lt;mpin-id&gt;</a>&nbsp;request to the RPA, which might revoke the access to the service for the specified user. The RPA should respond with 200 OK, if the RPS should proceed with the time permit request, or with 403 if the user is revoked.&nbsp;The actual RPA endpoint for the&nbsp;GET /permitUser&nbsp;request is configurable. If it is not configured, the RPS will not make this request and will assume that no user should be revoked by the RPA.</p>

<p abp="3290">Additional purpose of this request is to provide the Client with the current date and the location of the cache storage for MIRACL&#39;s share of the Time Permit. The Client should use those in order to check whether the MIRACL&#39;s TP share is stored locally, or on the cache storage, or it should be requested from MIRACL&#39;s D-TA.</p>

<p abp="3291">As part of this request the RPS will also generate and return in the response a unique signature which should further be used in the request for the second Time Permit Share from the MIRACL D-TA Service.</p>

<p abp="3292"><em abp="3293">&lt;mpin-id&gt;</em>&nbsp;is the hex-encoded M-Pin ID.</p>

<p abp="3294"><strong abp="3295">Parameters:&nbsp;</strong>&lt;none&gt;</p>

<p abp="3296"><strong abp="3297">Data:</strong>&nbsp;&lt;none&gt;</p>

<p abp="3298"><strong abp="3299">Response:</strong>&nbsp;200 OK on success, 4xx otherwise</p>

<p abp="3300"><strong abp="3301">Response Data:</strong></p>

<div abp="3302" class="code panel pdl">
<div abp="3303" class="codeContent panelContent pdl">
<div abp="3304">
<div abp="3305" class="syntaxhighlighter nogutter java" id="highlighter_891582">
<table abp="3306" border="0" cellpadding="0" cellspacing="0">
	<tbody abp="3307">
		<tr abp="3308">
			<td abp="3309" class="code">
			<div abp="3310" class="container" title="Hint: double-click to select code">
			<div abp="3311" class="line number1 index0 alt2" style="text-align: left;"><code abp="3312" class="java plain">{</code></div>

			<div abp="3313" class="line number2 index1 alt1" style="text-align: left;"><code abp="3314" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3315" class="java string">&quot;date&quot;</code><code abp="3316" class="java plain">: &lt;current-date&gt;,</code></div>

			<div abp="3317" class="line number3 index2 alt2" style="text-align: left;"><code abp="3318" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3319" class="java string">&quot;message&quot;</code><code abp="3320" class="java plain">: &lt;response-message&gt;,</code></div>

			<div abp="3321" class="line number4 index3 alt1" style="text-align: left;"><code abp="3322" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3323" class="java string">&quot;version&quot;</code><code abp="3324" class="java plain">: &lt;mpin-version&gt;,</code></div>

			<div abp="3325" class="line number5 index4 alt2" style="text-align: left;"><code abp="3326" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3327" class="java string">&quot;timePermit&quot;</code><code abp="3328" class="java plain">: &lt;time-permit-share&gt;,</code></div>

			<div abp="3329" class="line number6 index5 alt1" style="text-align: left;"><code abp="3330" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3331" class="java string">&quot;storageId&quot;</code><code abp="3332" class="java plain">: &lt;storage-id&gt;,</code></div>

			<div abp="3333" class="line number7 index6 alt2" style="text-align: left;"><code abp="3334" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3335" class="java string">&quot;signature&quot;</code><code abp="3336" class="java plain">: &lt;signature&gt;</code></div>

			<div abp="3337" class="line number8 index7 alt1" style="text-align: left;"><code abp="3338" class="java plain">}</code></div>
			</div>
			</td>
		</tr>
	</tbody>
</table>
</div>
</div>
</div>
</div>

<p abp="3339"><em abp="3340">&lt;current-date&gt;</em>&nbsp;- The current date in days since the Epoch (<span abp="3341">1 January 1970, UTC</span>).</p>

<p abp="3342"><em abp="3343">&lt;response-message&gt;</em>&nbsp;- A response message, usually&nbsp;<span abp="3344">&quot;M-Pin Time Permit Generated&quot;.</span></p>

<p abp="3345"><span abp="3346"><em abp="3347">&lt;mpin-version&gt;</em>&nbsp;- The version of the M-Pin protocol, currently&nbsp;</span><span abp="3348">&quot;0.3&quot;.</span></p>

<p abp="3349"><span abp="3350"><em abp="3351">&lt;time-permit-share&gt;</em>&nbsp;- Time Permit Share from the Customer-hosted D-TA Service.</span></p>

<p abp="3352"><span abp="3353"><em abp="3354">&lt;storage-id&gt;</em>&nbsp;- ID under which the MIRACL Time Permit Share is possibly stored on the cache storage. This ID is appended to the base Storage URL received in the Client Settings, to form the full URL for accessing the cache storage.</span></p>

<p abp="3355"><span abp="3356"><em abp="3357">&lt;signature&gt;</em>&nbsp;- A unique signature that should be used in subsequent request for the MIRACL share of the Time Permit.</span></p>

<h5 abp="3358" id="TechSpec-M-Pinv0.3RelyingPartyService-PUT/token">PUT /token</h5>

<p abp="3360">This request is made by the M-Pin Server as a result of authentication attempt. The server passes a token which indicates whether the authentication was successful or not, as well as a reference number (serving as an OTT) for the authentication attempt. This reference number is also provided to the Client, which further posts it to the&nbsp;POST /authenticate&nbsp;request to verify the authentication. This call is assumed to be performed over a secured SSL channel.</p>

<p abp="3362"><strong abp="3363">Parameters:&nbsp;</strong>&lt;none&gt;</p>

<p abp="3364"><strong abp="3365">Data:</strong></p>

<div abp="3366" class="code panel pdl">
<div abp="3367" class="codeContent panelContent pdl">
<div abp="3368">
<div abp="3369" class="syntaxhighlighter nogutter java" id="highlighter_678538">
<table abp="3370" border="0" cellpadding="0" cellspacing="0">
	<tbody abp="3371">
		<tr abp="3372">
			<td abp="3373" class="code">
			<div abp="3374" class="container" title="Hint: double-click to select code">
			<div abp="3375" class="line number1 index0 alt2" style="text-align: left;"><code abp="3376" class="java plain">{</code></div>

			<div abp="3377" class="line number2 index1 alt1" style="text-align: left;"><code abp="3378" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3379" class="java string">&quot;token&quot;</code><code abp="3380" class="java plain">: &lt;auth-token&gt;,</code></div>

			<div abp="3381" class="line number3 index2 alt2" style="text-align: left;"><code abp="3382" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3383" class="java string">&quot;authOTT&quot;</code><code abp="3384" class="java plain">: &lt;authentication-ott&gt;,</code></div>

			<div abp="3385" class="line number4 index3 alt1" style="text-align: left;"><code abp="3386" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3387" class="java string">&quot;signature&quot;</code><code abp="3388" class="java plain">: &lt;signature&gt;</code></div>

			<div abp="3389" class="line number5 index4 alt2" style="text-align: left;"><code abp="3390" class="java plain">}</code></div>
			</div>
			</td>
		</tr>
	</tbody>
</table>
</div>
</div>
</div>
</div>

<p abp="3391"><em abp="3392">&lt;auth-token&gt;</em><span abp="3393">&nbsp;- A Plain Authentication Token in the form of JSON object. Example:</span></p>

<div abp="3394" class="code panel pdl">
<div abp="3395" class="codeContent panelContent pdl">
<div abp="3396">
<div abp="3397" class="syntaxhighlighter nogutter java" id="highlighter_987668">
<table abp="3398" border="0" cellpadding="0" cellspacing="0">
	<tbody abp="3399">
		<tr abp="3400">
			<td abp="3401" class="code">
			<div abp="3402" class="container" title="Hint: double-click to select code">
			<div abp="3403" class="line number1 index0 alt2" style="text-align: left;"><code abp="3404" class="java plain">{</code></div>

			<div abp="3405" class="line number2 index1 alt1" style="text-align: left;"><code abp="3406" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3407" class="java string">&quot;WID&quot;</code><code abp="3408" class="java plain">:&nbsp;</code><code abp="3409" class="java string">&quot;0&quot;</code><code abp="3410" class="java plain">,</code></div>

			<div abp="3411" class="line number3 index2 alt2" style="text-align: left;"><code abp="3412" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3413" class="java string">&quot;expires&quot;</code><code abp="3414" class="java plain">:&nbsp;</code><code abp="3415" class="java string">&quot;2014-03-18T09:00:33Z&quot;</code><code abp="3416" class="java plain">,</code></div>

			<div abp="3417" class="line number4 index3 alt1" style="text-align: left;"><code abp="3418" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3419" class="java string">&quot;pinError&quot;</code><code abp="3420" class="java plain">:&nbsp;</code><code abp="3421" class="java value">0</code><code abp="3422" class="java plain">,</code></div>

			<div abp="3423" class="line number5 index4 alt2" style="text-align: left;"><code abp="3424" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3425" class="java string">&quot;successCode&quot;</code><code abp="3426" class="java plain">:&nbsp;</code><code abp="3427" class="java value">0</code><code abp="3428" class="java plain">,</code></div>

			<div abp="3429" class="line number6 index5 alt1" style="text-align: left;"><code abp="3430" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3431" class="java string">&quot;OTP&quot;</code><code abp="3432" class="java plain">:&nbsp;</code><code abp="3433" class="java string">&quot;0&quot;</code><code abp="3434" class="java plain">,</code></div>

			<div abp="3435" class="line number7 index6 alt2" style="text-align: left;"><code abp="3436" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3437" class="java string">&quot;mpin_id&quot;</code><code abp="3438" class="java plain">: &lt;mpin-id-plain&gt;,</code></div>

			<div abp="3439" class="line number8 index7 alt1" style="text-align: left;"><code abp="3440" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3441" class="java string">&quot;mpin_id_hex&quot;</code><code abp="3442" class="java plain">: &lt;mpin-id-hex&gt;,</code></div>

			<div abp="3443" class="line number9 index8 alt2" style="text-align: left;"><code abp="3444" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3445" class="java string">&quot;pinErrorCost&quot;</code><code abp="3446" class="java plain">:&nbsp;</code><code abp="3447" class="java value">0</code></div>

			<div abp="3448" class="line number10 index9 alt1" style="text-align: left;"><code abp="3449" class="java plain">}</code></div>
			</div>
			</td>
		</tr>
	</tbody>
</table>
</div>
</div>
</div>
</div>

<p abp="3450"><span abp="3451"><em abp="3452">&lt;authentication-ott&gt;</em>&nbsp;- Authentication reference number (OTT)</span></p>

<p abp="3453"><span abp="3454"><em abp="3455">&lt;signature&gt;</em>&nbsp;- HMAC signature over the next fields:&nbsp;</span><code abp="3456">&lt;mpin_id_hex&gt;&lt;successCode&gt;&lt;expires&gt;&lt;WID&gt;&lt;OTP&gt;&lt;authOTT&gt;</code>. The validity of this signature is verified by the RPS.</p>

<p abp="3457"><strong abp="3458">Response:</strong><span abp="3459">&nbsp;200 OK on success, 4xx otherwise</span></p>

<p abp="3460"><strong abp="3461">Response Data:</strong>&nbsp;&lt;none&gt;</p>

<h5 abp="3462" id="TechSpec-M-Pinv0.3RelyingPartyService-POST/authenticate">POST /authenticate</h5>

<p abp="3464">This request is made by the RPA to validate successful authentication for an end-user. The RPA should provide the authentication reference number&nbsp;<span abp="3465"><em abp="3466">&lt;authentication-ott&gt;</em>, in order for the RPS to validate the authentication result.&nbsp;</span></p>

<p abp="3467"><strong abp="3468">Parameters:&nbsp;</strong>&lt;none&gt;</p>

<p abp="3469"><strong abp="3470">Data:</strong></p>

<div abp="3471" class="code panel pdl">
<div abp="3472" class="codeContent panelContent pdl">
<div abp="3473">
<div abp="3474" class="syntaxhighlighter nogutter java" id="highlighter_620695">
<table abp="3475" border="0" cellpadding="0" cellspacing="0">
	<tbody abp="3476">
		<tr abp="3477">
			<td abp="3478" class="code">
			<div abp="3479" class="container" title="Hint: double-click to select code">
			<div abp="3480" class="line number1 index0 alt2" style="text-align: left;"><code abp="3481" class="java plain">{</code></div>

			<div abp="3482" class="line number2 index1 alt1" style="text-align: left;"><code abp="3483" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3484" class="java string">&quot;authOTT&quot;</code><code abp="3485" class="java plain">: &lt;authentication-ott&gt;</code></div>

			<div abp="3486" class="line number3 index2 alt2" style="text-align: left;"><code abp="3487" class="java plain">}</code></div>
			</div>
			</td>
		</tr>
	</tbody>
</table>
</div>
</div>
</div>
</div>

<p abp="3488"><em abp="3489">&lt;authentication-ott&gt;</em>&nbsp;- The authentication reference number (OTT) provided in the final result of the M-Pin dance between the Client and the M-Pin Server</p>

<p abp="3490"><strong abp="3491">Response:</strong></p>

<p abp="3492"><span abp="3493">200 Authentication successful - on success;</span></p>

<p abp="3494"><span abp="3495">401 Wrong PIN - on unsuccessful authentication;</span></p>

<p abp="3496"><span abp="3497">410 Wrong PIN&nbsp;- after N&nbsp;unsuccessful&nbsp;authentication&nbsp;</span>attempts.</p>

<p abp="3498">408&nbsp;Expired authentication request - the authOTT is invalid or expired.</p>

<p abp="3499"><strong abp="3500">Response Data:</strong></p>

<div abp="3501" class="code panel pdl">
<div abp="3502" class="codeContent panelContent pdl">
<div abp="3503">
<div abp="3504" class="syntaxhighlighter nogutter java" id="highlighter_993226">
<table abp="3505" border="0" cellpadding="0" cellspacing="0" style="float: left;">
	<tbody abp="3506">
		<tr abp="3507">
			<td abp="3508" class="code">
			<div abp="3509" class="container" title="Hint: double-click to select code">
			<div abp="3510" class="line number1 index0 alt2" style="text-align: left;"><code abp="3511" class="java plain">{</code></div>

			<div abp="3512" class="line number2 index1 alt1" style="text-align: left;"><code abp="3513" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3514" class="java string">&quot;status&quot;</code><code abp="3515" class="java plain">: &lt;response-status&gt;,</code></div>

			<div abp="3516" class="line number3 index2 alt2" style="text-align: left;"><code abp="3517" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3518" class="java string">&quot;message&quot;</code><code abp="3519" class="java plain">: &lt;response-message&gt;,</code></div>

			<div abp="3520" class="line number4 index3 alt1" style="text-align: left;"><code abp="3521" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3522" class="java string">&quot;userId&quot;</code><code abp="3523" class="java plain">: &lt;user-id&gt;,</code></div>

			<div abp="3524" class="line number5 index4 alt2" style="text-align: left;"><code abp="3525" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3526" class="java string">&quot;mpinId&quot;</code><code abp="3527" class="java plain">: &lt;mpin-id&gt;</code></div>

			<div abp="3528" class="line number6 index5 alt1" style="text-align: left;"><code abp="3529" class="java plain">}</code></div>
			</div>
			</td>
		</tr>
	</tbody>
</table>
</div>
</div>
</div>
</div>

<p abp="3530"><em abp="3531">&lt;response-status&gt;</em><span abp="3532">&nbsp;- The status of the authentication, either 200, 401 or 410. The same as the HTTP status code</span></p>

<p abp="3533"><span abp="3534"><em abp="3535">&lt;response-message&gt;</em>&nbsp;- Response message for the authentication. The same as the message in the HTTP status - &quot;Authentication successful&quot; or &quot;Wrong PIN&quot;</span></p>

<p abp="3536"><span abp="3537"><em abp="3538">&lt;user-id&gt;</em>&nbsp;- The identity of the user being authenticated.&nbsp;</span></p>

<p abp="3539"><span abp="3540"><em abp="3541">&lt;mpin-id&gt;</em>&nbsp;-&nbsp;The hex-encoded M-Pin ID of the user being authenticated.</span></p>

<h4 abp="3542" id="TechSpec-M-Pinv0.3RelyingPartyService-MobileAuthentication">Mobile Authentication</h4>

<h5 abp="3544" id="TechSpec-M-Pinv0.3RelyingPartyService-POST/loginResult"><span abp="3545">POST /loginResult</span><span abp="3547">&nbsp;</span></h5>

<p abp="3548"><span abp="3549">This request is made by the RPA to inform the RPS for a potential login restriction for the end-user that is currently being authenticated, and to provide optional logout data. This request is mostly useful for the Mobile authentication flow, where the Mobile App should receive as a response to the&nbsp;<span abp="3550">POST /rps/authenticate&nbsp;request a valid status, as well as the required data for a subsequent logout operation.</span><span abp="3552">&nbsp;If the&nbsp;</span><span abp="3553"><em abp="3554">waitForLoginResult</em>&nbsp;configuration option is set to&nbsp;<em abp="3556">True</em>, then the RPS will wait for this request before returning a response to&nbsp;POST /rps/authenticate, otherwise it will return the response right after returning response to the&nbsp;</span><span abp="3558">POST /authenticate&nbsp;request from the RPA.</span>&nbsp;</span></p>

<p abp="3560"><strong abp="3561">Parameters:&nbsp;</strong>&lt;none&gt;<span abp="3562">&nbsp;</span></p>

<p abp="3563"><strong abp="3564">Data:</strong></p>

<table abp="3565" border="0" cellpadding="0" cellspacing="0">
	<tbody abp="3566">
		<tr abp="3567">
			<td abp="3568" class="code">
			<div abp="3569" class="container" title="Hint: double-click to select code">
			<div abp="3570" class="line number1 index0 alt2" style="text-align: left;"><code abp="3571" class="java plain">{</code></div>

			<div abp="3572" class="line number2 index1 alt1" style="text-align: left;"><code abp="3573" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3574" class="java string">&quot;status&quot;</code><code abp="3575" class="java plain">: &lt;status&gt;,</code></div>

			<div abp="3576" class="line number3 index2 alt2" style="text-align: left;"><code abp="3577" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3578" class="java string">&quot;authOTT&quot;</code><code abp="3579" class="java plain">: &lt;authentication-ott&gt;,</code></div>

			<div abp="3580" class="line number4 index3 alt1" style="text-align: left;"><code abp="3581" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3582" class="java string">&quot;logoutURL&quot;</code><code abp="3583" class="java plain">: &lt;logout-endpoint&gt;,</code></div>

			<div abp="3584" class="line number5 index4 alt2" style="text-align: left;"><code abp="3585" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3586" class="java string">&quot;logoutData&quot;</code><code abp="3587" class="java plain">: &lt;logout-data&gt;</code></div>

			<div abp="3588" class="line number6 index5 alt1" style="text-align: left;"><code abp="3589" class="java plain">}</code></div>
			</div>
			</td>
		</tr>
	</tbody>
</table>

<p abp="3590"><em abp="3591" style="font-size: inherit;">&lt;status&gt;</em>&nbsp;- If the RPA doesn&#39;t band the user from logging-in, the status should be 200. Otherwise the status might be 401 or 410. See valid response of&nbsp;POST /rps/authenticate</p>

<p abp="3593"><span abp="3594"><em abp="3595">&lt;authentication-ott&gt;</em>&nbsp;- Authentication reference number (OTT)</span></p>

<p abp="3596"><em abp="3597">&lt;logout-endpoint&gt;</em>&nbsp;- (Optional) Endpoint to which the Mobile App should make request to logout the end-user. This endpoint might be alternatively set in the&nbsp;Configuration<span abp="3599">&nbsp;file</span>.</p>

<p abp="3600"><em abp="3601">&lt;logout-data&gt;</em>&nbsp;- (Optional) Any data that the Mobile App should provide while making request to the&nbsp;<em abp="3602">&lt;logout-endpoint&gt;</em>. This data might be a JSON object as well. If the&nbsp;<em abp="3603">logoutData</em>&nbsp;is not present, then the Mobile App will not present to the end-user the option to logout.<span abp="3604">&nbsp;</span></p>

<p abp="3605"><strong abp="3606">Response:</strong><span abp="3607">&nbsp;200 OK on success, 4xx otherwise</span><span abp="3608">&nbsp;</span></p>

<p abp="3609"><strong abp="3610">Response Data:</strong>&nbsp;&lt;none&gt;</p>

<h5 abp="3611" id="TechSpec-M-Pinv0.3RelyingPartyService-POST/rps/getAccessNumber"><span abp="3612">POST /rps/getAccessNumber</span></h5>

<p abp="3614"><span abp="3615">This request is made by the Client (through a proxy) to obtain the Access Number that is required for authentication through the Mobile Client.</span></p>

<p abp="3616"><strong abp="3617">Parameters:&nbsp;</strong>&lt;none&gt;</p>

<p abp="3618"><strong abp="3619">Data:</strong>&nbsp;&lt;none&gt;</p>

<p abp="3620"><strong abp="3621">Response:</strong><span abp="3622">&nbsp;200 OK on success, 4xx otherwise</span></p>

<p abp="3623"><strong abp="3624">Response Data:</strong><span abp="3625">&nbsp;</span></p>

<div abp="3626" class="code panel pdl">
<div abp="3627" class="codeContent panelContent pdl">
<div abp="3628">
<div abp="3629" class="syntaxhighlighter nogutter java" id="highlighter_391950">
<table abp="3630" border="0" cellpadding="0" cellspacing="0">
	<tbody abp="3631">
		<tr abp="3632">
			<td abp="3633" class="code">
			<div abp="3634" class="container" title="Hint: double-click to select code">
			<div abp="3635" class="line number1 index0 alt2" style="text-align: left;"><code abp="3636" class="java plain">{</code></div>

			<div abp="3637" class="line number2 index1 alt1" style="text-align: left;"><code abp="3638" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3639" class="java string">&quot;localTimeStart&quot;</code><code abp="3640" class="java plain">: &lt;access-number-expiration-start&gt;,</code></div>

			<div abp="3641" class="line number3 index2 alt2" style="text-align: left;"><code abp="3642" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3643" class="java string">&quot;ttlSeconds&quot;</code><code abp="3644" class="java plain">: &lt;access-number-expiration-in-seconds&gt;,</code></div>

			<div abp="3645" class="line number4 index3 alt1" style="text-align: left;"><code abp="3646" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3647" class="java string">&quot;localTimeEnd&quot;</code><code abp="3648" class="java plain">: &lt;access-number-expiration-end&gt;,</code></div>

			<div abp="3649" class="line number5 index4 alt2" style="text-align: left;"><code abp="3650" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3651" class="java string">&quot;webOTT&quot;</code><code abp="3652" class="java plain">: &lt;web-ott&gt;,</code></div>

			<div abp="3653" class="line number6 index5 alt1" style="text-align: left;"><code abp="3654" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3655" class="java string">&quot;accessNumber&quot;</code><code abp="3656" class="java plain">: &lt;access-number&gt;</code></div>

			<div abp="3657" class="line number7 index6 alt2" style="text-align: left;"><code abp="3658" class="java plain">}</code></div>
			</div>
			</td>
		</tr>
	</tbody>
</table>
</div>
</div>
</div>
</div>

<p abp="3659"><em abp="3660">&lt;access-number-expiration-in-seconds&gt;</em><span abp="3661">&nbsp;- Access Number expiration period in seconds.</span></p>

<p abp="3662"><em abp="3663">&lt;access-number-expiration-start&gt;</em>&nbsp;- Start time of Access Number expiration in seconds since the&nbsp;Epoch.</p>

<p abp="3664"><em abp="3665">&lt;access-number-expiration-end&gt;</em>&nbsp;- End time of Access Number expiration in seconds since the Epoch.</p>

<p abp="3666"><em abp="3667">&lt;web-ott&gt;</em>&nbsp;- Reference number (serves as OTT) for the mobile authentication</p>

<p abp="3668"><em abp="3669">&lt;access-number&gt;</em>&nbsp;- The Access Number.</p>

<h5 abp="3670" id="TechSpec-M-Pinv0.3RelyingPartyService-POST/rps/accessnumber">POST /rps/accessnumber</h5>

<p abp="3672">This request is made by the Client (through a proxy) to check whether an end-user has authenticated through the Mobile App. The Client provides the&nbsp;<em abp="3673">webOTT</em>&nbsp;to refer to the relevant mobile authentication transaction. When an end-user has authenticated successfully through the Mobile Client, an&nbsp;<em abp="3674">authOTT</em>&nbsp;is returned, so subsequent authentication&nbsp;requests to the RPA might be executed.</p>

<p abp="3675"><strong abp="3676">Parameters:&nbsp;</strong>&lt;none&gt;</p>

<p abp="3677"><strong abp="3678">Data:</strong></p>

<div abp="3679" class="code panel pdl">
<div abp="3680" class="codeContent panelContent pdl">
<div abp="3681">
<div abp="3682" class="syntaxhighlighter nogutter java" id="highlighter_974108">
<table abp="3683" border="0" cellpadding="0" cellspacing="0">
	<tbody abp="3684">
		<tr abp="3685">
			<td abp="3686" class="code">
			<div abp="3687" class="container" title="Hint: double-click to select code">
			<div abp="3688" class="line number1 index0 alt2" style="text-align: left;"><code abp="3689" class="java plain">{</code></div>

			<div abp="3690" class="line number2 index1 alt1" style="text-align: left;"><code abp="3691" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3692" class="java string">&quot;webOTT&quot;</code><code abp="3693" class="java plain">: &lt;web-ott&gt;</code></div>

			<div abp="3694" class="line number3 index2 alt2" style="text-align: left;"><code abp="3695" class="java plain">}</code></div>
			</div>
			</td>
		</tr>
	</tbody>
</table>
</div>
</div>
</div>
</div>

<p abp="3696"><strong abp="3697">Response:</strong></p>

<p abp="3698"><span abp="3699">200 OK - Successful Authentication.</span></p>

<p abp="3700"><span abp="3701">401 Unauthorized - User has not been authorized successfully yet.</span></p>

<p abp="3702"><strong abp="3703">Response Data:</strong></p>

<p abp="3704">Sent only with 200 OK response</p>

<div abp="3705" class="code panel pdl">
<div abp="3706" class="codeContent panelContent pdl">
<div abp="3707">
<div abp="3708" class="syntaxhighlighter nogutter java" id="highlighter_945200">
<table abp="3709" border="0" cellpadding="0" cellspacing="0">
	<tbody abp="3710">
		<tr abp="3711">
			<td abp="3712" class="code">
			<div abp="3713" class="container" title="Hint: double-click to select code">
			<div abp="3714" class="line number1 index0 alt2" style="text-align: left;"><code abp="3715" class="java plain">{</code></div>

			<div abp="3716" class="line number2 index1 alt1" style="text-align: left;"><code abp="3717" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3718" class="java string">&quot;authOTT&quot;</code><code abp="3719" class="java plain">: &lt;authentication-ott&gt;</code></div>

			<div abp="3720" class="line number3 index2 alt2" style="text-align: left;"><code abp="3721" class="java plain">}</code></div>
			</div>
			</td>
		</tr>
	</tbody>
</table>
</div>
</div>
</div>
</div>

<p abp="3722"><em abp="3723">&lt;authentication-ott&gt;</em>&nbsp;- The authentication reference number (OTT) provided in the final result of the M-Pin dance between the Client and the M-Pin Server.</p>

<h5 abp="3724" id="TechSpec-M-Pinv0.3RelyingPartyService-POST/rps/authenticate">POST /rps/authenticate</h5>

<p abp="3726">This request is made by the Mobile Client (through a proxy) to authenticate an end-user. The Mobile Client passes the&nbsp;<em abp="3727">authOTT</em>&nbsp;that was returned by the M-Pin Server as a result of the M-Pin Dance. The RPS obtains the Authentication Token using the&nbsp;<em abp="3728">authOTT</em>&nbsp;and verifies the result of the authentication.</p>

<p abp="3729"><strong abp="3730">Parameters:&nbsp;</strong>&lt;none&gt;</p>

<p abp="3731"><strong abp="3732">Data:</strong></p>

<div abp="3733" class="code panel pdl">
<div abp="3734" class="codeContent panelContent pdl">
<div abp="3735">
<div abp="3736" class="syntaxhighlighter nogutter java" id="highlighter_736326">
<table abp="3737" border="0" cellpadding="0" cellspacing="0">
	<tbody abp="3738">
		<tr abp="3739">
			<td abp="3740" class="code">
			<div abp="3741" class="container" title="Hint: double-click to select code">
			<div abp="3742" class="line number1 index0 alt2" style="text-align: left;"><code abp="3743" class="java plain">{</code></div>

			<div abp="3744" class="line number2 index1 alt1" style="text-align: left;"><code abp="3745" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3746" class="java string">&quot;mpinResponse&quot;</code><code abp="3747" class="java plain">: {</code></div>

			<div abp="3748" class="line number3 index2 alt2" style="text-align: left;"><code abp="3749" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3750" class="java string">&quot;authOTT&quot;</code><code abp="3751" class="java plain">: &lt;authentication-ott&gt;,</code></div>

			<div abp="3752" class="line number4 index3 alt1" style="text-align: left;"><code abp="3753" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3754" class="java string">&quot;version&quot;</code><code abp="3755" class="java plain">: &lt;mpin-version&gt;,</code></div>

			<div abp="3756" class="line number5 index4 alt2" style="text-align: left;"><code abp="3757" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3758" class="java string">&quot;type&quot;</code><code abp="3759" class="java plain">:&nbsp;</code><code abp="3760" class="java string">&quot;PASS2&quot;</code></div>

			<div abp="3761" class="line number6 index5 alt1" style="text-align: left;"><code abp="3762" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3763" class="java plain">}</code></div>

			<div abp="3764" class="line number7 index6 alt2" style="text-align: left;"><code abp="3765" class="java plain">}</code></div>
			</div>
			</td>
		</tr>
	</tbody>
</table>
</div>
</div>
</div>
</div>

<p abp="3766"><em abp="3767">&lt;authentication-ott&gt;</em>&nbsp;- The authentication reference number (OTT) provided in the final result of the M-Pin dance between the Client and the M-Pin Server.</p>

<p abp="3768"><span abp="3769"><em abp="3770">&lt;mpin-version&gt;</em>&nbsp;- The version of the M-Pin protocol, currently&nbsp;</span><span abp="3771">&quot;0.3&quot;.</span></p>

<p abp="3772"><strong abp="3773">Response:</strong></p>

<p abp="3774">200 Authentication successful - on success;</p>

<p abp="3775">401 Wrong PIN - on unsuccessful authentication;</p>

<p abp="3776">410 Wrong PIN&nbsp;- after N&nbsp;unsuccessful&nbsp;authentication&nbsp;attempts.</p>

<p abp="3777">408&nbsp;Expired authentication request - the authOTT is invalid or expired.</p>

<p abp="3778"><strong abp="3779">Response Data:</strong>&nbsp;&lt;none&gt;</p>

<h3 abp="3780" id="TechSpec-M-Pinv0.3RelyingPartyService-ExpectedAPIfortheRPA"><span abp="3781">Expected API for the RPA</span></h3>

<p abp="3783">The RPA is the only part in the M-Pin system that is strictly specific to each Customer and implements the logic of the specific Web Application. In order for this Web Application to serve as RPA, it should implement the bellow RESTful endpoints. Note that the actual URL&#39;s for the endpoints are customizable, and therefor example endpoint names are shown in the brackets. The actual endpoint URL&#39;s should be configured in the RPS (see&nbsp;<a href="#configuration">Configuration</a>).</p>

<h5 abp="3785" id="TechSpec-M-Pinv0.3RelyingPartyService-End-userVerificationCallbackEndpoint(POST/verify)">End-user Verification Callback Endpoint (POST /verify)</h5>

<p abp="3787">This request is made as part of the end-user registration and activation flow. The request is made by the RPS to the RPA to either verify the end-user identity in-place, or to initiate end-user identity verification process. If the RPA is able to verify the identity in-place, then it should return 200 OK with response data&nbsp;<code abp="3788">{&nbsp;</code><span abp="3789"><code abp="3790">&quot;forceActivate&quot;: true }</code>. If a verification process has been started (e.g. via sending a verification e-mail to the end-user), then the RPA should make a&nbsp;</span><span abp="3791">POST /user/&lt;mpin-id&gt;&nbsp;request to the RPS when the user identity has been verified, providing the same&nbsp;<em abp="3793">activateKey</em>&nbsp;that was received in this request.</span></p>

<p abp="3794"><strong abp="3795">Parameters:</strong>&nbsp;&lt;none&gt;</p>

<p abp="3796"><strong abp="3797">Data:</strong></p>

<div abp="3798" class="code panel pdl">
<div abp="3799" class="codeContent panelContent pdl">
<div abp="3800">
<div abp="3801" class="syntaxhighlighter nogutter java" id="highlighter_908552">
<table abp="3802" border="0" cellpadding="0" cellspacing="0">
	<tbody abp="3803">
		<tr abp="3804">
			<td abp="3805" class="code">
			<div abp="3806" class="container" title="Hint: double-click to select code">
			<div abp="3807" class="line number1 index0 alt2" style="text-align: left;"><code abp="3808" class="java plain">{</code></div>

			<div abp="3809" class="line number2 index1 alt1" style="text-align: left;"><code abp="3810" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3811" class="java string">&quot;activateKey&quot;</code><code abp="3812" class="java plain">: &lt;activate-key&gt;,</code></div>

			<div abp="3813" class="line number3 index2 alt2" style="text-align: left;"><code abp="3814" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3815" class="java string">&quot;mpinId&quot;</code><code abp="3816" class="java plain">: &lt;mpin-id&gt;,</code></div>

			<div abp="3817" class="line number4 index3 alt1" style="text-align: left;"><code abp="3818" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3819" class="java string">&quot;mobile&quot;</code><code abp="3820" class="java plain">: &lt;</code><code abp="3821" class="java value">0</code><code abp="3822" class="java plain">|</code><code abp="3823" class="java value">1</code><code abp="3824" class="java plain">&gt;,</code></div>

			<div abp="3825" class="line number5 index4 alt2" style="text-align: left;"><code abp="3826" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3827" class="java string">&quot;userId&quot;</code><code abp="3828" class="java plain">: &lt;user-id&gt;,</code></div>

			<div abp="3829" class="line number6 index5 alt1" style="text-align: left;"><code abp="3830" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3831" class="java string">&quot;expireTime&quot;</code><code abp="3832" class="java plain">: &lt;utc-formatted-expiration-time&gt;,</code></div>

			<div abp="3833" class="line number7 index6 alt2" style="text-align: left;"><code abp="3834" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3835" class="java string">&quot;resend&quot;</code><code abp="3836" class="java plain">: &lt;</code><code abp="3837" class="java keyword">true</code><code abp="3838" class="java plain">|</code><code abp="3839" class="java keyword">false</code><code abp="3840" class="java plain">&gt;,</code></div>

			<div abp="3841" class="line number8 index7 alt1" style="text-align: left;"><code abp="3842" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3843" class="java string">&quot;deviceName&quot;</code><code abp="3844" class="java plain">: &lt;device-name&gt;</code></div>

			<div abp="3845" class="line number9 index8 alt2" style="text-align: left;"><code abp="3846" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3847" class="java string">&quot;userData&quot;</code><code abp="3848" class="java plain">: &lt;user-data&gt;</code></div>

			<div abp="3849" class="line number10 index9 alt1" style="text-align: left;"><code abp="3850" class="java plain">}</code></div>
			</div>
			</td>
		</tr>
	</tbody>
</table>
</div>
</div>
</div>
</div>

<p abp="3851"><em abp="3852">&lt;activation-key&gt;</em>&nbsp;- An activation reference number, identifying the specific end-user verification and activation process.</p>

<p abp="3853"><em abp="3854">&lt;mpin-id&gt;</em>&nbsp;-&nbsp;The hex-encoded M-Pin ID of the user being registered/set-up.</p>

<p abp="3855"><em abp="3856">&lt;mobile&gt;</em>&nbsp;- Indicates (1 or 0) whether the flow is carried out by the mobile client (1), or not (0).</p>

<p abp="3857"><em abp="3858">&lt;user-id&gt;</em>&nbsp;- The identity of the user being&nbsp;registered/set-up.</p>

<p abp="3859"><em abp="3860">&lt;utc-formatted-expiration-time&gt;</em>&nbsp;- Expiration time for the user setup flow in case the RPS should wait for the user verification to be completed.</p>

<p abp="3861"><em abp="3862">&lt;resend&gt;</em>&nbsp;- Indicates (true or false) whether the setup flow for that user was just started, or re-started. If the end-user failed to receive the a verification e-mail (for instance) and requests to re-send the e-mail, this flag will be&nbsp;<code abp="3863">true</code>.</p>

<p abp="3864"><em abp="3865">&lt;device-name&gt;</em>&nbsp;- A friendly name describing the device from which the user is trying to register. The RPA might associate and save this name with the&nbsp;<em abp="3866">mpin-id</em>&nbsp;in order to be able later to recognize the&nbsp;<em abp="3867">mpin-id</em>&nbsp;given the device name.</p>

<p abp="3868"><em abp="3869">&lt;user-data&gt;</em>&nbsp;- Some opaque&nbsp;user data that is sent by the PIN Pad during the&nbsp;<em abp="3870">PUT /rps/user[/&lt;mpin-id&gt;]</em>&nbsp;request to the RPS. The RPS just passes that data to the RPA &quot;as is&quot;. This data might be used by the RPA as additional assistance the end-user verification process. The data might be set via the PIN Pad&nbsp;<span abp="3871"><em abp="3872">registerRequestFormatter()</em>&nbsp;callback</span></p>

<p abp="3873"><strong abp="3874">Response:</strong></p>

<p abp="3875">200 OK - user identity is verified or a verification process has been started</p>

<p abp="3876"><span abp="3877">4xx - user verification has failed.</span></p>

<p abp="3878"><strong abp="3879">Response Data:</strong></p>

<div abp="3880" class="code panel pdl">
<div abp="3881" class="codeContent panelContent pdl">
<div abp="3882">
<div abp="3883" class="syntaxhighlighter nogutter java" id="highlighter_935129">
<table abp="3884" border="0" cellpadding="0" cellspacing="0">
	<tbody abp="3885">
		<tr abp="3886">
			<td abp="3887" class="code">
			<div abp="3888" class="container" title="Hint: double-click to select code">
			<div abp="3889" class="line number1 index0 alt2" style="text-align: left;"><code abp="3890" class="java plain">{</code></div>

			<div abp="3891" class="line number2 index1 alt1" style="text-align: left;"><code abp="3892" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3893" class="java string">&quot;forceActivate&quot;</code><code abp="3894" class="java plain">: &lt;</code><code abp="3895" class="java keyword">true</code><code abp="3896" class="java plain">|</code><code abp="3897" class="java keyword">false</code><code abp="3898" class="java plain">&gt;</code></div>

			<div abp="3899" class="line number3 index2 alt2" style="text-align: left;"><code abp="3900" class="java plain">}</code></div>
			</div>
			</td>
		</tr>
	</tbody>
</table>
</div>
</div>
</div>
</div>

<p abp="3901"><em abp="3902"><span abp="3903">forceActive</span></em><span abp="3904">&nbsp;should be set to&nbsp;<code abp="3905">true</code>&nbsp;if the end-user has been verified in-place and the RPS should not expect further&nbsp;POST /user/&lt;mpin-id&gt;&nbsp;request to activate the user.</span></p>

<h5 abp="3907" id="TechSpec-M-Pinv0.3RelyingPartyService-End-userPermissionCallbackEndpoint(GET/permitUser?mpin_id=&lt;mpin-id&gt;)"><span abp="3908">End-user Permission Callback&nbsp;</span>Endpoint&nbsp;<span abp="3911">(GET /permitUser?mpin_id=&lt;mpin-id&gt;)</span></h5>

<p abp="3912"><span abp="3913">This request is optionally made as part of the end-user authentication flow. It is not mandatory to implement this endpoint. If implemented, the RPS will make this request to the RPA in order to assert that the end-user authentication might proceed on, and it can request the time permit shares for that user.</span></p>

<p abp="3914"><span abp="3915">If this endpoint is not set in the RPS configuration,&nbsp;<span abp="3916">the RPS won&#39;t make this request and will assume that the RPA is not interested to revoke any end-users.</span></span></p>

<p abp="3917"><strong abp="3918">Parameters:</strong>&nbsp;mpin_id=&lt;mpin-id&gt;</p>

<p abp="3919"><em abp="3920">&lt;mpin-id&gt;</em>&nbsp;is the hex-encoded M-Pin ID.</p>

<p abp="3921"><strong abp="3922">Data:</strong>&nbsp;&lt;none&gt;</p>

<p abp="3923"><strong abp="3924">Response:</strong></p>

<p abp="3925">200 OK - end-user is permitted to proceed with authentication</p>

<p abp="3926"><span abp="3927">4xx - end-user is not permitted not&nbsp;proceed with authentication</span></p>

<p abp="3928"><strong abp="3929">Response Data:</strong>&nbsp;&lt;none&gt;</p>

<h5 abp="3930" id="TechSpec-M-Pinv0.3RelyingPartyService-End-userAuthenticationEndpoint(POST/authenticate)">End-user Authentication&nbsp;<span abp="3932">Endpoint&nbsp;</span><span abp="3933">(POST /authenticate)</span></h5>

<p abp="3934">This request is part of the end-user authentication flow. It is made by the PIN Pad to the RPA in order to verify the end-user authentication against the M-Pin Server. The PIN Pad first authenticates the end-user against the M-Pin Server and afterwards send the result of that authentication to the RPA for verification. The RPA should then make&nbsp;<span abp="3935">POST /authenticate</span><span abp="3937">&nbsp;request to the RPS, sending only the&nbsp;</span><em abp="3938">authOTT</em><span abp="3939">&nbsp;in the request data. The RPS verifies that this&nbsp;<em abp="3940">authOTT</em>&nbsp;corresponds to a valid Authentication Token</span><span abp="3941">&nbsp;and returns status. The RPA should return the same status in the response to to the PIN Pad, but it can return also some custom response data that might be used on the client side.</span></p>

<p abp="3942"><span abp="3943">Implementing this endpoint is mandatory, and its URL should be set in the RPS configuration. The RPS will propagate it to the PIN Pad within the&nbsp;Client Settings.</span></p>

<p abp="3945"><strong abp="3946">Parameters:</strong>&nbsp;&lt;none&gt;</p>

<p abp="3947"><strong abp="3948">Data:</strong></p>

<div abp="3949" class="code panel pdl">
<div abp="3950" class="codeContent panelContent pdl">
<div abp="3951">
<div abp="3952" class="syntaxhighlighter nogutter java" id="highlighter_694304">
<table abp="3953" border="0" cellpadding="0" cellspacing="0">
	<tbody abp="3954">
		<tr abp="3955">
			<td abp="3956" class="code">
			<div abp="3957" class="container" title="Hint: double-click to select code">
			<div abp="3958" class="line number1 index0 alt2" style="text-align: left;"><code abp="3959" class="java plain">{</code></div>

			<div abp="3960" class="line number2 index1 alt1" style="text-align: left;"><code abp="3961" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3962" class="java string">&quot;mpinResponse&quot;</code><code abp="3963" class="java plain">: {</code></div>

			<div abp="3964" class="line number3 index2 alt2" style="text-align: left;"><code abp="3965" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3966" class="java string">&quot;version&quot;</code><code abp="3967" class="java plain">:&nbsp;</code><code abp="3968" class="java string">&quot;0.3&quot;</code><code abp="3969" class="java plain">,</code></div>

			<div abp="3970" class="line number4 index3 alt1" style="text-align: left;"><code abp="3971" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3972" class="java string">&quot;authOTT&quot;</code><code abp="3973" class="java plain">: &lt;authentication-ott&gt;,</code></div>

			<div abp="3974" class="line number5 index4 alt2" style="text-align: left;"><code abp="3975" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3976" class="java string">&quot;pass&quot;</code><code abp="3977" class="java plain">:&nbsp;</code><code abp="3978" class="java value">2</code></div>

			<div abp="3979" class="line number6 index5 alt1" style="text-align: left;"><code abp="3980" class="java spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code abp="3981" class="java plain">}</code></div>

			<div abp="3982" class="line number7 index6 alt2" style="text-align: left;"><code abp="3983" class="java plain">}</code></div>
			</div>
			</td>
		</tr>
	</tbody>
</table>
</div>
</div>
</div>
</div>

<p abp="3984"><em abp="3985">&lt;authentication-ott&gt;</em>&nbsp;- Authentication reference number (OTT)</p>

<p abp="3986"><strong abp="3987">Response:&nbsp;</strong><span abp="3988">The response should be basically the same as the one returned by the RPS&nbsp;</span><em abp="3989">POST /<span abp="3990">authenticate&nbsp;</span></em><span abp="3991">request</span></p>

<p abp="3992">200 Authentication successful - on success;</p>

<p abp="3993">401 Wrong PIN - on unsuccessful authentication;</p>

<p abp="3994">410 Wrong PIN&nbsp;- after N&nbsp;unsuccessful&nbsp;authentication&nbsp;attempts.</p>

<p abp="3995">408&nbsp;Expired authentication request - the authOTT is invalid or expired.</p>

<p abp="3996"><strong abp="3997">Response Data:&nbsp;</strong>&lt;none&gt; or any JSON-formatted application-specific data.&nbsp;This data might be used on the front-end side to implement any application-specific logic<span abp="3998">.</span></p>

<h3 abp="3999" id="TechSpec-M-Pinv0.3RelyingPartyService-Workflows"><span abp="4000">Workflows</span></h3>

<h4 abp="4002" id="TechSpec-M-Pinv0.3RelyingPartyService-M-PinSetup">End user registration flow</h4>

<p abp="4004"><img abp="4005" class="confluence-embedded-image" confluence-query-params="effects=border-simple,shadow-kn" data-image-src="/download/attachments/11534356/M-Pin%20Setup.png?version=11&amp;modificationDate=1413213302000&amp;api=v2&amp;effects=border-simple,shadow-kn" height="1413" src="http://docs.miracl.com/userfiles/1995/3089/ckfinder/images/M-Pin%20Setup.png?dc=201502241747-0" style="margin-right: auto; margin-left: auto; display: block;" width="1260" /></p>

<h4 abp="4006" id="TechSpec-M-Pinv0.3RelyingPartyService-M-PinAuthentication">End user authentication flow</h4>

<p abp="4008"><img abp="4009" class="confluence-embedded-image" confluence-query-params="effects=border-simple,shadow-kn" data-image-src="/download/attachments/11534356/M-Pin%20Authentication.png?version=8&amp;modificationDate=1413213302000&amp;api=v2&amp;effects=border-simple,shadow-kn" height="1163" src="http://docs.miracl.com/userfiles/1995/3089/ckfinder/images/M-Pin%20Authentication(1).png?dc=201502241747-0" style="margin-right: auto; margin-left: auto; display: block;" width="1261" /></p>

<h4 abp="4010" id="TechSpec-M-Pinv0.3RelyingPartyService-M-PinMobileAuthentication">End user mobile authentication</h4>

<p abp="4012"><img abp="4013" class="confluence-embedded-image" confluence-query-params="effects=border-simple,shadow-kn" data-image-src="/download/attachments/11534356/M-Pin%20Mobile%20Authentication.png?version=7&amp;modificationDate=1413213302000&amp;api=v2&amp;effects=border-simple,shadow-kn" height="1310" src="http://docs.miracl.com/userfiles/1995/3089/ckfinder/images/M-Pin%20Mobile%20Authentication.png?dc=201502241747-0" style="margin-right: auto; margin-left: auto; display: block;" width="1256" /></p>



<h2 abp="4035" id="TechSpec-M-Pinv0.3RelyingPartyService-Configuration">Configuration</h2>

<div abp="4037" class="code panel pdl">
<div abp="4038" class="codeHeader panelHeader pdl"><strong>language</strong> py</div>

<div abp="4038" class="codeHeader panelHeader pdl"><strong abp="4039">title </strong>&lt;installation-folder&gt;/config_rps.py</div>

<div abp="4040" class="codeContent panelContent pdl">
<div abp="4041">
<div abp="4042" class="syntaxhighlighter nogutter java" id="highlighter_118831">
<table abp="4043" border="0" cellpadding="0" cellspacing="0">
	<tbody abp="4044">
		<tr abp="4045">
			<td abp="4046" class="code">
			<div abp="4047" class="container" title="Hint: double-click to select code">
			<pre abp="4048" class="computer_code" style="text-align: left;">
from __future__ import unicode_literals
 
&quot;&quot;&quot;HTTP server settings&quot;&quot;&quot;
address = &lt;rps-listen-address&gt;
port = &lt;rps-port&gt;
 
&quot;&quot;&quot;Set Access-Control-Allow-Origin header&quot;&quot;&quot;
allowOrigin = &lt;access-control-allow-origin&gt;
 
&quot;&quot;&quot;Time synchronization
To be able to perform time based verification, by default RPS syncs its time
with CertiVox servers. If you set it to False, you should still sync the server
using an accurate NTP time server!
&quot;&quot;&quot;
syncTime = &lt;sync-time&gt;
 
&quot;&quot;&quot;
Dynamic options url
Location to be queried for dynamically (runtime) changeable options.
&#39;None&#39; mean dynamic options are disabled and it is default value.
&quot;&quot;&quot;
dynamicOptionsURL = &lt;dynamic-options-url&gt;
 
&quot;&quot;&quot;The location of your keys file (relative to mpin-backend/servers/dta).&quot;&quot;&quot;
credentialsFile = &lt;credentials-file&gt;
 
&quot;&quot;&quot;Entropy sources
D-TA supports multiple ways to gather entropy random, urandom, certivox or
combination of those.
&quot;&quot;&quot;
EntropySources = &lt;entropy-source&gt;
 
&quot;&quot;&quot;CertiVox server secret share acquisition
- dta - get server secret from CertiVox dta automatically on start
- credentials.json - get server secret from credentials.json (key: certivox_server_secret)
- manual - service will prompt for it
- the secret itself
You can get your CertiVox server secret by:
    ./scripts/getServerSecretShare.py credentials.json
which will output your credentials json including certivox_server_secret.
NOTE: Don&#39;t pipe it directly to the same file - you&#39;ll lose your original
      credentials file.
Alternatively you can copy only your certivox_server_secret value and supply it
either manually or via config.py setting the certivoxServerSecret to the
corresponding value.
&quot;&quot;&quot;
certivoxServerSecret = &lt;server-secret-source&gt;
 
&quot;&quot;&quot;Local DTA address.&quot;&quot;&quot;
DTALocalURL = &lt;local-dta-url&gt;
 
&quot;&quot;&quot;Access number options
- enable access number
- accessNumberExpireSeconds - The default time client will show the access number
- accessNumberExtendValiditySeconds - Validity of the access number (on top of accessNumberExpireSeconds)
- accessNumberUseCheckSum - Should access number have checksum
&quot;&quot;&quot;
requestOTP = &lt;request-otp&gt;
accessNumberExpireSeconds = &lt;access-number-expiration-in-seconds&gt;
accessNumberExtendValiditySeconds = &lt;access-number-extend-validity-in-seconds&gt;
accessNumberUseCheckSum = &lt;access-number-use-checksum&gt;
 
&quot;&quot;&quot;Authentication options
- waitForLoginResult -For the mobile flow. Wait the browser login before showing the Done/Logout button.
&quot;&quot;&quot;
waitForLoginResult = &lt;wait-for-login-result&gt;
VerifyUserExpireSeconds = &lt;user-verification-expiration-in-seconds&gt;
maxInvalidLoginAttempts = &lt;max-invalid-login-attempts&gt;
cacheTimePermits = &lt;cache-time-permits&gt;
 
&quot;&quot;&quot;RPA options
- RPAPermitUserURL - RPA Revocation endpoint
- RegisterForwardUserHeaders - Coma separated list of headers
    - &#39;&#39; - do not forward headers
    - * - forward all headers
- LogoutURL - RPA Logout url. For logout using the mobile client.
&quot;&quot;&quot;
RPAVerifyUserURL = &lt;rpa-verify-user-endpoint&gt;
RPAPermitUserURL = &lt;rpa-permit-user-endpoint&gt;
RPAAuthenticateUserURL = &lt;rpa-auth-validation-endpoint&gt;
RegisterForwardUserHeaders = &lt;forward-headers&gt;
LogoutURL = &lt;logout-endpoint&gt;
 
&quot;&quot;&quot;PIN pad client options&quot;&quot;&quot;
rpsBaseURL = &lt;rps-public-requests-base-url&gt;
rpsPrefix = &lt;rps-public-requests-prefix&gt;
setDeviceName = &lt;set-device-name&gt;
 
&quot;&quot;&quot;Key value storage options&quot;&quot;&quot;
storage = &lt;storage&gt;
 
redisHost = &lt;redis-host&gt;
redisPort = &lt;redis-port&gt;
redisDB = &lt;redis-db&gt;
redisPassword = &lt;redis-password&gt;
redisPrefix = &lt;redis-prefix&gt;
 
fileStorageLocation = &lt;json-storage-file-name&gt;
 
&quot;&quot;&quot;Debug options&quot;&quot;&quot;
logLevel = &lt;log-level&gt;</pre>
			</div>
			</td>
		</tr>
	</tbody>
</table>
</div>
</div>
</div>
</div>

<p abp="4134"><em abp="4135">&lt;rps-port&gt;</em>&nbsp;- The port on which the RPS listens. Example: 8011</p>

<p abp="4138"><em abp="4139">&lt;rps-public-requests-base-url&gt;</em><span abp="4140">&nbsp;- Base URL for the Public RPS API. This is address of the proxy, through which RPS requests might be done and could be relative. The client will append to this URL &quot;/rps/&lt;endpoint&gt;&quot; to make a request to the RPS. Example (Default):</span>&quot;&quot; (empty)</p>

<p abp="4142"><em abp="4143">&lt;rps-public-requests-prefix&gt;</em>&nbsp;- The prefix for Public RPS API. Example (Default): &quot;rps&quot;</p>

<p abp="4144"><span abp="4145"><em abp="4146">&lt;credentials-file&gt;</em>&nbsp;- The file that includes the Customer credential&nbsp;as App ID and App Key. Example:&nbsp;</span><span abp="4147">&quot;/opt/mpin/credentials.json&quot;</span></p>

<p abp="4148">&lt;entropy-source&gt;&nbsp;- Defines where the RPS gets entropy from. Two sources are available &#39;dev_urandom&#39; and &#39;certivox&#39; as each one could be used to get the whole entropy from, or both could be combined with a specific percentage of entropy to be retrieved from each source. Examples: &#39;dev_urandom:100&#39; (the Default), &#39;dev_urandom:60,certivox:40&#39;.</p>

<p abp="4148"><em style="margin: 0px; padding: 0px; border: none;"><span class="diff-html-added" style="margin: 0px; padding: 2px 4px; border: 0px rgb(147, 196, 159);">&lt;server-secret-source&gt;</span></em><span class="diff-html-added" style="margin: 0px; padding: 2px 4px; border: 0px rgb(147, 196, 159);">&nbsp;- Defines where the RPS, serving as a M-Pin Auth. Server, should take its Server Secret from. The available options are:</span></p>

<ul class="diff-block-target diff-block-context" style="font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif; margin: 10px 0px 0px 40px; padding: 0px; border: none; color: rgb(51, 51, 51); font-size: 12px; line-height: 17.1429px; background-color: rgb(255, 255, 255);">
	<li><span class="diff-html-added" style="margin: 0px; padding: 2px 4px; border: 0px rgb(147, 196, 159);">&#39;dta&#39; - get the secret from the D-TA</span></li>
	<li><span class="diff-html-added" style="margin: 0px; padding: 2px 4px; border: 0px rgb(147, 196, 159);">&#39;credentials.json&#39; - read it from the credentials file</span></li>
	<li><span class="diff-html-added" style="margin: 0px; padding: 2px 4px; border: 0px rgb(147, 196, 159);">&#39;manual&#39; - the RPS will prompt to read it from the user/admin</span></li>
	<li><span class="diff-html-added" style="margin: 0px; padding: 2px 4px; border: 0px rgb(147, 196, 159);">Explicitly specified in the config file.</span></li>
</ul>

<p class="diff-block-target diff-block-context" style="font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif; margin: 10px 0px 0px 30px; padding: 0px; border: none; color: rgb(110, 112, 110); font-size: 12px; line-height: 17.1429px; background-color: rgb(255, 255, 255);"><span style="color:#000000;"><span style="font-size:14px;"><span class="diff-html-added" style="margin: 0px; padding: 2px 4px; border: 0px rgb(147, 196, 159);">Example (Default): &#39;dta&#39;</span></span></span></p>

<p abp="4148"><em abp="4152">&lt;rpa-verify-user-endpoint&gt;</em>&nbsp;- The RPA endpoint for end-user identity verification. Example:&nbsp;&quot;http://127.0.0.1:8005/mpinVerify&quot;</p>

<p abp="4153"><em abp="4154">&lt;rpa-auth-validation-endpoint&gt;</em><span abp="4155">&nbsp;- Endpoint implemented by the RPA for&nbsp;</span>authentication&nbsp;validation.&nbsp;<span abp="4157">Example: &quot;/mpinAuthenticate&quot;</span></p>

<p abp="4158"><span abp="4159"><em abp="4160">&lt;rpa-permit-user-endpoint&gt;</em>&nbsp;- Endpoint implemented by the RPA for&nbsp;end-user revocation. Example: &quot;http://127.0.0.1:8005/mpinPermitUser&quot;</span></p>

<p abp="4161"><em abp="4162">&lt;local-dta-url&gt;</em>&nbsp;- The URL for the Customer-hosted D-TA Service. Example:&nbsp;<span abp="4163">&quot;http://127.0.0.1:8001&quot;</span></p>

<p abp="4164"><span abp="4165"><em abp="4166">&lt;wait-for-login-result&gt;</em>&nbsp;- Indicates (True or False) whether the RPS should wait for the&nbsp;</span><span abp="4167">POST /loginResult&nbsp;request before returning response to&nbsp;POST /rps/authenticate.</span></p>

<p abp="4168"><span abp="4169"><em abp="4170">&lt;logout-endpoint&gt;</em>&nbsp;- Default endpoint, typically implemented by the RPA, to which the Mobile App should make the logout request. This endpoint might be overwritten with the&nbsp;POST /loginResult, or alternatively might not be set as configuration option, but provided only during the request. Example: &quot;/logout&quot;</span></p>

<p abp="4171"><em abp="4172">&lt;set-device-name&gt;</em>&nbsp;- Indication&nbsp;(True or False) that is send from the RPS to the Client within the Client Settings. If set to&nbsp;<em abp="4173">True</em>, the Client should obtain a friendly device name and send it to the RPS within the&nbsp;PUT /rps/user&nbsp;request. The RPS will then forward it to the RPA within the&nbsp;POST /verify&nbsp;request.</p>

<p abp="4174"><em abp="4175">&lt;request-otp&gt;</em><span abp="4176">&nbsp;- Indicates (True or False) whether One-Time Password should be generated on successful&nbsp;authentication.&nbsp;</span><span abp="4177">Used for the Arion Server.</span></p>

<p abp="4178"><em abp="4179">&lt;access-number-expiration-in-seconds&gt;</em><span abp="4180">&nbsp;- Access Number expiration period in seconds.</span></p>

<p abp="4178"><em abp="4179">&lt;access-number-extend-validity-in-seconds&gt;</em>&nbsp;Additional extension in seconds of the Access Number validity. While the previous number&nbsp;<em style="font-family: Verdana, Arial, Helvetica, sans-serif; line-height: 19.2px; font-size: 14px; background-color: rgb(255, 255, 255);"><span class="diff-html-added" style="margin: 0px; padding: 2px 4px; border: 0px rgb(147, 196, 159);">&lt;access-number-expiration-in-seconds&gt;</span></em>&nbsp;is the one that the user sees in the UI. This additional extension is invisible and is meant to allow the user to enter an access number in the last seconds of the timeout period, and it is still processed. Example (Default): 5</p>

<p abp="4178"><span abp="4182"><em abp="4182">&lt;access-number-use-checksum&gt;</em>&nbsp;- Indicates (True or False) whether the generated Access Number includes a checksum digit, or not. This option is also provided in the client settings so the Client can act accordingly.</span></p>

<p abp="4181"><em abp="4182">&lt;user-verification-expiration-in-seconds&gt;</em>&nbsp;- Expiration time in seconds for the end-user identity verification completion. Example:&nbsp;<span abp="4183">3600</span></p>

<p abp="4193"><span abp="4194"><em abp="4195">&lt;storage&gt;</em>&nbsp;- The storage mechanism that the RPS should use. Currently available storage&#39;s are &quot;memory&quot; (default), &quot;redis&quot;</span></p>

<p abp="4196"><em abp="4197">&lt;redis-host&gt;</em>&nbsp;- The address of the Redis storage to be used in case that storage option is set to &quot;redis&quot;. Example: &quot;127.0.0.1&quot;</p>

<p abp="4204"><em abp="4205">&lt;redis-prefix&gt;</em>&nbsp;- Prefix to be used when storing elements on Redis. Example: &quot;mpin&quot;</p>

<p abp="4204"><em style="margin: 0px; padding: 0px; border: none;"><span class="diff-html-added" style="margin: 0px; padding: 2px 4px; border: 0px rgb(147, 196, 159);">&lt;json-storage-file-name&gt;</span></em><span class="diff-html-added" style="margin: 0px; padding: 2px 4px; border: 0px rgb(147, 196, 159);">&nbsp;- Path and name for the JSON-formatted file to be used as a storage. This option is useful when several RPS instances are running on the same machine for better CPU core utilization.</span></p>

<p abp="4204"><em style="margin: 0px; padding: 0px; border: none;"><span class="diff-html-added" style="margin: 0px; padding: 2px 4px; border: 0px rgb(147, 196, 159);">&lt;access-control-allow-origin&gt;</span></em><span class="diff-html-added" style="margin: 0px; padding: 2px 4px; border: 0px rgb(147, 196, 159);">&nbsp;- a list of origins that are specified in the Access-Control-Allow-Origin header. The format is a comma-separated list, enclosed by square brackets. The default is to allow any origin -&nbsp;[&#39;*&#39;]&nbsp;</span></p>

<p abp="4204"><em style="margin: 0px; padding: 0px; border: none;"><span class="diff-html-added" style="margin: 0px; padding: 2px 4px; border: 0px rgb(147, 196, 159);">&lt;sync-time&gt;</span></em><span style="margin: 0px; padding: 2px 4px; border: 0px rgb(147, 196, 159);">&nbsp;- Indicates (True or False) whether the RPS should make an attempt to syn its time with the CertiVox API. The RPS should be in sync with the rest of the services in any case, but the machine on which it is running might be synced through&nbsp;other means, like NTP.</span></p>

<p abp="4204"><em style="margin: 0px; padding: 0px; border: none;"><span class="diff-html-added" style="margin: 0px; padding: 2px 4px; border: 0px rgb(147, 196, 159);">&lt;max-invalid-login-attempts&gt;</span></em><span class="diff-html-added" style="margin: 0px; padding: 2px 4px; border: 0px rgb(147, 196, 159);">&nbsp;- The number of consecutive invalid login attempts after which the end-user is blocked. Example (Default): 3</span></p>

<p abp="4204"><em style="margin: 0px; padding: 0px; border: none;"><span class="diff-html-added" style="margin: 0px; padding: 2px 4px; border: 0px rgb(147, 196, 159);">&lt;cache-time-permits&gt;</span></em><span class="diff-html-added" style="margin: 0px; padding: 2px 4px; border: 0px rgb(147, 196, 159);">&nbsp;- Indicates (True or False) whether the RPS should cache the time permits that the local D-TA generates. If they are cached, it is done either in memory on in the Redis database.</span></p>

<p abp="4204"><em style="margin: 0px; padding: 0px; border: none;"><span class="diff-html-added" style="margin: 0px; padding: 2px 4px; border: 0px rgb(147, 196, 159);">&lt;dynamic-options-url&gt;</span></em><span class="diff-html-added" style="margin: 0px; padding: 2px 4px; border: 0px rgb(147, 196, 159);">&nbsp;- URL to retrieve dynamic configuration options from. This option allows the RPA to provide an endpoint from which the RPS could retrieve some of the config options. This way the RPA could control some of the RPS&#39;s config options. If not specified or set to &#39;None&#39;, the RPS won&#39;t query for dynamic options, which is the default.</span></p>
</div>
