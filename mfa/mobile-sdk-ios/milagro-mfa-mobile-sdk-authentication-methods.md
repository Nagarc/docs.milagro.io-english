---
currentMenu: milagro-mfa-mobile-sdk-user-authentications-methods-ios
---

<div class="WordSection1">
<h1>Authentication Methods Reference</h1>
<h2>Overview</h2>
<p class="MsoNormal">This page provides a list of the Authentication methods used, along with brief descriptions, in the Milagro MFA Mobile SDK for iOS. They relate to performing User Authentication.</p>
<p class="MsoNormal">To view the other methods, refer to the <a href="#">API Reference</a> page.</p>

</div>
<h1>StartAuthentication Method</h1>
<h2>Description</h2>
This method starts the authentication process for a given user. It attempts to retrieve the Time Permits for the user. If successful, it returns status code <span style="font-family: courier new,courier,monospace;">OK</span>, and if not, it returns status code <span style="font-family: courier new,courier,monospace;">REVOKED</span>. If the <i>Time Permits</i> are retrieved, the app reads the PIN/secret from the end-user and calls one of the <code style="box-sizing: border-box;">FinishAuthentication</code> variants to authenticate the user.
<h2>Definition</h2>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt; background: #E2EFD9; margin-left: 0in; margin-right: 0in;">
<p class="CVXAPIDefinition" style="line-height: 125%; font-family: 'Courier New';"><span style="font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: inherit; color: #333333; line-height: 1.4; background-color: rgba(0, 0, 0, 0.0392157);">+ (MpinStatus*) StartAuthentication: (const id&lt;IUser&gt;) user;</span></p>

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
<p class="CVXAPIParameterName" style="margin-bottom: 6.0pt;"><b><i><span style="font-family: 'Courier New';">user</span></i></b></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.75pt 0in 5.75pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">IUser</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">Yes</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">The User ID</p>
</td>
</tr>
</tbody>
</table>
<h2>Return Status</h2>
<ul>
	<li><span style="font-family: courier new,courier,monospace;">OK </span>- The authentication process has been started successfully</li>
	<li><span style="font-family: courier new,courier,monospace;">REVOKED </span>- Time permit for the given user was refused by the server.</li>
	<li><span style="font-family: courier new,courier,monospace;">FLOW_ERROR </span>The user is in the incorrect state, i.e. its state is not <span style="font-family: courier new,courier,monospace;">REGISTERED</span><span style="font-family: courier new,courier,monospace;"> </span></li>
</ul>
<h2>Example</h2>
<pre class="computer_code" style="margin-bottom: 20px; unicode-bidi: embed;">MpinStatus* mpinStatus = [MPin StartAuthentication:iuser];

switch (mpinStatus.status) {
    case OK:
        break;
    case REVOKED:
        // User is revoked, canot authenticate
        break;
    default:
        // Show error message and exit
        break;
}

NSString* authPin;
//
// Read PIN Code or secret from the user
//

mpinStatus = [MPin FinishAuthentication:iuser pin:authPin];

switch (mpinStatus.status) {
    case OK:
        // Authentication successful
        break;
    case INCORRECT_PIN:
        // Authentication failed
        if ([iuser getState] == BLOCKED) {
            // User is blocked and cannot authenticate anymore
        }
        break;
    default:
        // Show error message and exit
        break;
}</pre>
<h1><span style="font-family: 'Courier New';"><span style="font-size: 42px;">CheckAccessNumber</span></span></h1>
<h2>Description</h2>
This method is used only when a user needs to be authenticated to a remote (browser) session, using <em style="color: #3e454c; font-family: Lato, sans-serif; font-size: 16.8px; line-height: 26.88px; background-color: #ffffff;">Access Number</em>. The access numbers have a check-sum digit in them which needs to be verified on the client side, in order to prevent calling the back-end with non-compliant access numbers. The method returns status <code style="color: #3e454c; font-size: 16.8px; line-height: 26.88px; box-sizing: border-box; background-color: #ffffff;">OK</code> if successful, and <code style="color: #3e454c; font-size: 16.8px; line-height: 26.88px; box-sizing: border-box; background-color: #ffffff;">INCORRECT_ACCESS_NUMBER</code> if not.
<h2>Definition</h2>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt; background: #E2EFD9; margin-left: 0in; margin-right: 0in;">
<p class="CVXAPIDefinition"><b><span style="line-height: 105%; font-family: 'Courier New';">+ (MpinStatus*) CheckAccessNumber: (NSString*) an;</span></b></p>

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
<p class="CVXAPIParameterName" style="margin-bottom: 6.0pt;"><b><i><span style="font-family: 'Courier New';">an</span></i></b></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.75pt 0in 5.75pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">NSString*</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">Yes</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">Access Number used to authenticate the user</p>
</td>
</tr>
</tbody>
</table>
<h2>Return Values</h2>
<ul>
	<li>OK (if successful)</li>
	<li>INCORRECT_ACCESS_NUMBER (if not)</li>
</ul>
<h2>Examples</h2>
<pre class="computer_code">MpinStatus* mpinStatus = [MPin StartAuthentication:iuser];

switch (mpinStatus.status) {
    case OK:
        break;
    case REVOKED:
        // User is revoked, canot authenticate
        break;
    default:
        // Show error message and exit
        break;
}

NSString* accessNumber;
//
// Read Access Number from the user
//

mpinStatus = [MPin CheckAccessNumber:accessNumber];

if ( mpinStatus.status != OK ) {
    // Access Number is not correct
}

NSString* authPin;
//
// Read PIN Code or secret from the user
//

mpinStatus = [MPin FinishAuthenticationAN:iuser pin:authPin accessNumber:accessNumber];

switch (mpinStatus.status) {
    case OK:
        // Authentication successful
        break;
    case INCORRECT_ACCESS_NUMBER :
        // Access Number not accepted by server
        break;
    case INCORRECT_PIN:
        // Authentication failed
        if ([iuser getState] == BLOCKED) {
            // User is blocked and cannot authenticate anymore
        }
        break;
    default:
        // Show error message and exit
        break;
}</pre>
<h1><span style="font-size: 36px;"><span style="font-family: 'Courier New';">FinishAuthentication</span></span></h1>
<h2>Description</h2>
This method performs end-user authentication. The <span style="font-size: 14px;"><em style="font-weight: normal; font-size: 14px; line-height: 19.2px;">user</em></span> to be authenticated and the pin (secret) are passed as parameters. The method uses the provided <em>pin</em> and the stored <em>M-Pin Token</em> to do the authentication against the <em style="font-weight: normal; font-size: 14px; line-height: 19.2px;">M-Pin Authentication Server</em> and then logs into the RPA. The RPA passes back <span style="font-size: 14px;"><em style="font-weight: normal; font-size: 14px; line-height: 19.2px;">User Data</em></span> with the authentication response, which is returned to the application through the <code style="color: #3e454c; font-size: 16.8px; line-height: 26.88px; box-sizing: border-box;">authResultData</code> parameter. If authenticated, the returned status is <code style="color: #3e454c; font-size: 16.8px; line-height: 26.88px; box-sizing: border-box;">OK<span style="font-size: 12px;"><span style="font-family: arial,helvetica,sans-serif;"> <span style="font-size: 14px;"><span style="font-family: tahoma,geneva,sans-serif;"><span dir="ltr">and if not, </span></span></span></span></span></code><span style="font-size: 12px;"><span style="font-family: arial,helvetica,sans-serif;"><code style="color: #3e454c; font-size: 16.8px; line-height: 26.88px; box-sizing: border-box; padding: 0.2em 0px; margin: 0px; border-radius: 3px;"><span style="font-size: 14px;"><span style="font-family: tahoma,geneva,sans-serif;"><span dir="ltr">it would be </span></span></span></code></span></span><code style="color: #3e454c; font-size: 16.8px; line-height: 26.88px; box-sizing: border-box;">INCORRECT_PIN</code>. After the third (configurable in the RPS) unsuccessful authentication attempt, the method returns status <code style="color: #3e454c; font-size: 16.8px; line-height: 26.88px; box-sizing: border-box;">INCORRECT_PIN</code> and the User State is set to <code style="color: #3e454c; font-size: 16.8px; line-height: 26.88px; box-sizing: border-box;">BLOCKED</code>.
<h2>Definition</h2>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt; background: #E2EFD9; margin-left: 0in; margin-right: 0in;">
<p class="CVXAPIDefinition"><b><span style="line-height: 105%; font-family: 'Courier New';">+ (MpinStatus*) FinishAuthentication: (const id&lt;IUser&gt;) user pin: (NSString*) pin;</span></b></p>
<p class="CVXAPIDefinition"><b><span style="line-height: 105%; font-family: 'Courier New';">+ (MpinStatus*) FinishAuthentication: (const id&lt;IUser&gt;) user pin: (NSString*) pin authResultData: (NSString**) authResultData;</span></b></p>

</div>
<h2>Parameters</h2>
<table class="MsoNormalTable" style="margin-left: 2.75pt; border-collapse: collapse; border: none;" border="1" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td style="width: 188px; border: 1pt solid windowtext; padding: 0in 5.4pt; background: #f4f4f4;" valign="top" width="135">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;"><b><span style="color: #7f7f7f;">Parameter Name</span></b></p>
</td>
<td style="border-style: solid solid solid none; border-top-color: windowtext; border-right-color: windowtext; border-bottom-color: windowtext; border-top-width: 1pt; border-right-width: 1pt; border-bottom-width: 1pt; padding: 0in 5.75pt; width: 120px; background: #f4f4f4;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;"><b><span style="color: #7f7f7f;">Parameter Type</span></b></p>
</td>
<td style="border-style: solid solid solid none; border-top-color: windowtext; border-right-color: windowtext; border-bottom-color: windowtext; border-top-width: 1pt; border-right-width: 1pt; border-bottom-width: 1pt; padding: 0in 5.4pt; width: 15px; background: #f4f4f4;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;"><b><span style="color: #7f7f7f;">Required?</span></b></p>
</td>
<td style="border: solid windowtext 1.0pt; border-left: none; background: #F4F4F4; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;"><b><span style="color: #7f7f7f;">Description</span></b></p>
</td>
</tr>
<tr>
<td style="width: 188px; border-style: none solid solid; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; padding: 0in 5.4pt; background: #e2efd9;" valign="top" width="135">
<p class="CVXAPIParameterName" style="margin-bottom: 6.0pt;"><b><i><span style="font-family: 'Courier New';">user</span></i></b></p>
</td>
<td style="border-style: none solid solid none; border-bottom-color: windowtext; border-bottom-width: 1pt; border-right-color: windowtext; border-right-width: 1pt; padding: 0in 5.75pt; width: 120px;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">IUser</p>
</td>
<td style="border-style: none solid solid none; border-bottom-color: windowtext; border-bottom-width: 1pt; border-right-color: windowtext; border-right-width: 1pt; padding: 0in 5.4pt; width: 15px;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">Yes</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">The User ID</p>
</td>
</tr>
<tr>
<td style="width: 188px; border-style: none solid solid; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; padding: 0in 5.4pt; background: #e2efd9;" valign="top" width="135">
<p class="CVXAPIParameterName" style="margin-bottom: 6.0pt;"><b><i><span style="font-family: 'Courier New';">pin</span></i></b></p>
</td>
<td style="border-style: none solid solid none; border-bottom-color: windowtext; border-bottom-width: 1pt; border-right-color: windowtext; border-right-width: 1pt; padding: 0in 5.75pt; width: 120px;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">NSString*</p>
</td>
<td style="border-style: none solid solid none; border-bottom-color: windowtext; border-bottom-width: 1pt; border-right-color: windowtext; border-right-width: 1pt; padding: 0in 5.4pt; width: 15px;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">Yes</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">The PIN/secret entered by the end-user</p>
</td>
</tr>
<tr>
<td style="width: 188px; border-style: none solid solid; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; padding: 0in 5.4pt; background: #e2efd9;" valign="top" width="135">
<p class="CVXAPIParameterName" style="margin-bottom: 6.0pt;"><b><i><span style="font-family: 'Courier New';">authResultData</span></i></b></p>
</td>
<td style="border-style: none solid solid none; border-bottom-color: windowtext; border-bottom-width: 1pt; border-right-color: windowtext; border-right-width: 1pt; padding: 0in 5.75pt; width: 120px;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">NSString**</p>
</td>
<td style="border-style: none solid solid none; border-bottom-color: windowtext; border-bottom-width: 1pt; border-right-color: windowtext; border-right-width: 1pt; padding: 0in 5.4pt; width: 15px;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">No</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">Optionally, the result of the authentication would be passed back in that parameter</p>
</td>
</tr>
</tbody>
</table>
<h2>Return Status</h2>
<ul>
	<li><span style="font-family: 'courier new', courier, monospace;">OK<span style="font-family: arial, helvetica, sans-serif;"> - Authentication successfull</span></span></li>
	<li><span style="font-family: 'courier new', courier, monospace;">INCORRECT_PIN<span style="font-family: arial, helvetica, sans-serif;"> - Authentication failed.</span></span></li>
	<li><span style="font-family: 'courier new', courier, monospace;">FLOW_ERROR<span style="font-family: arial, helvetica, sans-serif;"> - The user is in the incorrect state.</span></span></li>
</ul>
<h2>Example</h2>
<pre class="computer_code" style="margin-bottom: 20px; unicode-bidi: embed;">MpinStatus* mpinStatus = [MPin StartAuthentication:iuser];

switch (mpinStatus.status) {
    case OK:
        break;
    case REVOKED:
        // User is revoked, canot authenticate
        break;
    default:
        // Show error message and exit
        break;
}

NSString* authPin;
//
// Read PIN Code or secret from the user
//

mpinStatus = [MPin FinishAuthentication:iuser pin:authPin];

switch (mpinStatus.status) {
    case OK:
        // Authentication successful
        break;
    case INCORRECT_PIN:
        // Authentication failed
        if ([iuser getState] == BLOCKED) {
            // User is blocked and cannot authenticate anymore
        }
        break;
    default:
        // Show error message and exit
        break;
}</pre>
<h1><span style="font-size: 34px;"><span style="font-family: 'Courier New';">FinishAuthenticationOTP</span></span></h1>
<h2>Description</h2>
<p style="color: #2789b1; text-decoration: none;">This method performs end-user authentication for an OTP. It is similar to the <a style="color: #7ecefd; text-decoration: none; transition-duration: 0.3s; font-family: Lato, sans-serif; font-size: 16.8px; line-height: 26.88px; background-color: #ffffff;" href="#">FinishAuthentication</a> method but the RPA issues an OTP instead of logging the user into the application. The returned status is also similar to the <a style="color: #7ecefd; text-decoration: none; transition-duration: 0.3s; font-family: Lato, sans-serif; font-size: 16.8px; line-height: 26.88px; background-color: #ffffff;" href="#">FinishAuthentication</a> method except that an OTP structure is also returned. The OTP structure is as follows:</p>

<pre style="box-sizing: border-box; overflow: auto; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; margin-top: 0px; margin-bottom: 0px; font-stretch: normal; line-height: 1.45; padding: 16px; border-radius: 3px; word-wrap: normal; word-break: normal; color: #333333; background-color: #f7f7f7;"><span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">@interface</span> <span class="pl-en" style="box-sizing: border-box; color: #795da3;">OTP</span>: <span class="pl-e" style="box-sizing: border-box; color: #795da3;">NSObject</span>

<span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">@property</span> (<span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">nonatomic</span>, <span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">retain</span>, <span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">readonly</span>) MpinStatus* status;
<span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">@property</span> (<span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">nonatomic</span>, <span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">retain</span>, <span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">readonly</span>) <span class="pl-c1" style="box-sizing: border-box; color: #0086b3;">NSString</span>* otp;
<span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">@property</span> (<span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">atomic</span>, <span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">readonly</span>) <span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">long</span> expireTime;
<span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">@property</span> (<span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">atomic</span>, <span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">readonly</span>) <span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">int</span> ttlSeconds;
<span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">@property</span> (<span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">atomic</span>, <span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">readonly</span>) <span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">long</span> nowTime;

-(<span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">id</span>) <span class="pl-en" style="box-sizing: border-box; color: #795da3;">initWith</span><span class="pl-en" style="box-sizing: border-box; color: #795da3;">:</span> (MpinStatus*)<span class="pl-smi" style="box-sizing: border-box;">status</span> <span class="pl-en" style="box-sizing: border-box; color: #795da3;">otp</span><span class="pl-en" style="box-sizing: border-box; color: #795da3;">:</span> (<span class="pl-c1" style="box-sizing: border-box; color: #0086b3;">NSString</span>*)<span class="pl-smi" style="box-sizing: border-box;">otp</span> <span class="pl-en" style="box-sizing: border-box; color: #795da3;">expireTime</span><span class="pl-en" style="box-sizing: border-box; color: #795da3;">:</span> (<span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">long</span>)<span class="pl-smi" style="box-sizing: border-box;">expTime</span> <span class="pl-en" style="box-sizing: border-box; color: #795da3;">ttlSeconds</span><span class="pl-en" style="box-sizing: border-box; color: #795da3;">:</span> (<span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">int</span>)<span class="pl-smi" style="box-sizing: border-box;">ttlSeconds</span> <span class="pl-en" style="box-sizing: border-box; color: #795da3;">nowTime</span><span class="pl-en" style="box-sizing: border-box; color: #795da3;">:</span> (<span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">long</span>)<span class="pl-smi" style="box-sizing: border-box;">nowTime</span>;

<span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">@end</span>
</pre>
<table style="border-collapse: collapse; border-spacing: 0px; color: #000000; font-family: Verdana, Arial, Helvetica, sans-serif; font-size: 12px; width: 1061px;" border="1" cellspacing="1" cellpadding="1">
<tbody>
<tr>
<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px solid #cccccc; vertical-align: top; color: #585858; width: 192px;"><strong style="font-style: inherit;">Terms used</strong></td>
<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px solid #cccccc; vertical-align: top; color: #585858; width: 840px;"><strong style="font-style: inherit;">Description</strong></td>
</tr>
<tr>
<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px solid #cccccc; vertical-align: top; color: #585858; width: 192px;">otp</td>
<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px solid #cccccc; vertical-align: top; color: #585858; width: 840px;">The otp string is the issued OTP</td>
</tr>
<tr>
<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px solid #cccccc; vertical-align: top; color: #585858; width: 192px;">expireTime</td>
<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px solid #cccccc; vertical-align: top; color: #585858; width: 840px;">The M-Pin system time when the OTP expires</td>
</tr>
<tr>
<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px solid #cccccc; vertical-align: top; color: #585858; width: 192px;">ttlSeconds</td>
<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px solid #cccccc; vertical-align: top; color: #585858; width: 840px;">The expiration period in seconds</td>
</tr>
<tr>
<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px solid #cccccc; vertical-align: top; color: #585858; width: 192px;">nowTime</td>
<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px solid #cccccc; vertical-align: top; color: #585858; width: 840px;">The current M-Pin system time</td>
</tr>
<tr>
<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px solid #cccccc; vertical-align: top; color: #585858; width: 192px;">status</td>
<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px solid #cccccc; vertical-align: top; color: #585858; width: 840px;"><span style="color: #585858;">The status of the OTP generation. If </span><span style="color: #585858;">OK - OTP is successfully generated, if FLOW_ERROR - OTP was not generated, probably because the RPA doesn't support that functionality.</span></td>
</tr>
</tbody>
</table>
<div class="info">Note that OTP is generated only by RPA that supports that functionality, such as M-Pin SSO. For RPA's that do not support OTP generation the <em style="font-family: Verdana, Arial, Helvetica, sans-serif; font-size: 12px; line-height: 19.2px;">status</em> within the returned <em style="font-family: Verdana, Arial, Helvetica, sans-serif; font-size: 12px; line-height: 19.2px;">otp</em> structure would be <code style="font-size: 12px; line-height: 19.2px;">Status FLOW_ERROR.</code></div>
<h2>Definition</h2>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt; background: #E2EFD9; margin-left: 0in; margin-right: 0in;">
<p class="CVXAPIDefinition"><b><span style="line-height: 105%; font-family: 'Courier New';">+ (MpinStatus*) FinishAuthenticationOTP: (id&lt;IUser&gt;) user pin: (NSString*) pin otp: (OTP**) otp;</span></b></p>

</div>
<h2>Parameters</h2>
<table class="MsoNormalTable" style="margin-left: -.4pt; border-collapse: collapse;" border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td style="border: solid windowtext 1.0pt; background: #F4F4F4; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;"><b><span style="color: #7f7f7f;">Parameter Name</span></b></p>
</td>
<td style="border: solid windowtext 1.0pt; border-left: none; background: #F4F4F4; padding: 0in 2.9pt 0in 2.9pt;" valign="top">
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
<td style="border: solid windowtext 1.0pt; border-top: none; background: #E2EFD9; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="CVXAPIParameterName" style="margin-bottom: 6.0pt;"><b><i><span style="font-family: 'Courier New';">user</span></i></b></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 2.9pt 0in 2.9pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">IUser</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">Yes</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">The user that is being authenticated</p>
</td>
</tr>
<tr>
<td style="border: solid windowtext 1.0pt; border-top: none; background: #E2EFD9; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="CVXAPIParameterName" style="margin-bottom: 6.0pt;"><b><i><span style="font-family: 'Courier New';">pin</span></i></b></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 2.9pt 0in 2.9pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">NSString*</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">Yes</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">The PIN/secret that the user has entered</p>
</td>
</tr>
<tr>
<td style="border: solid windowtext 1.0pt; border-top: none; background: #E2EFD9; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="CVXAPIParameterName" style="margin-bottom: 6.0pt;"><b><i><span style="font-family: 'Courier New';">otp</span></i></b></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 2.9pt 0in 2.9pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">OTP**</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">Yes</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">The resulting OTP is returned here.</p>
</td>
</tr>
</tbody>
</table>
<h2>Return Values</h2>
<ul>
	<li><span style="font-family: 'courier new', courier, monospace;">OK<span style="font-family: arial, helvetica, sans-serif;"> - Authentication successfull</span></span></li>
	<li><span style="font-family: 'courier new', courier, monospace;">INCORRECT_PIN<span style="font-family: arial, helvetica, sans-serif;"> - Authentication failed.</span></span></li>
	<li><span style="font-family: 'courier new', courier, monospace;">FLOW_ERROR<span style="font-family: arial, helvetica, sans-serif;"> - The user is in the incorrect state.</span></span></li>
</ul>
<h2>Examples</h2>
<pre class="computer_code">MpinStatus* mpinStatus = [MPin StartAuthentication:iuser];

switch (mpinStatus.status) {
    case OK:
        break;
    case REVOKED:
        // User is revoked, canot authenticate
        break;
    default:
        // Show error message and exit
        break;
}

NSString* authPin;
//
// Read PIN Code or secret from the user
//

OTP *otp = nil;
mpinStatus = [MPin FinishAuthenticationOTP:iuser pin:authPin otp:&amp;otp];

switch (mpinStatus.status) {
    case OK:
        // Authentication successful
        if ( otp == nil || otp.status.status != OK ) {
            // Provided OTP is not valid - backend doesn't support OTP, exit
        }
        // Display otp.otp to the user
        // otp.ttlSeconds holds the OTP expiration time in seconds
        break;
    case INCORRECT_PIN:
        // Authentication failed
        if ([iuser getState] == BLOCKED) {
            // User is blocked and cannot authenticate anymore
        }
        break;
    default:
        // Show error message and exit
        break;
}</pre>
<h1 style="margin: 0px 0px 15px; padding: 0px; font-stretch: normal; font-family: Arial, sans-serif;"><span style="font-size: 34px;"><span style="font-family: 'Courier New';">FinishAuthenticationAN</span></span></h1>
<h2>Description</h2>
This method authenticates a user with an Access Number which is obtained out-of-band, either from a browser session, through reading a QR code orsent via Push Message . The user then logs into the PC/Browser session which was associated with the provided Access Number although the actual authentication is done on the Mobile Device. <br style="color: #3e454c; font-family: Lato, sans-serif; font-size: 16.8px; line-height: 26.88px;" />
<span style="font-size: 12px;"><i style="color: #3e454c; font-family: Lato, sans-serif; font-size: 16.8px; line-height: 26.88px;">accessNumber</i></span> is the Access Number obtained out-of-band.
<h2>Definition</h2>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt; background: #E2EFD9; margin-left: 0in; margin-right: 0in;">
<p class="CVXAPIDefinition"><b><span style="line-height: 105%; font-family: 'Courier New';">+ (MpinStatus*) FinishAuthenticationAN: (id&lt;IUser&gt;) user pin: (NSString*) pin accessNumber: (NSString*) an;</span></b></p>

</div>
<h2>Parameters</h2>
<table class="MsoNormalTable" style="margin-left: -.4pt; border-collapse: collapse;" border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td style="border: solid windowtext 1.0pt; background: #F4F4F4; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;"><b><span style="color: #7f7f7f;">Parameter Name</span></b></p>
</td>
<td style="border: solid windowtext 1.0pt; border-left: none; background: #F4F4F4; padding: 0in 2.9pt 0in 2.9pt;" valign="top">
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
<td style="border: solid windowtext 1.0pt; border-top: none; background: #E2EFD9; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="CVXAPIParameterName" style="margin-bottom: 6.0pt;"><b><i><span style="font-family: 'Courier New';">user</span></i></b></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 2.9pt 0in 2.9pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">IUser</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">Yes</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;"><span style="color: #3e454c; font-family: Lato, sans-serif; font-size: 16.8px;">The user that is being authenticated</span></p>
</td>
</tr>
<tr>
<td style="border: solid windowtext 1.0pt; border-top: none; background: #E2EFD9; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="CVXAPIParameterName" style="margin-bottom: 6.0pt;"><b><i><span style="font-family: 'Courier New';">pin</span></i></b></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 2.9pt 0in 2.9pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">NSString*</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">Yes</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;"><span style="color: #3e454c; font-family: Lato, sans-serif; font-size: 16.8px;">The PIN/secret that the user has entered</span></p>
</td>
</tr>
<tr>
<td style="border: solid windowtext 1.0pt; border-top: none; background: #E2EFD9; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="CVXAPIParameterName" style="margin-bottom: 6.0pt;"><b><i><span style="font-family: 'Courier New';">an</span></i></b></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 2.9pt 0in 2.9pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">NSString*</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">Yes</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">The Access Number obtained out-of-band and required for the authentication.</p>
</td>
</tr>
</tbody>
</table>
<h2>Return Status</h2>
<ul>
	<li><span style="font-family: courier new,courier,monospace;">OK</span> - Successful Authentication</li>
	<li><span style="font-family: courier new,courier,monospace;">INCORRECT_PIN</span> - Authentication failed because of an incorrect PIN code. After the third (configurable in the RPS) unsuccessful authentication attempt, the method still returns status <code style="line-height: 19.2px;">INCORRRECT_PIN</code> but the user state is set to <code style="line-height: 19.2px;">BLOCKED</code>.</li>
	<li><span style="font-family: courier new,courier,monospace;">INCORRECT_ACCESS_NUMBER</span> - The authentication failed because of incorrect <em style="font-weight: normal; line-height: 19.2px;">Access Number.</em></li>
</ul>
<h2>Examples</h2>
<pre class="computer_code">MpinStatus* mpinStatus = [MPin StartAuthentication:iuser];

switch (mpinStatus.status) {
    case OK:
        break;
    case REVOKED:
        // User is revoked, canot authenticate
        break;
    default:
        // Show error message and exit
        break;
}

NSString* accessNumber;
//
// Read Access Number from the user
//

mpinStatus = [MPin CheckAccessNumber:accessNumber];

if ( mpinStatus.status != OK ) {
    // Access Number is not correct
}

NSString* authPin;
//
// Read PIN Code or secret from the user
//

mpinStatus = [MPin FinishAuthenticationAN:iuser pin:authPin accessNumber:accessNumber];

switch (mpinStatus.status) {
    case OK:
        // Authentication successful
        break;
    case INCORRECT_ACCESS_NUMBER :
        // Access Number not accepted by server
        break;
    case INCORRECT_PIN:
        // Authentication failed
        if ([iuser getState] == BLOCKED) {
            // User is blocked and cannot authenticate anymore
        }
        break;
    default:
        // Show error message and exit
        break;
}</pre>
<div class="WordSection1">
<h1><span class="CVXCodeinText"><b><span style="font-family: 'Courier New'; font-size: 42px;">CanLogout</span></b></span> Method</h1>
<h2>Description</h2>
<p class="MsoNormal">This method checks if a user's logout information was provided by the RPA, and the remote (Browser) session can be terminated from a mobile device. It is used after authentiction with an Access Number, through the FinishAuthenticationAN method. It will return <span style="font-family: 'Courier New';">TRUE</span> if the user can be logged-out from the remote session, and <span style="font-family: 'Courier New';">FALSE</span> otherwise.</p>

<h2>Definition</h2>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt; background: #E2EFD9; margin-left: 0in; margin-right: 0in;">
<p class="CVXAPIDefinition"><code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: inherit; padding: 0.2em 0px; margin: 0px; border-radius: 3px; background-color: rgba(0, 0, 0, 0.0392157);">+ (Boolean) CanLogout: (const id&lt;IUser&gt;) user;</code></p>

</div>
<h2>Parameters</h2>
<table class="MsoNormalTable" style="margin-left: -.4pt; border-collapse: collapse;" border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td style="border: solid windowtext 1.0pt; background: #F4F4F4; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;"><b><span style="color: #7f7f7f;">Parameter Name</span></b></p>
</td>
<td style="border: solid windowtext 1.0pt; border-left: none; background: #F4F4F4; padding: 0in 2.9pt 0in 2.9pt;" valign="top">
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
<td style="border: solid windowtext 1.0pt; border-top: none; background: #E2EFD9; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="CVXAPIParameterName" style="margin-bottom: 6.0pt;"><b><i><span style="font-family: 'Courier New';">user</span></i></b></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 2.9pt 0in 2.9pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">IUser</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">Yes</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">The User ID</p>
</td>
</tr>
</tbody>
</table>
<h2>Return Values</h2>
<p class="MsoListParagraphCxSpFirst" style="margin-left: 0.5in; text-indent: -.25in; line-height: 105%;"><span style="font-family: Symbol;">·<span style="font: 7.0pt 'Times New Roman';">         </span></span><span class="CVXCodeinText"><span style="font-family: 'Courier New';">TRUE</span></span> – the User can be logged out from the remote session</p>
<p class="MsoListParagraphCxSpLast" style="margin-left: 0.5in; text-indent: -.25in; line-height: 105%;"><span style="font-family: Symbol;">·<span style="font: 7.0pt 'Times New Roman';">         </span></span><span class="CVXCodeinText"><span style="font-family: 'Courier New';">FALSE</span></span> – the User cannot be logged out from the remote session</p>

<h2>Example</h2>
<p class="MsoNormal">The following code demonstrates the use of the method:</p>

<div style="border: solid windowtext 1.0pt; padding: 1.0pt 1.0pt 1.0pt 1.0pt; margin-left: 4.5pt; margin-right: 4.5pt;">
<pre class="computer_code" style="border: none; padding: 0in;"><span style="font-size: 12px;"><span style="line-height: 150%; font-family: 'Courier New';">MpinStatus* mpinStatus = [MPin Authenticate:iuser];

// To logout
if([Mpin CanLogout:iuser])
{
    [Mpin Logout:iuser];
} </span></span></pre>
</div>
</div>
<div class="WordSection1">
<h1><span class="CVXCodeinText"><b><span style="font-size: 31.5pt; line-height: 106%; font-family: 'Courier New';">Logout</span></b></span> Method</h1>
<h2>Description</h2>
<p class="MsoNormal">This method tries to log the user out of a remote (Browser) session after successfully authenticating them via the <code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 18.6px; padding: 0.2em 0px; margin: 0px; border-radius: 3px; color: #333333;">FinishAuthenticationAN </code>method. Before calling this method, ensure that logout data was provided by the RPA and that the logout operation can be actually performed. The method returns <code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0.2em 0px; margin: 0px; border-radius: 3px; color: #333333; background-color: rgba(0, 0, 0, 0.0392157);">TRUE</code> if the logged-out request to the RPA is successful, and <code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0.2em 0px; margin: 0px; border-radius: 3px; color: #333333; background-color: rgba(0, 0, 0, 0.0392157);">FALSE</code> otherwise.</p>

<h2>Definition</h2>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt; background: #E2EFD9; margin-left: 0in; margin-right: 0in;">
<p class="CVXAPIDefinition"><code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: inherit; padding: 0.2em 0px; margin: 0px; border-radius: 3px; background-color: rgba(0, 0, 0, 0.0392157);">+ (Boolean) Logout: (const id&lt;IUser&gt;) user;</code></p>

</div>
<h2>Parameters</h2>
<table class="MsoNormalTable" style="margin-left: -.4pt; border-collapse: collapse;" border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td style="border: solid windowtext 1.0pt; background: #F4F4F4; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;"><b><span style="color: #7f7f7f;">Parameter Name</span></b></p>
</td>
<td style="border: solid windowtext 1.0pt; border-left: none; background: #F4F4F4; padding: 0in 2.9pt 0in 2.9pt;" valign="top">
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
<td style="border: solid windowtext 1.0pt; border-top: none; background: #E2EFD9; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="CVXAPIParameterName" style="margin-bottom: 6.0pt;"><b><i><span style="font-family: 'Courier New';">user</span></i></b></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 2.9pt 0in 2.9pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">IUser</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">Yes</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">The User ID</p>
</td>
</tr>
</tbody>
</table>
<h2>Return Values</h2>
<p class="MsoListParagraphCxSpFirst" style="margin-left: 0.5in; text-indent: -.25in; line-height: 105%;"><span style="font-family: Symbol;">·</span><span style="font: 7.0pt 'Times New Roman';">         </span><span class="CVXCodeinText"><span style="font-family: 'Courier New';">TRUE</span></span> – the log-out request to the RPA has been successful</p>
<p class="MsoListParagraphCxSpLast" style="margin-left: 0.5in; text-indent: -.25in; line-height: 105%;"><span style="font-family: Symbol;">·</span><span style="font: 7.0pt 'Times New Roman';">         </span><span class="CVXCodeinText"><span style="font-family: 'Courier New';">FALSE</span></span> – the log-out request to the RPA has failed</p>

<h2>Example</h2>
<p class="MsoNormal">The following code demonstrates the use of the method:</p>

<div style="border: solid windowtext 1.0pt; padding: 1.0pt 1.0pt 1.0pt 1.0pt; margin-left: 4.5pt; margin-right: 4.5pt;">
<pre class="computer_code" style="border: none; padding: 0in;"><span style="font-size: 12px;"><span style="line-height: 150%; font-family: 'Courier New';">MpinStatus* mpinStatus = [MPin Authenticate:iuser];

// To logout
if([Mpin CanLogout:iuser])
{
    [Mpin Logout:iuser];
} </span></span></pre>
</div>
</div>