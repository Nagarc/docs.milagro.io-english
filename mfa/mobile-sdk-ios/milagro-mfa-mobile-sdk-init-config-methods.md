---
currentMenu: milagro-mfa-mobile-sdk-init-config-methods-ios
---

<div id="generated-toc" class="generate_from_h2"></div>


<div class="WordSection1">
<h1>Initialization and Configuration Methods - Milagro MFA Mobile SDK for IOS</h1>
<h2 class="MsoNormal">Overview</h2>
<p class="MsoNormal">This page provides a list, along with brief descriptions, of the Initialization and Configuration methods used in the Milagro MFA Mobile SDK for iOS. They relate to intializing the Milagro MFA Mobile SDK and configuring the back-end URL.</p>
<p class="MsoNormal">To view the other methods, see the <a href="#">API Reference</a> page.</p>
<p class="MsoNormal"></p>

</div>
<h1><span style="font-family: courier new,courier,monospace;"><strong>InitSDK</strong></span></h1>
<h2>Description</h2>
This method constructs/initializes the SDK object.
<div class="info">Note that after this initialization, the SDK will not be ready for usage until <code style="box-sizing: border-box; font-family: Consolas,;">SetBackend</code> is called with a valid <em style="box-sizing: border-box; color: #333333;">Definition</em></div>
<h2>Definition</h2>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt; background: #E2EFD9; margin-left: 0in; margin-right: 0in;">
<p class="CVXAPIDefinition" style="line-height: 125%; font-family: 'Courier New';"><code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: inherit; padding: 0.2em 0px; margin: 0px; border-radius: 3px; background-color: rgba(0, 0, 0, 0.0392157);">+ (void) initSDK;</code></p>

</div>
<h2>Parameters</h2>
None.
<h2>Return Values</h2>
None. This method always succeeeds.
<h2>Example</h2>
<pre class="computer_code" style="margin-bottom: 20px; unicode-bidi: embed;">/*
* Initializing the SDK
*/
[MPin initSDK];
MpinStatus* status = [MPin SetBackend:@"http://my.backend.com"];

if (mpinStatus.status != OK) {
    // Show error message and exit
}</pre>
<div class="WordSection1">
<h1><span style="font-size: 42px;"><span class="CVXCodeinTitle"><b><span style="font-family: 'Courier New';">TestBackend</span></b></span></span></h1>
<h2>Description</h2>
<p class="MsoNormal">This method tests if <code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0.2em 0px; margin: 0px; border-radius: 3px; color: #333333; background-color: rgba(0, 0, 0, 0.0392157);">server</code> is a valid back-end URL by trying to retrieve Client Settings from it. You can specify a custom RPS prefix if it was customized at the back-end and is different from the default <code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0.2em 0px; margin: 0px; border-radius: 3px; color: #333333; background-color: rgba(0, 0, 0, 0.0392157);">"rps"</code>. If the back-end URL is a valid one, the method will return status <code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0.2em 0px; margin: 0px; border-radius: 3px; color: #333333; background-color: rgba(0, 0, 0, 0.0392157);">OK</code>.</p>

<h2>Definition</h2>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt; background: #E2EFD9; margin-left: 0in; margin-right: 0in;">
<p class="CVXAPIDefinition" style="line-height: 125%; font-family: 'Courier New';"><code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: inherit; padding: 0.2em 0px; margin: 0px; border-radius: 3px; background-color: rgba(0, 0, 0, 0.0392157);">+ (MpinStatus*) TestBackend: (const NSString*) url;</code></p>
<p class="CVXAPIDefinition" style="line-height: 125%; font-family: 'Courier New';"><code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: inherit; padding: 0.2em 0px; margin: 0px; border-radius: 3px; background-color: rgba(0, 0, 0, 0.0392157);">+ (MpinStatus*) TestBackend: (const NSString*) url rpsPrefix: (const NSString*) rpsPrefix;</code></p>

</div>
<h2>Parameters</h2>
<table class="MsoNormalTable" style="margin-left: -.4pt; border-collapse: collapse;" border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td style="border: solid windowtext 1.0pt; background: #F4F4F4; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;"><code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: inherit; padding: 0.2em 0px; margin: 0px; border-radius: 3px; background-color: rgba(0, 0, 0, 0.0392157);"><b><span style="color: #7f7f7f;">Parameter Name</span></b></code></p>
</td>
<td style="border: solid windowtext 1.0pt; border-left: none; background: #F4F4F4; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;"><code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: inherit; padding: 0.2em 0px; margin: 0px; border-radius: 3px; background-color: rgba(0, 0, 0, 0.0392157);"><b><span style="color: #7f7f7f;">Parameter Type</span></b></code></p>
</td>
<td style="border: solid windowtext 1.0pt; border-left: none; background: #F4F4F4; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;"><code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: inherit; padding: 0.2em 0px; margin: 0px; border-radius: 3px; background-color: rgba(0, 0, 0, 0.0392157);"><b><span style="color: #7f7f7f;">Required?</span></b></code></p>
</td>
<td style="border: solid windowtext 1.0pt; border-left: none; background: #F4F4F4; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;"><code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: inherit; padding: 0.2em 0px; margin: 0px; border-radius: 3px; background-color: rgba(0, 0, 0, 0.0392157);"><b><span style="color: #7f7f7f;">Description</span></b></code></p>
</td>
</tr>
<tr>
<td style="border: solid windowtext 1.0pt; border-top: none; background: #E2EFD9; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="CVXAPIParameterName"><code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: inherit; padding: 0.2em 0px; margin: 0px; border-radius: 3px; background-color: rgba(0, 0, 0, 0.0392157);"><span style="font-family: 'Courier New';"><b><i>url</i></b></span></code></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; background: #E2EFD9; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;"><code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: inherit; padding: 0.2em 0px; margin: 0px; border-radius: 3px; background-color: rgba(0, 0, 0, 0.0392157);">NSString*</code></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;"><code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: inherit; padding: 0.2em 0px; margin: 0px; border-radius: 3px; background-color: rgba(0, 0, 0, 0.0392157);">Yes </code></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal">The URL of the M-Pin back-end service to test.</p>
</td>
</tr>
<tr>
<td style="border: solid windowtext 1.0pt; border-top: none; background: #E2EFD9; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="CVXAPIParameterName"><code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: inherit; padding: 0.2em 0px; margin: 0px; border-radius: 3px; background-color: rgba(0, 0, 0, 0.0392157);"><span style="font-family: 'Courier New';"><b><i>rpsPrefix</i></b></span></code></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; background: #E2EFD9; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;"><code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: inherit; padding: 0.2em 0px; margin: 0px; border-radius: 3px; background-color: rgba(0, 0, 0, 0.0392157);">NSString*</code></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;"><code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: inherit; padding: 0.2em 0px; margin: 0px; border-radius: 3px; background-color: rgba(0, 0, 0, 0.0392157);">No </code></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal">A string representing the prefix for the requests to the RPS. Required only if the default prefix has been changed. If not provided, the value defaults to <span class="CVXCodeinText" style="color: #3e454c; font-family: Lato, sans-serif; font-size: 16.8px; line-height: 26.88px;"><span style="font-family: 'Courier New';">rps</span></span>.</p>
</td>
</tr>
</tbody>
</table>
<h2>Return Status</h2>
<p class="MsoListParagraph" style="margin-left: 0.5in; text-indent: -.25in;"><span style="font-family: Symbol;">·</span><span style="font-size: 7.0pt; line-height: 105%; font-family: 'Times New Roman',serif;">         </span><span class="CVXCodeinText"><span style="font-family: 'Courier New';">OK - Back-end service URL verifies OK</span></span><span class="CVXCodeinText"><span style="font-family: 'Courier New';"></span></span></p>
<p class="MsoListParagraph" style="margin-left: 0.5in; text-indent: -.25in;"><span style="font-family: Symbol;">·</span><span style="font-size: 7.0pt; line-height: 105%; font-family: 'Times New Roman',serif;">         </span><span class="CVXCodeinText"><span style="font-family: 'Courier New';">NETWORK_ERROR - Back-end service URL verification failed</span></span></p>

<h2>Example</h2>
<p class="MsoNormal"><code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: inherit; padding: 0.2em 0px; margin: 0px; border-radius: 3px;">The code snippet below tests the following URL:<span style="font-family: 'Courier New';"> <span class="CVXCodeinText"><span style="font-family: 'Courier New';">http://ec2-54-77-232-113.eu-west-1.compute.amazonaws.com</span></span></span>.</code></p>

<div>
<pre class="computer_code"><code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: inherit; padding: 0.2em 0px; margin: 0px; border-radius: 3px;">MpinStatus* mpinStatus = [MPin TestBackend:@"http://ec2-54-77-232-113.eu-west-1.compute.amazonaws.com"];</code>

if (mpinStatus.status != OK) {
    // Show error message
}</pre>
</div>
</div>
<h1><span style="font-size: 42px;"><span class="CVXCodeinTitle"><b><span style="font-family: 'Courier New';">SetBackend</span></b></span></span></h1>
<h2>Description</h2>
<p class="MsoNormal">This method changes the currently configured back-end in the SDK. <span style="font-family: courier new,courier,monospace;">url</span> is the new back-end URL that should be used. Optionally, a custom RPS prefix might be specified if it was customized at the back-end and is different from the default <code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0.2em 0px; margin: 0px; border-radius: 3px; color: #333333; background-color: rgba(0, 0, 0, 0.0392157);">"rps"</code>. If successful, the method will return status <code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0.2em 0px; margin: 0px; border-radius: 3px; color: #333333; background-color: rgba(0, 0, 0, 0.0392157);">OK</code>.</p>

<h2>Definition</h2>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt; background: #E2EFD9; margin-left: 0in; margin-right: 0in;">
<p class="CVXAPIDefinition" style="line-height: 125%; font-family: 'Courier New';"><code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: inherit; padding: 0.2em 0px; margin: 0px; border-radius: 3px; background-color: rgba(0, 0, 0, 0.0392157);">+ (MpinStatus*) SetBackend: (const NSString*) url;</code></p>
<p class="CVXAPIDefinition" style="line-height: 125%; font-family: 'Courier New';"><code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: inherit; padding: 0.2em 0px; margin: 0px; border-radius: 3px; background-color: rgba(0, 0, 0, 0.0392157);">+ (MpinStatus*) SetBackend: (const NSString*) url rpsPrefix: (const NSString*) rpsPrefix;</code></p>

</div>
<h2>Parameters</h2>
<table class="MsoNormalTable" style="margin-left: -.4pt; border-collapse: collapse;" border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td style="border: 1pt solid windowtext; width: 141px; background: #f4f4f4;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;"><b><span style="color: #7f7f7f;">Parameter Name</span></b></p>
</td>
<td style="border-style: solid solid solid none; border-top-color: windowtext; border-right-color: windowtext; border-bottom-color: windowtext; border-top-width: 1pt; border-right-width: 1pt; border-bottom-width: 1pt; padding: 0in 5.75pt; width: 86px; background: #f4f4f4;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;"><b><span style="color: #7f7f7f;">Parameter Type</span></b></p>
</td>
<td style="border-style: solid solid solid none; border-top-color: windowtext; border-right-color: windowtext; border-bottom-color: windowtext; border-top-width: 1pt; border-right-width: 1pt; border-bottom-width: 1pt; padding: 0in 5.4pt; width: 72px; background: #f4f4f4;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;"><b><span style="color: #7f7f7f;">Required?</span></b></p>
</td>
<td style="border: solid windowtext 1.0pt; border-left: none; background: #F4F4F4; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;"><b><span style="color: #7f7f7f;">Description</span></b></p>
</td>
</tr>
<tr>
<td style="border-style: none solid solid; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; padding: 0in 5.4pt; width: 141px; background: #e2efd9;" valign="top"><span style="font-family: courier new,courier,monospace;"><strong><em>url</em></strong></span></td>
<td style="border-style: none solid solid none; border-bottom-color: windowtext; border-bottom-width: 1pt; border-right-color: windowtext; border-right-width: 1pt; padding: 0in 5.4pt; width: 87px; background: #e2efd9;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;">NSString*</p>
</td>
<td style="border-style: none solid solid none; border-bottom-color: windowtext; border-bottom-width: 1pt; border-right-color: windowtext; border-right-width: 1pt; padding: 0in 5.4pt; width: 72px;" valign="top">Yes</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">The server URL used for the new M-Pin back-end service.</td>
</tr>
<tr>
<td style="border-style: none solid solid; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; padding: 0in 5.4pt; width: 141px; background: #e2efd9;" valign="top"><strong><span style="font-family: courier new,courier,monospace;"><em>rpsPrefix</em></span></strong></td>
<td style="border-style: none solid solid none; border-bottom-color: windowtext; border-bottom-width: 1pt; border-right-color: windowtext; border-right-width: 1pt; padding: 0in 5.4pt; width: 87px; background: #e2efd9;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;">NSString*</p>
</td>
<td style="border-style: none solid solid none; border-bottom-color: windowtext; border-bottom-width: 1pt; border-right-color: windowtext; border-right-width: 1pt; padding: 0in 5.4pt; width: 72px;" valign="top">No</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">A string representing the prefix for the requests to the RPS. Required only if the default prefix has been changed. If not provided, the value defaults to <span class="CVXCodeinText" style="color: #3e454c; font-family: Lato, sans-serif; font-size: 16.8px; line-height: 17.808px;"><span style="font-family: 'Courier New';">rps</span></span>.</td>
</tr>
</tbody>
</table>
<h2>Return Values</h2>
<p class="MsoListParagraph" style="margin-left: 0.5in; text-indent: -.25in;"><span style="font-family: Symbol;">·</span><span style="font-size: 7.0pt; line-height: 105%; font-family: 'Times New Roman',serif;">         </span><span class="CVXCodeinText"><span style="font-family: 'Courier New';">OK</span></span> – Back-end service URL configured successfully</p>
<p class="MsoListParagraph" style="margin-left: 0.5in; text-indent: -.25in;"><span style="font-family: Symbol;">·</span><span style="font-size: 7.0pt; line-height: 105%; font-family: 'Times New Roman',serif;">         </span><span class="CVXCodeinText"><span style="font-family: 'Courier New';">NETWORK_ERROR</span></span> – Setting back-end service URL failed</p>

<h2>Example</h2>
<p class="MsoNormal">The following example sets the M-Pin back-end service to <span class="CVXCodeinText;" style="font-family: 'Courier New';">http://ec2-54-77-232-113.eu-west-1.compute.amazonaws.com</span>.</p>

<div>
<pre class="computer_code"><code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: inherit; padding: 0.2em 0px; margin: 0px; border-radius: 3px;">MpinStatus* mpinStatus = [MPin SetBackend:@"http://ec2-54-77-232-113.eu-west-1.compute.amazonaws.com"];</code>

if (mpinStatus.status != OK) {
    // Show error message
}</pre>
</div>
<h1><span class="CVXCodeinText;"><b><span style="font-family: 'Courier New';">GetClientParam</span></b> Method</span></h1>
<h2>Description</h2>
This method returns the value for a <em style="box-sizing: border-box;">Client Setting</em> with the given key. The value is returned as a String always, i.e. when a numeric or a boolean value is expected, the conversion should be handled by the application. It uses the following client settings:
<ul>
	<li style="box-sizing: border-box;"><code style="box-sizing: border-box; font-family: Consolas,;">accessNumberDigits</code> - The number of Access Number digits that should be entered by the user, prior to calling <code style="box-sizing: border-box; font-family: Consolas,;">FinishAuthenticationAN</code></li>
	<li style="box-sizing: border-box;"><code style="box-sizing: border-box; font-family: Consolas,;">setDeviceName</code> - Indicates (<code style="box-sizing: border-box; font-family: Consolas,;">true/false</code>) whether the application should ask the user to insert a <em style="box-sizing: border-box;">Device Name</em> and pass it to the <code style="box-sizing: border-box; font-family: Consolas,;">MakeNewUser</code> method</li>
	<li style="box-sizing: border-box;"><code style="box-sizing: border-box; font-family: Consolas,;">appID</code> - Unique ID assigned to each customer or application, used by the backend. It is a hex-encoded long numeric value and can only be used for information purposes and does not affect the behaviour of the application in any way</li>
</ul>
<h2>Definition</h2>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt; background: #E2EFD9; margin-left: 0in; margin-right: 0in;">
<p class="CVXAPIDefinition" style="line-height: 105%; font-family: 'Courier New';"><b>+ (NSString*) GetClientParam: (const NSString*) key;</b></p>

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
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">NSString*</p>
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
NSString - the value of the requested client parameter
<h2>Example</h2>
<pre class="computer_code">NSString* appID = [MPin GetClientParam:@"appID"];

if ( appID == nil ) {
    //Handle error
}</pre>