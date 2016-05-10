---
currentMenu: milagro-mfa-mobile-sdk-registration-methods-ios
---

<div id="generated-toc" class="generate_from_h2"></div>


<div class="WordSection1">
<h1>Registration  Methods - Milagro MFA <strong>Mobile SDK for iOS</strong></h1>
<h2>Overview</h2>
<p class="MsoNormal">This page provides a list, along with brief descriptions, of the Registration methods used in the Milagro MFA Mobile SDK for iOS. They describe the procedures involved in registering a new user.</p>
<p class="MsoNormal">To view the other methods, refer to the <a href="#">API Reference</a> page.</p>

</div>
###StartRegistration
<h2>Description</h2>
<p style="margin: 0px 0px 16px; padding: 0px; line-height: 25.6px; color: #333333; font-family: 'Helvetica Neue', Helvetica, 'Segoe UI', Arial, freesans, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol'; font-size: 16px; box-sizing: border-box; background-color: #ffffff;">This method initializes the registration for a User that has already been created. The server starts the registration flow, sending the necessary requests to the back-end service. The State of the User instance will change to <code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0.2em 0px; margin: 0px; border-radius: 3px; background-color: rgba(0, 0, 0, 0.0392157);">STARTED_REGISTRATION</code>. The status will indicate whether the operation was successful or not. During this call, an M-Pin ID for the end-user will be issued by the RPS and stored within the user object. The RPA can also start a user identity verification procedure, by sending a verification e-mail.</p>
<p style="margin: 0px 0px 16px; padding: 0px; line-height: 25.6px; color: #333333; font-family: 'Helvetica Neue', Helvetica, 'Segoe UI', Arial, freesans, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol'; font-size: 16px; box-sizing: border-box; background-color: #ffffff;">The application can also pass additional <code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0.2em 0px; margin: 0px; border-radius: 3px; background-color: rgba(0, 0, 0, 0.0392157);">userData</code> which might help the RPA to verify the user identity. The RPA might decide to verify the identity without starting a verification process. In this case, the returned status from the call will still be <code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0.2em 0px; margin: 0px; border-radius: 3px; background-color: rgba(0, 0, 0, 0.0392157);">OK</code>, but the User State will be set to <code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0.2em 0px; margin: 0px; border-radius: 3px; background-color: rgba(0, 0, 0, 0.0392157);">ACTIVATED</code>.</p>

<h3 style="margin: 30px 0px 20px; padding: 0px; font-size: 1.4em; font-stretch: normal; font-family: Arial, sans-serif; color: #3e454c; background-color: #ffffff;">What Is the Difference Between<span class="CVXCodeinText"><span style="font-family: 'Courier New';"> StartRegistration</span></span> and <span style="font-family: 'Courier New';">RestartRegistration</span>?</h3>
<div class="info">The <span class="CVXCodeinText" style="font-family: Verdana, Arial, Helvetica, sans-serif; font-size: 12px; line-height: 19.2px;"><span style="font-family: 'Courier New';">StartRegistration</span></span> method generates a new M-Pin ID while <a style="text-decoration: none; color: #7ecefd; transition-duration: 0.3s; font-family: Verdana, Arial, Helvetica, sans-serif; font-size: 12px; line-height: 19.2px;" href="http://docs.miracl.com/startregistration-method-m-pin-mobile-sdk-for-ios#"><span class="CVXCodeinText" style="line-height: 19.2px;"><span style="font-family: 'Courier New';">RestartRegistration</span></span></a> uses the ID that has already been generated for the user. So <span class="CVXCodeinText" style="font-family: Verdana, Arial, Helvetica, sans-serif; font-size: 12px; line-height: 19.2px;"><span style="font-family: 'Courier New';">StartRegistration</span></span> can only be called for Users in the <span style="font-family: courier new,courier,monospace;">INVALID</span> state while <span class="CVXCodeinText" style="font-family: Verdana, Arial, Helvetica, sans-serif; font-size: 12px; line-height: 19.2px;"><span style="font-family: 'Courier New';">RestartRegistration</span></span> is used for those in the <span style="font-family: courier new,courier,monospace;">STARTED_REGISTRATION</span> state. Besides this, both methods work identically, as they both cause the RPA to re-start the User identity verification process.</div>
<h2 style="margin: 30px 0px 0.5em; padding: 0px 0px 10px; font-size: 2em; color: #2185c5; font-stretch: normal; line-height: 1em; font-family: Arial, sans-serif; border-bottom-width: 1px; border-bottom-style: solid; background-color: #ffffff;">Definition</h2>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt; background: #E2EFD9; margin-left: 0in; margin-right: 0in;">
<p class="CVXAPIDefinition" style="line-height: 125%; font-family: 'Courier New';"><span style="font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: inherit; color: #333333; line-height: 1.4; background-color: rgba(0, 0, 0, 0.0392157);">+ (MpinStatus*) StartRegistration: (const id&lt;IUser&gt;) user;</span></p>
<p class="CVXAPIDefinition" style="line-height: 125%; font-family: 'Courier New';"><span style="font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: inherit; color: #333333; line-height: 1.4; background-color: rgba(0, 0, 0, 0.0392157);">+ (MpinStatus*) StartRegistration: (const id&lt;IUser&gt;) user userData: (NSString*) userData;</span></p>
<p class="CVXAPIDefinition" style="line-height: 125%; font-family: 'Courier New';"><span style="font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: inherit; color: #333333; line-height: 1.4; background-color: rgba(0, 0, 0, 0.0392157);">+ (MpinStatus*) StartRegistration: (const id&lt;IUser&gt;) user activateCode: (NSString*) activateCode;</span></p>
<p class="CVXAPIDefinition" style="line-height: 125%; font-family: 'Courier New';"><span style="font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: inherit; color: #333333; line-height: 1.4; background-color: rgba(0, 0, 0, 0.0392157);">+ (MpinStatus*) StartRegistration: (const id&lt;IUser&gt;) user activateCode: (NSString*) activateCode userData: (NSString*) userData;</span></p>

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
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">The user to be registered</p>
</td>
</tr>
<tr>
<td style="width: 101.35pt; border: solid windowtext 1.0pt; border-top: none; background: #E2EFD9; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="135">
<p class="CVXAPIParameterName" style="margin-bottom: 6.0pt;"><b><i><span style="font-family: 'Courier New';">userData</span></i></b></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.75pt 0in 5.75pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">NSString*</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">No</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">Optional application specific user data that might be needed by the RPA in order to register the user</p>
</td>
</tr>
<tr>
<td style="width: 101.35pt; border: solid windowtext 1.0pt; border-top: none; background: #E2EFD9; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="135">
<p class="CVXAPIParameterName" style="margin-bottom: 6.0pt;"><b><i><span style="font-family: 'Courier New';">activateCode</span></i></b></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.75pt 0in 5.75pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">NSString*</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">No</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">Optional activation code that might be issued by the RPA and required during the registration process</p>
</td>
</tr>
</tbody>
</table>
<h2>Return Values</h2>
<ul style="margin: 5px 0px 0px 20px; padding: 0px 0px 0px 12px; font-family: Verdana, Arial, Helvetica, sans-serif; font-size: 12px; background-color: #ffffff;">
	<li><span style="font-family: 'courier new', courier, monospace;">OK</span> – User registation started successfully</li>
	<li><span style="font-family: 'courier new', courier, monospace;">IDENTITY_NOT_AUTHORIZED</span> – User registration refused by remote server</li>
	<li><span style="font-family: 'courier new', courier, monospace;">FLOW_ERROR</span> – the User is in the incorrect state, i.e. its state is not <span style="font-family: 'courier new', courier, monospace;">INVALID</span></li>
</ul>
<h2>Example</h2>
The following code snippet creates a new User and handles its registration process:
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 1.0pt 1.0pt 1.0pt;">
<div class="computer_code" style="margin-top: 0px; margin-bottom: 20px; padding: 0in; unicode-bidi: embed; font-family: Consolas, 'Courier New', Courier, mono, serif; border: none; font-size: 12px; line-height: 1.7em; color: #666666; background-color: #f9f9f9;">
<pre class="computer_code">id iuser = [MPin MakeNewUser:@"me@MIRACL.org" deviceName:@"My Smartphone"];
MpinStatus* mpinStatus = [MPin StartRegistration:iuser];

if(mpinStatus.status != OK) {
    // Handle error
}</pre>
</div>
</div>
<div class="WordSection1">
<h1><span style="font-size: 36px;"><span class="CVXCodeinText"><b><span style="font-family: 'Courier New';">RestartRegistration</span></b></span></span></h1>
<h2>Description</h2>
<p class="MsoNormal">The <span class="CVXCodeinText"><b><span style="font-family: 'Courier New';">RestartRegistration</span></b></span> method re-initializes the registration process for a User whose registration process has already started. The method causes the RPA to re-start the User identity verification procedure by sending a verification email. The User’s status remains at <span class="CVXCodeinText"><span style="font-family: 'Courier New';">STARTED_REGISTRATION</span></span> until the<span class="CVXCodeinText"><span style="font-family: 'Courier New';"> ConfirmRegistration</span></span> method has been executed successfully.</p>

<div class="info">In a demo application, the RPA can be configured to verify identities without starting a verification process. In this case, the status of the call will still be <span class="CVXCodeinText" style="line-height: 19.2000007629395px;"><span style="font-family: 'Courier New';">OK</span></span>, but the User state will be set to <span class="CVXCodeinText" style="line-height: 19.2000007629395px;"><span style="font-family: 'Courier New';">ACTIVATED</span></span>.</div>
<p class="MsoNormal">The application might require some additional data (passed in the <span class="CVXCodeinText"><span style="font-family: 'Courier New';">userData</span></span> parameter) to verify the user’s identity.</p>

<h3>What Is the Difference Between<span class="CVXCodeinText"><span style="font-family: 'Courier New';"> StartRegistration</span></span> and <span class="CVXCodeinText"><span style="font-family: 'Courier New';">RestartRegistration</span></span>?</h3>
<div class="info"><span style="line-height: 19.2000007629395px;">The </span><a href="#"><span class="CVXCodeinText" style="line-height: 19.2000007629395px;"><span style="font-family: 'Courier New';">StartRegistration</span></span><span style="line-height: 19.2000007629395px;"> method</span></a> generates a new M-Pin ID while <span class="CVXCodeinText" style="line-height: 19.2000007629395px;"><span style="font-family: 'Courier New';">RestartRegistration</span></span><span style="line-height: 19.2000007629395px;"> uses the ID that has already been generated for the user. So </span><span class="CVXCodeinText" style="line-height: 19.2000007629395px;"><span style="font-family: 'Courier New';">StartRegistration</span></span><span style="line-height: 19.2000007629395px;"> can be called only for Users in the </span><span style="font-family: courier new,courier,monospace;">INVALID</span><span style="line-height: 19.2000007629395px;"> state and </span><span class="CVXCodeinText" style="line-height: 19.2000007629395px;"><span style="font-family: 'Courier New';">RestartRegistration</span></span><span style="line-height: 19.2000007629395px;"> is designed to be used for Users in the </span><span style="font-family: courier new,courier,monospace;">STARTED_REGISTRATION</span><span style="line-height: 19.2000007629395px;"> state. Apart from that, both methods work basically the same, as they both cause the RPA to re-start the User identity verification.</span></div>
<h2>Definition</h2>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt; background: #E2EFD9; margin-left: 0in; margin-right: 0in;">
<p class="CVXAPIDefinition" style="line-height: 125%; font-family: 'Courier New';"><code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: inherit; padding: 0.2em 0px; margin: 0px; border-radius: 3px; background-color: rgba(0, 0, 0, 0.0392157);">+ (MpinStatus*) RestartRegistration: (const id&lt;IUser&gt;) user;</code></p>
<p class="CVXAPIDefinition" style="line-height: 125%; font-family: 'Courier New';"><code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: inherit; padding: 0.2em 0px; margin: 0px; border-radius: 3px; background-color: rgba(0, 0, 0, 0.0392157);">+ (MpinStatus*) RestartRegistration: (const id&lt;IUser&gt;) user userData: (const NSString*) userData;</code></p>

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
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">The user to be registered</p>
</td>
</tr>
<tr>
<td style="width: 101.35pt; border: solid windowtext 1.0pt; border-top: none; background: #E2EFD9; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="135">
<p class="CVXAPIParameterName" style="margin-bottom: 6.0pt;"><b><i><span style="font-family: 'Courier New';">userData</span></i></b></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.75pt 0in 5.75pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">NSString</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">No</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">Optional application specific user data that might be needed by the RPA in order to register the user</p>
</td>
</tr>
</tbody>
</table>
<h2>Return Values</h2>
<p class="MsoListParagraphCxSpFirst" style="margin-left: 0.5in; text-indent: -.25in; line-height: 105%;"><span style="font-family: Symbol;">·<span style="font: 7.0pt 'Times New Roman';">       </span></span><span class="CVXCodeinText"><span style="font-family: 'Courier New';">OK</span></span> – User registered has been restarted successfully.</p>
<p class="MsoListParagraphCxSpMiddle" style="margin-left: 0.5in; text-indent: -.25in; line-height: 105%;"><span style="font-family: Symbol;">·<span style="font: 7.0pt 'Times New Roman';">       </span></span><span class="CVXCodeinText"><span style="font-family: 'Courier New';">IDENTITY_NOT_AUTHORIZED</span></span> – User registration refused by remote server</p>
<p class="MsoListParagraphCxSpLast" style="margin-left: 0.5in; text-indent: -.25in; line-height: 105%;"><span style="font-family: Symbol;">·<span style="font: 7.0pt 'Times New Roman';">       </span></span><span class="CVXCodeinText"><span style="font-family: 'Courier New';">FLOW_ERROR</span></span> – the User is in the incorrect state, i.e its state is not <span style="font-family: courier new,courier,monospace;">STARTED_REGISTRATION</span><code> </code></p>

<h2>Example</h2>
<p class="MsoNormal">The following code snippet demonstrates a sample implementation of restarting a User registration</p>

<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt;">
<pre class="computer_code">id iuser = [MPin MakeNewUser:@"me@MIRACL.org" deviceName:@"My Smartphone"];
MpinStatus* mpinStatus = [MPin StartRegistration:iuser];

if(mpinStatus.status != OK) {
    // Handle error
}

if ([iuser getState] == STARTED_REGISTRATION)
{
    // Waiting for identity verification, which doesn't happen
    mpinStatus = [MPin RestartRegistration:iuser];
    
    //
    // Wait for identity confirmation
    //

    mpinStatus = [MPin ConfirmRegistration:iuser];
    
    if (mpinStatus.status == IDENTITY_NOT_VERIFIED) {
        // The identity has not been verified
    } else if (mpinStatus.status != OK) {
        // Handle error
    }
    
    NSString* setupPin;

    /* Read PIN from user */
    
    mpinStatus = [MPin FinishRegistration:iuser pin:setupPin];
    
    if (mpinStatus.status != OK) {
        // Handle error
    }
}</pre>
</div>
</div>
<h1><span class="CVXCodeinText"><b><span style="font-size: 29pt; line-height: 106%; font-family: 'Courier New';">ComfirmRegistration</span></b></span></h1>
<h2>Description</h2>
The ConfirmRegistration method allows the application to check whether the user identity verification process has been finalized or not. The <code style="color: #3e454c; font-size: 16.8px; line-height: 26.88px; box-sizing: border-box;">user</code> object should be either in the <code style="color: #3e454c; font-size: 16.8px; line-height: 26.88px; box-sizing: border-box;"><span style="font-size: 14px;"><span style="font-family: courier new,courier,monospace;">STARTED_REGISTRATION</span></span> </code>or the <code style="color: #3e454c; font-size: 16.8px; line-height: 26.88px; box-sizing: border-box;"><span style="font-size: 14px;"><span style="font-family: courier new,courier,monospace;">ACTIVATED</span></span> </code>state. The latter is possible if the RPA activated the user immediately with the call to <code style="color: #3e454c; font-size: 16.8px; line-height: 26.88px; box-sizing: border-box;">StartRegistration</code> and no verification process is started. During the call to <code style="color: #3e454c; font-size: 16.8px; line-height: 26.88px; box-sizing: border-box;">ConfirmRegistration,</code> the SDK will try to retrieve a Client Key for the user, which will succeed if the user has already been verified/activated, but will fail otherwise. The method returns status <span style="font-size: 14px;"><code style="color: #3e454c; font-size: 16.8px; line-height: 26.88px; box-sizing: border-box;">OK</code></span> if the Client Key is successfully retrieved and <span style="font-family: courier new,courier,monospace;"><code style="color: #3e454c; font-size: 16.8px; line-height: 26.88px; box-sizing: border-box;">IDENTITY_NOT_VERIFIED</code></span> if the identity is not verified. If the method is successful, the application will get the desired PIN/secret from the end-user and then call <code style="color: #3e454c; font-size: 16.8px; line-height: 26.88px; box-sizing: border-box;">FinishRegistration</code> to provide the PIN.
<div class="info">Note The application can provide a platform specific identifier for sending <em style="font-size: 12px; font-weight: normal; line-height: 19.2px;">push messages</em> to the device by using the optional parameter pushMessageIdentifier. The push messages can be used as an alternative to the <em style="line-height: 1.6em; font-size: 12px;">Access Number</em>, as part of the authentication flow.</div>
<h2>Definition</h2>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt; background: #E2EFD9; margin-left: 0in; margin-right: 0in;">
<p class="CVXAPIDefinition" style="line-height: 125%; font-family: 'Courier New';"><span style="font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: inherit; color: #333333; line-height: 1.4; background-color: rgba(0, 0, 0, 0.0392157);">+ (MpinStatus*) ConfirmRegistration: (const id&lt;IUser&gt;) user;</span></p>
<p class="CVXAPIDefinition" style="line-height: 125%; font-family: 'Courier New';"><span style="font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: inherit; color: #333333; line-height: 1.4; background-color: rgba(0, 0, 0, 0.0392157);">+ (MpinStatus*) ConfirmRegistration: (const id&lt;IUser&gt;) user pushNotificationIdentifier: (NSString*) pushNotificationIdentifier;</span></p>

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
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">The user that is being registered</p>
</td>
</tr>
<tr>
<td style="width: 101.35pt; border: solid windowtext 1.0pt; border-top: none; background: #E2EFD9; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="135">
<p class="CVXAPIParameterName" style="margin-bottom: 6.0pt;"><b><span style="font-family: 'Courier New';">pushNotificationIdentifier</span></b></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.75pt 0in 5.75pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">NSString*</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">No</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">An application instance specific Push Message Identifier/Token, which could later be used by the server to send Push Messages to the application.</p>
</td>
</tr>
</tbody>
</table>
<h2>Return Values</h2>
<ul>
	<li>OK - if the client key is successfully retrieved</li>
	<li>IDENTITY_NOT_VERIFIED - if the user identity is not verified</li>
</ul>
<h2>Example</h2>
<pre class="computer_code">id iuser = [MPin MakeNewUser:@"me@MIRACL.org" deviceName:@"My Smartphone"];
MpinStatus* mpinStatus = [MPin StartRegistration:iuser];

if(mpinStatus.status != OK) {
    // Handle error
}

if ([iuser getState] == STARTED_REGISTRATION)
{
    // Waiting for identity verification, which doesn't happen
    mpinStatus = [MPin RestartRegistration:iuser];
    
    //
    // Wait for identity confirmation
    //

    mpinStatus = [MPin ConfirmRegistration:iuser];
    
    if (mpinStatus.status == IDENTITY_NOT_VERIFIED) {
        // The identity has not been verified
    } else if (mpinStatus.status != OK) {
        // Handle error
    }
    
    NSString* setupPin;

    /* Read PIN from user */
    
    mpinStatus = [MPin FinishRegistration:iuser pin:setupPin];
    
    if (mpinStatus.status != OK) {
        // Handle error
    }
}</pre>
<div class="WordSection1">
<h1><span class="CVXCodeinText;"><b><span style="font-family: 'Courier New';">FinishRegistration</span></b></span></h1>
<h2>Description</h2>
<p class="MsoNormal">This method finalizes the user registration process. It extracts the <em style="box-sizing: border-box; color: #333333; font-family: 'Helvetica Neue', Helvetica, 'Segoe UI', Arial, freesans, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol'; font-size: 16px; font-weight: normal; line-height: 25.6px;">M-Pin Token</em> from the <em style="box-sizing: border-box; color: #333333; font-family: 'Helvetica Neue', Helvetica, 'Segoe UI', Arial, freesans, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol'; font-size: 16px; font-weight: normal; line-height: 25.6px;">Client Key </em>for the provided <code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0.2em 0px; margin: 0px; border-radius: 3px; color: #333333; background-color: rgba(0, 0, 0, 0.0392157);">pin</code> (secret), and then stores the token in the secure storage. On successful completion, the User state will be set to <code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0.2em 0px; margin: 0px; border-radius: 3px; color: #333333; background-color: rgba(0, 0, 0, 0.0392157);">REGISTERED</code> and the method will return status <code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0.2em 0px; margin: 0px; border-radius: 3px; color: #333333; background-color: rgba(0, 0, 0, 0.0392157);">OK.</code></p>

<h2>Definition</h2>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt; background: #E2EFD9; margin-left: 0in; margin-right: 0in;">
<p class="CVXAPIDefinition">+ (MpinStatus*) FinishRegistration: (const id&lt;IUser&gt;) user pin: (NSString*) pin;</p>

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
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;"><span style="color: #3e454c; font-family: Lato, sans-serif; font-size: 16.8px;">The User ID</span></p>
</td>
</tr>
<tr>
<td style="width: 101.35pt; border: solid windowtext 1.0pt; border-top: none; background: #E2EFD9; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="135">
<p class="CVXAPIParameterName" style="margin-bottom: 6.0pt;"><b><i><span style="font-family: 'Courier New';">pin</span></i></b></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.75pt 0in 5.75pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">NSString*</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">Yes</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">The pin that is entered by the user</p>
</td>
</tr>
</tbody>
</table>
<h2>Return Status</h2>
<p class="MsoListParagraphCxSpFirst" style="margin-left: 0.5in; text-indent: -.25in; line-height: 105%;"><span style="font-family: Symbol;">·<span style="font: 7.0pt 'Times New Roman';">       </span></span><span class="CVXCodeinText"><span style="font-family: 'Courier New';">OK</span></span> – User registered successfully and its status set to <span class="CVXCodeinText"><span style="font-family: 'Courier New';">REGISTERED</span></span></p>
<p class="MsoListParagraphCxSpMiddle" style="margin-left: 0.5in; text-indent: -.25in; line-height: 105%;"><span style="font-family: Symbol;">·<span style="font: 7.0pt 'Times New Roman';">       </span></span><span class="CVXCodeinText"><span style="font-family: 'Courier New';">FLOW_ERROR</span></span> – the User object is in an incorrect state (See <a href="#">Understanding User States</a>).</p>

<h2>Example</h2>
<p class="MsoNormal">The following code snippet creates a new User identity for a particular device and if the registration process is successful, finalizes it.</p>

<div style="border: solid windowtext 1.0pt; padding: 1.0pt 1.0pt 1.0pt 1.0pt;">
<pre class="computer_code">id iuser = [MPin MakeNewUser:@"me@MIRACL.org" deviceName:@"My Smartphone"];
MpinStatus* mpinStatus = [MPin StartRegistration:iuser];

if(mpinStatus.status != OK) {
    // Handle error
}

if ([iuser getState] == STARTED_REGISTRATION)
{
    // Waiting for identity verification, which doesn't happen
    mpinStatus = [MPin RestartRegistration:iuser];
    
    //
    // Wait for identity confirmation
    //

    mpinStatus = [MPin ConfirmRegistration:iuser];
    
    if (mpinStatus.status == IDENTITY_NOT_VERIFIED) {
        // The identity has not been verified
    } else if (mpinStatus.status != OK) {
        // Handle error
    }
    
    NSString* setupPin;

    /* Read PIN from user */
    
    mpinStatus = [MPin FinishRegistration:iuser pin:setupPin];
    
    if (mpinStatus.status != OK) {
        // Handle error
    }
}</pre>
<p class="CVXCodeExample"></p>

</div>
</div>