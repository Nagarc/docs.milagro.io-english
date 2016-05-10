---
currentMenu: milagro-mfa-mobile-sdk-authentication-methods-android
---

<div id="generated-toc" class="generate_from_h2"></div>

<div class="WordSection1">
<h1>Authentication Methods</h1>
<h2>Overview</h2>
<p class="MsoNormal">This page provides a list of the Authentication methods used, along with brief descriptions, in the M-Pin Mobile SDK for iOS. They relate to performing User Authentication.</p>
<p class="MsoNormal">To view the other methods, refer to the <a href="#">API Reference</a> page.</p>

</div>
<h1><span style="font-family: 'Courier New';"><span style="font-size: 40px;">StartAuthentication</span></span> Method</h1>
<h2>Description</h2>
<p class="Normal">This method starts the authentication process for a given <code style="box-sizing: border-box; font-family: Consolas,;">user</code>. It attempts to retrieve the Time Permits for the user. If successful, it returns status code OK, and if not, it returns status code REVOKED. If the <i>Time Permits</i> are retrieved, the app reads the PIN/secret from the end-user and calls one of the <code style="font-style: normal; box-sizing: border-box;">FinishAuthentication</code> variants to authenticate the user.</p>

<h2>Definition</h2>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt; background: #E2EFD9; margin-left: 0in; margin-right: 0in;">
<p class="CVXAPIDefinition" style="line-height: 105%; font-family: 'Courier New';"><b>Status StartAuthentication(User user)</b></p>

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
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">User</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">Yes</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">The user ID</p>
</td>
</tr>
</tbody>
</table>
<h2>Return Status Codes</h2>
<ul>
	<li><span style="font-family: 'courier new', courier, monospace;">OK </span>- The authentication process has been started successfully</li>
	<li><span style="font-family: 'courier new', courier, monospace;">REVOKED </span>- Time permit for the given user was refused by the server.</li>
	<li><span style="font-family: courier new,courier,monospace;">FLOW_ERROR </span>- The user is in the incorrect state, i.e. its state is not <span style="font-family: courier new,courier,monospace;">REGISTERED</span></li>
</ul>
<h2>Example</h2>
<pre class="computer_code">Status status = sdk.StartAuthentication(user);

switch (status.getStatusCode())
{
    case Status.Code.OK:
        break;
    case Status.Code.REVOKED:
        // User is revoked, cannot authenticate
        break;
    default:
        // Show error message and exit
        break;
}

String authPin;
//
// Read PIN Code or secret from the user
//
status = sdk.FinishAuthentication(user, authPin);

switch (status.getStatusCode())
{
    case Status.Code.OK:
        // Authentication successful
        break;
    case Status.Code.INCORRECT_PIN:
        // Authentication failed
        if (user.GetState() == State.BLOCKED)
        {
            // User is blocked and cannot authenticate anymore
        }
        break;
    default:
        // Show error message and exit
        break;
}</pre>
<h1><span style="font-family: 'Courier New';"><span style="font-size: 40px;">CheckAccessNumber</span></span></h1>
<h2>Description</h2>
This method is used only when a user needs to be authenticated to a remote (browser) session, using <em>Access Number</em>. The access numbers have a check-sum digit in them which needs to be verified on the client side, in order to prevent calling the back-end with non-compliant access numbers. The method returns status<code style="font-style: normal; box-sizing: border-box;"> OK</code> if successful, and status <code style="font-style: normal; box-sizing: border-box;">INCORRECT_ACCESS_NUMBER</code> if not.
<h2>Definition</h2>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt; background: #E2EFD9; margin-left: 0in; margin-right: 0in;">
<p class="CVXAPIDefinition"><b><span style="line-height: 105%; font-family: 'Courier New';">Status CheckAccessNumber(String accessNumber)</span></b></p>

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
<p class="CVXAPIParameterName" style="margin-bottom: 6.0pt;"><b><i><span style="font-family: 'Courier New';">accessNumber</span></i></b></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.75pt 0in 5.75pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">String</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">Yes</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">Access Number used for authenticating a user to a remote browser</p>
</td>
</tr>
</tbody>
</table>
<h2>Return Status</h2>
<ul style="margin: 5px 0px 0px 20px; padding: 0px 0px 0px 12px; font-family: Verdana, Arial, Helvetica, sans-serif; font-size: 12px;">
	<li>OK (if successful)</li>
	<li>INCORRECT_ACCESS_NUMBER (if not)</li>
</ul>
<h2>Examples</h2>
<pre class="computer_code">Status status = sdk.StartAuthentication(user);

switch (status.getStatusCode())
{
    case Status.Code.OK:
        break;
    case Status.Code.REVOKED:
        // User is revoked, cannot authenticate
        break;
    default:
        // Show error message and exit
        break;
}

String accessNumber;
//
// Read Access Number from the user
//

status = sdk.CheckAccessNumber(accessNumber);

if (status.getStatusCode() != Status.Code.OK)
{
    // Access Number is not correct
}

String authPin;
//
// Read PIN Code or secret from the user
//
status = sdk.FinishAuthenticationAN(user, authPin, accessNumber);

switch (status.getStatusCode())
{
    case Status.Code.OK:
        // Authentication successful
        break;
    case Status.Code.INCORRECT_ACCESS_NUMBER:
        // Access Number not accepted by server
        break;
    case Status.Code.INCORRECT_PIN:
        // Authentication failed
        if (user.GetState() == State.BLOCKED)
        {
            // User is blocked and cannot authenticate anymore
        }
        break;
    default:
        // Show error message and exit
        break;
}</pre>
<h1><span style="font-size: 34px;"><span style="font-family: 'Courier New';">FinishAuthentication</span> Method</span></h1>
<h2>Description</h2>
This method performs end-user authentication. The <em>user</em> to be authenticated and the pin (secret) are passed as parameters. The method uses the provided pin and the stored <em style="font-weight: normal; line-height: 19.2px;">M-Pin Token</em> to do the authentication against the <em>M-Pin Authentication Server</em> and then logs into the RPA. The RPA passes back <em>User Data</em> with the authentication response, which is returned to the application through the <code style="color: #3e454c; font-size: 16.8px; line-height: 26.88px; box-sizing: border-box;">authResultData</code> parameter. If authenticated, the returned status is <code style="color: #3e454c; font-size: 16.8px; line-height: 26.88px; box-sizing: border-box;">OK</code> and if not, it would be <code style="color: #3e454c; font-size: 16.8px; line-height: 26.88px; box-sizing: border-box;">INCORRECT_PIN.</code>

After the third (configurable in the RPS) unsuccessful authentication attempt, the method returns status <code style="color: #3e454c; font-size: 16.8px; line-height: 26.88px; box-sizing: border-box;">INCORRECT_PIN</code> and the User State is set to <code style="color: #3e454c; font-size: 16.8px; line-height: 26.88px; box-sizing: border-box;">BLOCKED</code>.
<h2>Definition</h2>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt; background: #E2EFD9; margin-left: 0in; margin-right: 0in;">
<p class="CVXAPIDefinition"><b><span style="line-height: 105%; font-family: 'Courier New';">Status FinishAuthentication(User user, String pin)</span></b></p>
<p class="CVXAPIDefinition"><b><span style="line-height: 105%; font-family: 'Courier New';">Status FinishAuthentication(User user, String pin, StringBuilder authResultData)</span></b></p>

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
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">User</p>
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
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">String</p>
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
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">StringBuilder</p>
</td>
<td style="border-style: none solid solid none; border-bottom-color: windowtext; border-bottom-width: 1pt; border-right-color: windowtext; border-right-width: 1pt; padding: 0in 5.4pt; width: 15px;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">No</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">The authentication result data that is returned by the RPA</p>
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
<h2>Example</h2>
<pre class="computer_code">Status status = sdk.StartAuthentication(user);

switch (status.getStatusCode())
{
    case Status.Code.OK:
        break;
    case Status.Code.REVOKED:
        // User is revoked, cannot authenticate
        break;
    default:
        // Show error message and exit
        break;
}

String authPin;
//
// Read PIN Code or secret from the user
//
status = sdk.FinishAuthentication(user, authPin);

switch (status.getStatusCode())
{
    case Status.Code.OK:
        // Authentication successful
        break;
    case Status.Code.INCORRECT_PIN:
        // Authentication failed
        if (user.GetState() == State.BLOCKED)
        {
            // User is blocked and cannot authenticate anymore
        }
        break;
    default:
        // Show error message and exit
        break;
}</pre>
<h1><span style="font-size: 34px;"><span style="font-family: 'Courier New';">FinishAuthenticationOTP</span></span></h1>
<h2>Description</h2>
This method performs end-user authentication for an OTP. It is similar to the FinishAuthentication method but the RPA issues an OTP instead of logging the user into the application. The returned status is also similar to the FinishAuthentication method except that an OTP structure is returned.

The OTP structure is as follows:
<pre style="margin-top: 0px; margin-bottom: 20px; padding: 15px; font-size: 12px; unicode-bidi: embed; border: 1px dotted; color: #333333; box-sizing: border-box; overflow: auto; background-color: #ffffff;"><span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">class</span> <span class="pl-en" style="box-sizing: border-box; color: #795da3;">OTP</span>
{
<span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">public:</span>
    String otp;
    <span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">long</span> expireTime;
    <span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">int</span> ttlSeconds;
    <span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">long</span> nowTime;
    Status status;
};</pre>
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
<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px solid #cccccc; vertical-align: top; color: #585858; width: 840px;">The status of the OTP generation. If <span style="color: #585858;">OK - OTP is successfully generated, if FLOW_ERROR - OTP was not generated, probably because the RPA doesn't support that functionality.</span></td>
</tr>
</tbody>
</table>
<div class="info" style="margin: 0px; padding: 5px 30px; line-height: 1.6em; font-family: Verdana, Arial, Helvetica, sans-serif; font-size: 12px; background: url('/images/info.png') 5px 50% no-repeat #d2eefc;">Note that OTP is generated only by RPA's that support this functionality, such as M-Pin SSO. For RPA's that do not support OTP generation, the <em style="font-weight: inherit; font-size: 12px; line-height: 19.2px;">status</em> within the returned <em style="font-weight: inherit; font-size: 12px; line-height: 19.2px;">otp</em> structure would be <code style="font-size: 12px; line-height: 19.2px;">Status FLOW_ERROR.</code></div>
<h2>Definition</h2>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt; background: #E2EFD9; margin-left: 0in; margin-right: 0in;">
<p class="CVXAPIDefinition"><b><span style="line-height: 105%; font-family: 'Courier New';">Status FinishAuthenticationOTP(User user, String pin, OTP otp)</span></b></p>

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
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">User</p>
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
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">String</p>
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
<p class="CVXAPIParameterName" style="margin-bottom: 6.0pt;"><b><i><span style="font-family: 'Courier New';">otp</span></i></b></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 2.9pt 0in 2.9pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">OTP</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;"><span style="color: #3e454c; font-family: Lato, sans-serif; font-size: 16.8px;">Yes</span></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;"><span style="color: #3e454c; font-family: Lato, sans-serif; font-size: 16.8px;">The resulting OTP is returned here. </span></p>
</td>
</tr>
</tbody>
</table>
<h2>Return Status</h2>
<ul style="font-size: 12px;">
	<li><span style="font-family: 'courier new', courier, monospace;">OK<span style="font-family: arial, helvetica, sans-serif;"> - Authentication successfull</span></span></li>
	<li><span style="font-family: 'courier new', courier, monospace;">INCORRECT_PIN<span style="font-family: arial, helvetica, sans-serif;"> - Authentication failed.</span></span></li>
	<li><span style="font-family: 'courier new', courier, monospace;">FLOW_ERROR<span style="font-family: arial, helvetica, sans-serif;"> - The user is in the incorrect state.</span></span></li>
</ul>
<h2>Examples</h2>
<pre class="computer_code">Status status = sdk.StartAuthentication(user);

switch (status.getStatusCode())
{
    case Status.Code.OK:
        break;
    case Status.Code.REVOKED:
        // User is revoked, cannot authenticate
        break;
    default:
        // Show error message and exit
        break;
}

String authPin;
//
// Read PIN Code or secret from the user
//
OTP otp = new OTP();
status = sdk.FinishAuthenticationOTP(user, authPin, otp);

switch (status.getStatusCode())
{
    case Status.Code.OK:
        // Authentication successful
        if (otp.status == null || otp.status.getStatusCode() != Status.Code.OK)
        {
            // Provided OTP is not valid - backend doesn't support OTP, exit
        }
        // Display otp.otp to the user
        // otp.ttlSeconds holds the OTP expiration time in seconds
        break;
    case Status.Code.INCORRECT_PIN:
        // Authentication failed
        if (user.GetState() == State.BLOCKED)
        {
            // User is blocked and cannot authenticate anymore
        }
        break;
    default:
        // Show error message and exit
        break;
}</pre>
<h1 style="margin: 0px 0px 15px; padding: 0px; font-stretch: normal; font-family: Arial, sans-serif;"><span style="font-size: 34px;"><span style="font-family: 'Courier New';">FinishAuthenticationAN</span></span></h1>
<h2>Description</h2>
This method authenticates a user with an Access Number which is obtained out-of-band, either from a browser session, through reading a QR code orsent via Push Message. The user then logs into the PC/Browser session which was associated with the provided Access Number although the actual authentication is done on the Mobile Device.

<i>accessNumber</i> is the Access Number obtained out-of-band.
<h2>Definition</h2>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt; background: #E2EFD9; margin-left: 0in; margin-right: 0in;">
<p class="CVXAPIDefinition"><b><span style="line-height: 105%; font-family: 'Courier New';">Status FinishAuthenticationAN(User user, String pin, String accessNumber)</span></b></p>

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
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">User</p>
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
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">String</p>
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
<p class="CVXAPIParameterName" style="margin-bottom: 6.0pt;"><span style="font-family: 'Courier New';"><b><i>accessNumber</i></b></span></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 2.9pt 0in 2.9pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">String</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">Yes</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;"><span style="color: #3e454c; font-family: Lato, sans-serif; font-size: 16.8px;">The Access Number obtained out-of-band and required for the authentication.</span></p>
</td>
</tr>
</tbody>
</table>
<h2>Return Status</h2>
<ul>
	<li><span style="font-family: 'courier new', courier, monospace;">OK</span> - Successful Authentication</li>
	<li><span style="font-family: 'courier new', courier, monospace;">INCORRECT_PIN</span> - Authentication failed because of an incorrect PIN code. After the third (configurable in the RPS) unsuccessful authentication attempt, the method still returns status <code style="line-height: 19.2px;">INCORRRECT_PIN</code> but the user state is set to <code style="line-height: 19.2px;">BLOCKED</code>.</li>
	<li><span style="font-family: 'courier new', courier, monospace;">INCORRECT_ACCESS_NUMBER</span> - The authentication failed because of incorrect <em style="font-weight: normal; line-height: 19.2px;">Access Number.</em></li>
</ul>
<h2>Examples</h2>
<pre class="computer_code">Status status = sdk.StartAuthentication(user);

switch (status.getStatusCode())
{
    case Status.Code.OK:
        break;
    case Status.Code.REVOKED:
        // User is revoked, cannot authenticate
        break;
    default:
        // Show error message and exit
        break;
}

String accessNumber;
//
// Read Access Number from the user
//

status = sdk.CheckAccessNumber(accessNumber);

if (status.getStatusCode() != Status.Code.OK)
{
    // Access Number is not correct
}

String authPin;
//
// Read PIN Code or secret from the user
//
status = sdk.FinishAuthenticationAN(user, authPin, accessNumber);

switch (status.getStatusCode())
{
    case Status.Code.OK:
        // Authentication successful
        break;
    case Status.Code.INCORRECT_ACCESS_NUMBER:
        // Access Number not accepted by server
        break;
    case Status.Code.INCORRECT_PIN:
        // Authentication failed
        if (user.GetState() == State.BLOCKED)
        {
            // User is blocked and cannot authenticate anymore
        }
        break;
    default:
        // Show error message and exit
        break;
}</pre>
<div class="WordSection1">
<h1><span class="CVXCodeinText"><b><span style="font-family: 'Courier New'; font-size: 42px;">CanLogout</span></b></span></h1>
<h2>Description</h2>
<p class="MsoNormal">This method is used after authentication with an Access Number through FinishAuthenticationAN. After such an authentication, the Mobile Device can log out the end-user from the Browser session, if the RPA supports that functionality. This method checks whether logout information was provided by the RPA and the remote (Browser) session can be terminated from the Mobile Device. The method will return <code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0.2em 0px; margin: 0px; border-radius: 3px; color: #333333; background-color: rgba(0, 0, 0, 0.0392157);">true</code> if the user can be logged-out from the remote session, and <code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0.2em 0px; margin: 0px; border-radius: 3px; color: #333333; background-color: rgba(0, 0, 0, 0.0392157);">false</code> otherwise.</p>

<h2>Definition</h2>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt; background: #E2EFD9; margin-left: 0in; margin-right: 0in;">
<p class="CVXAPIDefinition"><b><span style="line-height: 105%; font-family: 'Courier New';">boolean CanLogout(</span></b><span style="line-height: 105%; font-family: 'Courier New';">User<b> <i>user)</i></b></span></p>

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
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">User</p>
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
<p class="MsoListParagraphCxSpFirst" style="margin-left: 0.5in; text-indent: -.25in; line-height: 105%;"><span style="font-family: Symbol;">·<span style="font: 7.0pt 'Times New Roman';">       </span></span><span class="CVXCodeinText"><span style="font-family: 'Courier New';">true</span></span> – the User can be logged out from the remote session</p>
<p class="MsoListParagraphCxSpLast" style="margin-left: 0.5in; text-indent: -.25in; line-height: 105%;"><span style="font-family: Symbol;">·<span style="font: 7.0pt 'Times New Roman';">       </span></span><span class="CVXCodeinText"><span style="font-family: 'Courier New';">false</span></span> – the User cannot be logged out from the remote session</p>

<h2>Example</h2>
<p class="MsoNormal">The following code snippet logs out the User from the browser/online session after one minute.</p>

<div class="info">The code assumes the <span class="CVXCodeinText"><span style="font-family: 'Courier New';">accessNumber</span></span> to be an input from the user.</div>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 1.0pt 1.0pt 1.0pt; margin-left: 4.5pt; margin-right: 4.5pt;">
<pre class="computer_code">Status status = sdk.FinishAuthenticationAN(user, pin, accessNumber);

if (status.getStatusCode() != Status.Code.OK) {
    // handle error
}

if (sdk.CanLogout(user)) {
    SystemClock.sleep(60000);   //Waiting for 60 seconds before logging out
    sdk.Logout(user);
}</pre>
</div>
</div>
<div class="WordSection1">
<h1><span class="CVXCodeinText"><b><span style="font-size: 31.5pt; line-height: 106%; font-family: 'Courier New';">Logout</span></b></span></h1>
<h2>Description</h2>
<p class="MsoNormal">This method tries to log out the end-user from a remote (Browser) session after a successful authentication through FinishAuthenticationAN. Before calling this method, it is recommended to ensure that logout data was provided by the RPA and that the logout operation can be actually performed. The method will return <code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0.2em 0px; margin: 0px; border-radius: 3px; color: #333333; background-color: rgba(0, 0, 0, 0.0392157);">TRUE</code> if the logged-out request to the RPA was successful, and <code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0.2em 0px; margin: 0px; border-radius: 3px; color: #333333; background-color: rgba(0, 0, 0, 0.0392157);">FALSE</code> otherwise.</p>

<h2>Definition</h2>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt; background: #E2EFD9; margin-left: 0in; margin-right: 0in;">
<p class="CVXAPIDefinition"><span style="font-family: courier new,courier,monospace;">boolean</span><b><span style="line-height: 105%; font-family: 'Courier New';"> Logout(</span></b><span style="line-height: 105%; font-family: 'Courier New';">User<b> <i>user</i>)</b></span></p>

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
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">User</p>
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
<p class="MsoListParagraphCxSpFirst" style="margin-left: 0.5in; text-indent: -.25in; line-height: 105%;"><span style="font-family: Symbol;">·</span><span style="font: 7.0pt 'Times New Roman';">        </span><span class="CVXCodeinText"><span style="font-family: 'Courier New';">true</span></span> – the log-out request to the RPA has been successful</p>
<p class="MsoListParagraphCxSpLast" style="margin-left: 0.5in; text-indent: -.25in; line-height: 105%;"><span style="font-family: Symbol;">·</span><span style="font: 7.0pt 'Times New Roman';">        </span><span class="CVXCodeinText"><span style="font-family: 'Courier New';">false</span></span> – the log-out request to the RPA has failed</p>

<h2>Example</h2>
<p class="MsoNormal">The following code snippet logs out the User from the browser/online session after one minute.</p>

<div class="info">The code assumes the <span class="CVXCodeinText"><b><span style="font-family: 'Courier New';">accessNumber</span></b></span> to be an input from the user.</div>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 1.0pt 1.0pt 1.0pt; margin-left: 4.5pt; margin-right: 4.5pt;">
<pre class="computer_code">Status status = sdk.FinishAuthenticationAN(user, pin, accessNumber);

if (status.getStatusCode() != Status.Code.OK) {
    // handle error
}

if (sdk.CanLogout(user)) {
    SystemClock.sleep(60000);   //Waiting for 60 seconds before logging out
    sdk.Logout(user);
}</pre>
</div>
</div>