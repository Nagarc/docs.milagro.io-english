---
currentMenu: milagro-mfa-mobile-sdk-init-config-methods-android
---

<div id="generated-toc" class="generate_from_h2"></div>

<h1><span style="font-size: 28px;">Initialization and Configuration Methods</span></h1>
<h2>Overview</h2>
<p class="MsoNormal">This page provides a list and brief description of the Initialization and Configuration methods used in the Milagro Mobile SDK for Android. They relate to initializing the SDK and configuring the back-end URL.</p>
<p class="MsoNormal">To view the other methods, refer to the <a href="#">API Reference</a> page.</p>

<h1>MPinSDK</h1>
<!-- MsoSubtitle -->
<h2>Description</h2>
This method constructs an SDK instance.

<!-- Standard Paragraph -->
<h2>Definition</h2>
<!-- Standard Paragraph -->
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt; background: #E2EFD9; margin-left: 0in; margin-right: 0in;">
<p class="CVXAPIDefinition"><b><span style="line-height: 105%; font-family: 'Courier New';">MPinSDK()</span></b></p>

</div>
<h2 class="Body">Parameters</h2>
None
<h2>Return Values</h2>
None
<h2>Example</h2>
The following example initializes an instance and sets the back-end service to http://ec2-54-77-232-113.eu-west-1.compute.amazonaws.com.
<div>
<pre class="computer_code">// Create a new MPinSDK instance
MPinSDK sdk = new MPinSDK();

// Initialize the SDK
HashMap&lt;String, String&gt; config = new HashMap&lt;&gt;();
config.put("backend", "http://ec2-54-77-232-113.eu-west-1.compute.amazonaws.com");

Status status = sdk.Init(config, context);</pre>
</div>
<h1><strong>Init</strong></h1>
<h2>Description</h2>
This method initializes the SDK. It receives a key/value map of the configuration parameters. The additional <code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0.2em 0px; margin: 0px; border-radius: 3px; color: #333333; background-color: rgba(0, 0, 0, 0.0392157);">context</code> parameter is of type <code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0.2em 0px; margin: 0px; border-radius: 3px; color: #333333; background-color: rgba(0, 0, 0, 0.0392157);">android.content.Context</code> and is usually retrieved from the system's <code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0.2em 0px; margin: 0px; border-radius: 3px; color: #333333; background-color: rgba(0, 0, 0, 0.0392157);">getApplicationContext()</code>method.
<h2>Definition</h2>
<div>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt; background: #E2EFD9; margin-left: 0in; margin-right: 0in;">
<p class="CVXAPIDefinition"><b><span style="line-height: 105%; font-family: 'Courier New';">Status Init(Map&lt;String, String&gt; config, Context context)</span></b></p>

</div>
</div>
<h2>Parameters</h2>
<table class="MsoNormalTable" style="margin-left: -.4pt; border-collapse: collapse;" border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td style="border: solid windowtext 1.0pt; background: #F4F4F4; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;"><b><span style="color: #7f7f7f;">Parameter Name</span></b></p>
</td>
<td style="border: solid windowtext 1.0pt; border-left: none; background: #F4F4F4; padding: 0in 5.75pt 0in 5.75pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;"><b><span style="color: #7f7f7f;">Parameter Type</span></b></p>
</td>
<td style="border: solid windowtext 1.0pt; border-left: none; background: #F4F4F4; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;"><b><span style="color: #7f7f7f;">Required?</span></b></p>
</td>
<td style="border: solid windowtext 1.0pt; border-left: none; background: #F4F4F4; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;"><b><span style="color: #7f7f7f;">Description</span></b></p>
</td>
</tr>
<tr>
<td style="border: solid windowtext 1.0pt; border-top: none; background: #E2EFD9; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="CVXAPIParameterName"><b><i><span style="font-family: 'Courier New';">config</span></i></b></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; background: #E2EFD9; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;">Map&lt;String, String&gt;</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;">Yes</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal">Key/value dictionary of initialization parameters</p>
</td>
</tr>
<tr>
<td style="border: solid windowtext 1.0pt; border-top: none; background: #E2EFD9; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="CVXAPIParameterName"><b><i><span style="font-family: 'Courier New';">IContext</span></i></b></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; background: #E2EFD9; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal">Context</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;">No</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="line-height: 106%;">An additional context parameter of type android.content.Content. It is usually retrieved from the system's getApplicationContext() method.</p>
</td>
</tr>
</tbody>
</table>
<h2>Return Values</h2>
<ul>
	<li><span style="font-family: courier new,courier,monospace;">NETWORK_ERROR</span> - in case there was a problem to communicate with the back-end</li>
</ul>
<h2>Example</h2>
<pre class="computer_code" style="margin-bottom: 20px; unicode-bidi: embed;">MPinSDK sdk = new MPinSDK();

HashMap&lt;String, String&gt; config = new HashMap&lt;String, String&gt;();
config.put(MPinSDK.CONFIG_BACKEND, "http://ec2-54-77-232-113.eu-west-1.compute.amazonaws.com");

Status status = sdk.Init(config, context);

if (status.getStatusCode() != Status.Code.OK) {
    // handle error
}</pre>
<div class="WordSection1">
<h1><span style="font-size: 42px;"><span class="CVXCodeinTitle"><b><span style="font-family: 'Courier New';">SetBackend</span></b></span></span></h1>
<h2>Description</h2>
<p class="MsoNormal">The <span class="CVXCodeinText"><b><span style="font-family: 'Courier New';">SetBackend</span></b></span> method modifies the currently configured back-end service. The back-end is initially set at SDK initialization (i.e. through the <span class="CVXCodeinText"><span style="font-family: 'Courier New';">Mpin</span></span> method), but it can be changed at any time using <span class="CVXCodeinText"><span style="font-family: 'Courier New';">SetBackend</span></span>.</p>

<h2>Definition</h2>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt; background: #E2EFD9; margin-left: 0in; margin-right: 0in;">
<p class="CVXAPIDefinition" style="line-height: 105%; font-family: 'Courier New';"><b>Status SetBackend(</b>String<b><i> server</i>) </b></p>
<p class="CVXAPIDefinition" style="line-height: 105%; font-family: 'Courier New';"><b>Status SetBackend(</b>String<b><i> server</i>, </b>String<b><i> rpsPrefix</i>) </b></p>

</div>
<h2>Parameters</h2>
<table class="MsoNormalTable" style="margin-left: -.4pt; border-collapse: collapse;" border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td style="border: solid windowtext 1.0pt; background: #F4F4F4; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;"><b><span style="color: #7f7f7f;">Parameter Name</span></b></p>
</td>
<td style="border: solid windowtext 1.0pt; border-left: none; background: #F4F4F4; padding: 0in 5.75pt 0in 5.75pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;"><b><span style="color: #7f7f7f;">Parameter Type</span></b></p>
</td>
<td style="border: solid windowtext 1.0pt; border-left: none; background: #F4F4F4; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;"><b><span style="color: #7f7f7f;">Required?</span></b></p>
</td>
<td style="border: solid windowtext 1.0pt; border-left: none; background: #F4F4F4; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;"><b><span style="color: #7f7f7f;">Description</span></b></p>
</td>
</tr>
<tr>
<td style="border: solid windowtext 1.0pt; border-top: none; background: #E2EFD9; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="CVXAPIParameterName"><b><i><span style="font-family: 'Courier New';">server</span></i></b></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; background: #E2EFD9; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;">String</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;">Yes</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal">The server URL used for the new M-Pin back-end service.</p>
</td>
</tr>
<tr>
<td style="border: solid windowtext 1.0pt; border-top: none; background: #E2EFD9; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="CVXAPIParameterName"><b><i><span style="font-family: 'Courier New';">rpsPrefix</span></i></b></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; background: #E2EFD9; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal">String</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;">No</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="line-height: 106%;">A string representing the prefix for the requests to the RPS. Required only if the default prefix has been changed. If not provided, the value defaults to <span class="CVXCodeinText"><span style="font-family: 'Courier New';">rps</span></span>.</p>
</td>
</tr>
</tbody>
</table>
<h2>Return Values</h2>
<p class="MsoListParagraph" style="margin-left: 0.5in; text-indent: -.25in;"><span style="font-family: Symbol;">·</span><span style="font-size: 7.0pt; line-height: 105%; font-family: 'Times New Roman',serif;">         </span><span class="CVXCodeinText"><span style="font-family: 'Courier New';">OK</span></span> – Back-end service URL configured successfully</p>
<p class="MsoListParagraph" style="margin-left: 0.5in; text-indent: -.25in;"><span style="font-family: Symbol;">·</span><span style="font-size: 7.0pt; line-height: 105%; font-family: 'Times New Roman',serif;">         </span><span class="CVXCodeinText" style="line-height: 19.2px; text-indent: -24px;"><span style="font-family: 'Courier New';">NETWORK_ERROR</span></span> – The specified back-end could not be reached</p>

<h2>Example</h2>
<p class="MsoNormal">The following example sets the back-end service to <span class="CVXCodeinText;" style="font-family: 'Courier New';">http://ec2-54-77-232-113.eu-west-1.compute.amazonaws.com</span>.</p>

<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt;">
<p class="CVXCodeExample" style="border: none; padding: 0in;"><span style="font-size: 11.0pt; line-height: 150%; font-family: 'Courier New';">Status status = sdk.SetBackend(“http://ec2-54-77-232-113.eu-west-1.compute.amazonaws.com”);</span></p>
if (status.getStatusCode() != Status.Code.OK) {

// handle error

}

</div>
</div>
<div class="WordSection1">
<h1><span style="font-size: 42px;"><span class="CVXCodeinTitle"><b><span style="font-family: 'Courier New';">TestBackend</span></b></span></span></h1>
<h2>Description</h2>
<p class="MsoNormal">The <span class="CVXCodeinText"><b><span style="font-family: 'Courier New';">TestBackend</span></b></span> method tests whether the back-end service is operational by sending a request for retrieving the Client Settings to back-end.</p>

<h2>Definition</h2>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt; background: #E2EFD9; margin-left: 0in; margin-right: 0in;">
<p class="CVXAPIDefinition" style="line-height: 105%; font-family: 'Courier New';"><b>Status TestBackend(</b>String<b><i> server</i>) </b></p>
<p class="CVXAPIDefinition" style="line-height: 105%; font-family: 'Courier New';"><b>Status TestBackend(</b>String<b><i> server</i>, </b>String<b><i> rpsPrefix</i>)</b></p>

</div>
<h2>Parameters</h2>
<table class="MsoNormalTable" style="margin-left: -.4pt; border-collapse: collapse;" border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td style="border: solid windowtext 1.0pt; background: #F4F4F4; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;"><b><span style="color: #7f7f7f;">Parameter Name</span></b></p>
</td>
<td style="border: solid windowtext 1.0pt; border-left: none; background: #F4F4F4; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;"><b><span style="color: #7f7f7f;">Parameter Type</span></b></p>
</td>
<td style="border: solid windowtext 1.0pt; border-left: none; background: #F4F4F4; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;"><b><span style="color: #7f7f7f;">Required?</span></b></p>
</td>
<td style="border: solid windowtext 1.0pt; border-left: none; background: #F4F4F4; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;"><b><span style="color: #7f7f7f;">Description</span></b></p>
</td>
</tr>
<tr>
<td style="border: solid windowtext 1.0pt; border-top: none; background: #E2EFD9; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="CVXAPIParameterName"><b><i><span style="font-family: 'Courier New';">server</span></i></b></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; background: #E2EFD9; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;">String</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;">Yes</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal">The URL of the M-Pin back-end service to test.</p>
</td>
</tr>
<tr>
<td style="border: solid windowtext 1.0pt; border-top: none; background: #E2EFD9; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="CVXAPIParameterName"><b><i><span style="font-family: 'Courier New';">rpsPrefix</span></i></b></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; background: #E2EFD9; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal">String</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;">No</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal">A string representing the prefix for the requests to the RPS. Required only if the default prefix has been changed. If not provided, the value defaults to <span class="CVXCodeinText"><span style="font-family: 'Courier New';">rps</span></span>.</p>
</td>
</tr>
</tbody>
</table>
<h2>Return Values</h2>
<p class="MsoListParagraph" style="margin-left: 0.5in; text-indent: -.25in;"><span style="font-family: Symbol;">·</span><span style="font-size: 7.0pt; line-height: 105%; font-family: 'Times New Roman',serif;">         </span><span class="CVXCodeinText"><span style="font-family: 'Courier New';">OK</span></span> – Back-end service URL verifies OK</p>
<p class="MsoListParagraph" style="margin-left: 0.5in; text-indent: -.25in;"><span style="font-family: Symbol;">·</span><span style="font-size: 7.0pt; line-height: 105%; font-family: 'Times New Roman',serif;">         </span><span class="CVXCodeinText" style="line-height: 19.2px; text-indent: -24px;"><span style="font-family: 'Courier New';">NETWORK_ERROR</span></span> – The specified back-end could not be reached</p>

<h2>Example</h2>
<p class="MsoNormal">The code snippet below tests the following URL:<span style="font-family: 'Courier New';"> <span class="CVXCodeinText"><span style="font-family: 'Courier New';">http://ec2-54-77-232-113.eu-west-1.compute.amazonaws.com</span></span></span>.</p>

<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt;">
<p class="CVXCodeExample" style="border: none; padding: 0in;"><span style="font-size: 11.0pt; line-height: 150%; font-family: 'Courier New';">Status status = sdk.TestBackend(“http://ec2-54-77-232-113.eu-west-1.compute.amazonaws.com”);</span></p>
if (status.getStatusCode() != Status.Code.OK) {

// handle error

}

</div>
</div>
<h1><span class="CVXCodeinText;"><b><span style="font-family: 'Courier New';">GetClientParam</span></b> Method</span></h1>
<h2>Description</h2>
This method returns the value for a <em style="box-sizing: border-box;">Client Setting</em> with the given key. The value is returned as a String always, i.e. when a numeric or a boolean value is expected, the conversion should be handled by the application. It uses the following client settings:
<ul>
	<li style="box-sizing: border-box;"><code style="box-sizing: border-box; font-family: Consolas,;">accessNumberDigits</code> - The number of Access Number digits that should be entered by the user, prior to calling <a href="#"><code style="box-sizing: border-box; font-family: Consolas,;">FinishAuthenticationAN</code></a></li>
	<li style="box-sizing: border-box;"><code style="box-sizing: border-box; font-family: Consolas,;">setDeviceName</code> - Indicates (<code style="box-sizing: border-box; font-family: Consolas,;">true/false</code>) whether the application should ask the user to insert a <em style="box-sizing: border-box;">Device Name</em> and pass it to the <a href="#"><code style="box-sizing: border-box; font-family: Consolas,;">MakeNewUser</code></a> method</li>
	<li style="box-sizing: border-box;"><code style="box-sizing: border-box; font-family: Consolas,;">appID</code> - Unique ID assigned to each customer or application, used by the backend. It is a hex-encoded long numeric value and can only be used for information purposes and does not affect the behaviour of the application in any way.</li>
</ul>
<h2>Definition</h2>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt; background: #E2EFD9; margin-left: 0in; margin-right: 0in;">
<p class="CVXAPIDefinition" style="line-height: 105%; font-family: 'Courier New';"><b>String GetClientParam(String key)</b></p>

</div>
<h2>Parameters</h2>
<table class="MsoNormalTable" style="margin-left: 2.75pt; border-collapse: collapse; border: none;" border="1" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td style="width: 101.35pt; border: solid windowtext 1.0pt; background: #F4F4F4; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="135">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;"><b><span style="color: #7f7f7f;">Parameter Name</span></b></p>
</td>
<td style="border: solid windowtext 1.0pt; border-left: none; background: #F4F4F4; padding: 0in 5.75pt 0in 5.75pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;"><b><span style="color: #7f7f7f;">Parameter Type</span></b></p>
</td>
<td style="border: solid windowtext 1.0pt; border-left: none; background: #F4F4F4; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;"><b><span style="color: #7f7f7f;">Required?</span></b></p>
</td>
<td style="border: solid windowtext 1.0pt; border-left: none; background: #F4F4F4; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;"><b><span style="color: #7f7f7f;">Description</span></b></p>
</td>
</tr>
<tr>
<td style="width: 101.35pt; border: solid windowtext 1.0pt; border-top: none; background: #E2EFD9; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="135">
<p class="CVXAPIParameterName" style="margin-bottom: 6.0pt;"><b><i><span style="font-family: 'Courier New';">key</span></i></b></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.75pt 0in 5.75pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">String</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">Yes</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;"><span style="color: #3e454c; font-family: Lato, sans-serif; font-size: 16.8px; background-color: #ffffff;">The name of the requested parameter</span></p>
</td>
</tr>
</tbody>
</table>
<h2>Return Values</h2>
String - the value of the requested client parameter
<h2>Example</h2>
<pre class="computer_code" style="margin-bottom: 20px; unicode-bidi: embed;">String appID = sdk.GetClientParam("appID");</pre>