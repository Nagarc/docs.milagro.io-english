---
currentMenu: milagro-mfa-mobile-sdk-user-management-methods-ios
---

<div class="WordSection1">
<h1>User Management Methods - Milagro MFA Mobile SDK for iOS</h1>
<h2>Overview</h2>
<p class="MsoNormal">This page provides a list, along with brief descriptions, of the User Management methods used in the Milagro MFA Mobile SDK for iOS. To view the other methods, refer to the <a href="#">API Reference</a> page.</p>

</div>
<div class="WordSection1">
<h1><span class="CVXCodeinText"><b><span style="font-family: 'Courier New'; font-size: 42px;">MakeNewUser</span></b></span></h1>
<h2>Description</h2>
<p class="MsoNormal">This method creates a new User object which represents an end-user . The User has its own unique identity which is passed as the id parameter to this method. You can also specify an optional <span style="font-family: courier new,courier,monospace;">deviceName</span><span style="font-family: arial,helvetica,sans-serif;"><span class="CVXCodeinText">, as a</span> U</span>ser can have multiple Devices. The deviceId is passed to the RPA which stores it and uses it later to determine which M-Pin ID is associated with this Device. The return value is a reference to the newly created user.</p>

<div class="info" style="margin-left: 40px;">Note: The newly created User is in an <span class="CVXCodeinText" style="line-height: 19.2000007629395px;"><span style="font-family: 'Courier New';">INVALID</span></span> state.</div>
<div class="info" style="margin-left: 40px;">For a description of the User class, see <a href="#">Understanding User States</a>.</div>
<p style="box-sizing: border-box; margin-top: 0px; margin-bottom: 16px; color: #333333; font-family: 'Helvetica Neue', Helvetica, 'Segoe UI', Arial, freesans, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol'; font-size: 16px; line-height: 25.6px; background-color: #ffffff;">
The Objective-C version of the User class is as follows:</p>

<div class="highlight highlight-source-objc" style="box-sizing: border-box; margin-bottom: 16px; color: #333333; font-family: 'Helvetica Neue', Helvetica, 'Segoe UI', Arial, freesans, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol'; font-size: 16px; line-height: 25.6px; background-color: #ffffff;">
<pre style="box-sizing: border-box; overflow: auto; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; margin-top: 0px; margin-bottom: 0px; font-stretch: normal; line-height: 1.45; padding: 16px; border-radius: 3px; word-wrap: normal; word-break: normal; background-color: #f7f7f7;"><span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">typedef</span> <span class="pl-en" style="box-sizing: border-box; color: #795da3;">NS_ENUM</span>(<span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">NSInteger</span>, UserState)
{
    INVALID,
    STARTED_REGISTRATION,
    REGISTERED,
    ACTIVATED,
    BLOCKED
};

<span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">@protocol</span> <span class="pl-en" style="box-sizing: border-box; color: #795da3;">IUser</span> &lt;NSObject&gt;
-(<span class="pl-c1" style="box-sizing: border-box; color: #0086b3;">NSString</span>*) <span class="pl-en" style="box-sizing: border-box; color: #795da3;">getIdentity</span>;
-(UserState) <span class="pl-en" style="box-sizing: border-box; color: #795da3;">getState</span>;
<span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">@end</span></pre>
</div>
<h2>Definition</h2>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt; background: #E2EFD9; margin-left: 0in; margin-right: 0in;">
<p class="CVXAPIDefinition" style="line-height: 125%; font-family: 'Courier New';"><span style="font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: inherit; color: #333333; line-height: 1.4; background-color: rgba(0, 0, 0, 0.0392157);">+ (id&lt;IUser&gt;) MakeNewUser: (const NSString*) identity;</span></p>
<p class="CVXAPIDefinition" style="line-height: 125%; font-family: 'Courier New';"><span style="font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: inherit; color: #333333; line-height: 1.4; background-color: rgba(0, 0, 0, 0.0392157);">+ (id&lt;IUser&gt;) MakeNewUser: (const NSString*) identity deviceName: (const NSString*) devName;</span></p>

</div>
<h2>Parameters</h2>
<table class="MsoNormalTable" style="margin-left: -.4pt; border-collapse: collapse; border: none;" border="1" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td style="border: solid windowtext 1.0pt; background: #F4F4F4; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
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
<td style="border: solid windowtext 1.0pt; border-top: none; background: #E2EFD9; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="CVXAPIParameterName" style="margin-bottom: 6.0pt;"><span style="font-family: 'Courier New';"><b><i>identity</i></b></span></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.75pt 0in 5.75pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">NSString</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">Yes</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">A string that uniquely identifies the User, e.g. the end-user’s email address.</p>
</td>
</tr>
<tr>
<td style="border: solid windowtext 1.0pt; border-top: none; background: #E2EFD9; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="CVXAPIParameterName" style="margin-bottom: 6.0pt;"><b><i><span style="font-family: 'Courier New';">devName</span></i></b></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.75pt 0in 5.75pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">NSString</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">No</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">A user-friendly string that identifies the particular end-user device. Each deviceID must be unique for its User.</p>
</td>
</tr>
</tbody>
</table>
<h2>Return Values</h2>
Returns an object for the new User.
<h2>Examples</h2>
<h3>Example1</h3>
<p class="MsoNormal">The following code snippet creates a new User identity.</p>

<div style="border: solid windowtext 1.0pt; padding: 1.0pt 1.0pt 1.0pt 1.0pt;">
<pre class="computer_code"><span style="font-size: 12px;"><span style="line-height: 150%; font-family: 'Courier New';">id</span></span><span style="font-size: 11.0pt; line-height: 150%; font-family: 'Courier New';"><span style="font-size: 12px;"> iuser = [MPin MakeNewUser:@"me@MIRACL.org"];
MpinStatus* mpinStatus = [MPin StartRegistration:iuser];

switch (mpinStatus.status) {
case OK:
    switch ([iuser getState]) {
    case INVALID:
       /* Do something */
       break;
    case STARTED_REGISTRATION:
       /* Do something */
       break;
    case ACTIVATED:
       /* Do something */
       break;
    case REGISTERED:
       /* Do something */
       break;
    default:
       /* Do something */
       break;
    }
    break;

default:
    /* Do something */
    break;
} </span></span></pre>
</div>
<h3>Example2</h3>
<p class="MsoNormal">The following code snippet creates a new User identity specifying a Device Name.</p>

<div style="border: solid windowtext 1.0pt; padding: 1.0pt 1.0pt 1.0pt 1.0pt;">
<pre class="computer_code"><span style="font-size: 12px;"><span style="line-height: 150%; font-family: 'Courier New';">id</span></span><span style="font-size: 11.0pt; line-height: 150%; font-family: 'Courier New';"><span style="font-size: 12px;"> iuser = [MPin MakeNewUser:@"me@MIRACL.org" deviceName:@"My office smartphone"];
MpinStatus* mpinStatus = [MPin StartRegistration:iuser];

switch (mpinStatus.status) {
case OK:
    switch ([iuser getState]) {
    case INVALID:
       /* Do something */
       break;
    case STARTED_REGISTRATION:
       /* Do something */
       break;
    case ACTIVATED:
       /* Do something */
       break;
    case REGISTERED:
       /* Do something */
       break;
    default:
       /* Do something */
       break;
    }
    break;

default:
    /* Do something */
    break;
} </span></span></pre>
</div>
</div>
<div class="WordSection1">
<h1><span class="CVXCodeinText"><b><span style="font-family: 'Courier New'; font-size: 42px;">DeleteUser</span></b></span></h1>
<h2>Description</h2>
<p class="Normal">This method deletes a user from the users list that the SDK maintains. All the user data, including its M-Pin ID, its state and M-Pin Token will be deleted.</p>

<div class="info">As the <span class="CVXCodeinText" style="line-height: 19.2000007629395px;"><b><span style="font-family: 'Courier New';">DeleteUser</span></b></span> method deletes all the data related to the User, a new User with the same identity can be created after that, using the <span class="CVXCodeinText" style="line-height: 19.2000007629395px;"><span style="font-family: 'Courier New';">MakeNewUser</span></span> method.</div>
<h2>Definition</h2>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt; background: #E2EFD9; margin-left: 0in; margin-right: 0in;">
<p class="CVXAPIDefinition"><code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: inherit; padding: 0.2em 0px; margin: 0px; border-radius: 3px; background-color: rgba(0, 0, 0, 0.0392157);">+ (void) DeleteUser: (const id&lt;IUser&gt;) user;</code></p>

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
<p class="CVXAPIParameterName" style="margin-bottom: 6.0pt;"><em><strong><span style="font-family: 'Courier New';">user</span></strong></em></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.75pt 0in 5.75pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;">IUser</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;">Yes</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;">The User ID</p>
</td>
</tr>
</tbody>
</table>
<h2>Return Values</h2>
None
<h2>Example</h2>
<p class="MsoNormal">The following code snippet matches a User's identity against the list of all Users and if there is a match, deletes the selected User.</p>

<div style="border: solid windowtext 1.0pt; padding: 1.0pt 1.0pt 1.0pt 1.0pt; margin-left: 4.5pt; margin-right: 4.5pt;">
<pre class="computer_code" style="border: none; padding: 0in;"><span style="font-size: 12px;"><span style="line-height: 150%; font-family: 'Courier New';">NSMutableArray *users = [MPin listUsers];

for (int i = 0; i &lt; [users count]; i++) {
    id</span></span><span style="font-size: 11.0pt; line-height: 150%; font-family: 'Courier New';"><span style="font-size: 12px;"> iuser = [users objectAtIndex:i];
    [MPin DeleteUser:iuser];
} </span></span></pre>
</div>
</div>
<div class="WordSection1">
<h1><span class="CVXCodeinText"><b><span style="font-family: 'Courier New'; font-size: 42px;">ListUsers</span></b></span></h1>
<h2>Description</h2>
<p class="MsoNormal">This method populates the provided vector with all the users that are currently available in the SDK's users list. They will be listed according to their states to indicate their registration status.</p>

<h2>Definition</h2>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt; background: #E2EFD9; margin-left: 0in; margin-right: 0in;">
<p class="CVXAPIDefinition"><code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: inherit; padding: 0.2em 0px; margin: 0px; border-radius: 3px; background-color: rgba(0, 0, 0, 0.0392157);">+ (NSMutableArray*) listUsers;</code></p>

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
<p class="CVXAPIParameterName" style="margin-bottom: 6.0pt;"><em><strong><span style="font-family: 'Courier New';">listUsers</span></strong></em></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.75pt 0in 5.75pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;">NSMutableArray</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;"></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;"></p>
</td>
</tr>
</tbody>
</table>
<h2>Return Values</h2>
Returns a list of users in <span style="font-family: 'Courier New';">NSMutableArray*</span> format.
<h2>Example</h2>
<p class="MsoNormal">The following code snippet matches a User's identity against the list of all Users and if there is a match, deletes the selected User.</p>

<div style="border: solid windowtext 1.0pt; padding: 1.0pt 1.0pt 1.0pt 1.0pt; margin-left: 4.5pt; margin-right: 4.5pt;">
<pre class="computer_code" style="border: none; padding: 0in;"><span style="font-size: 12px;"><span style="line-height: 150%; font-family: 'Courier New';">NSMutableArray *users = [MPin listUsers];

for (int i = 0; i &lt; [users count]; i++) {
    id</span></span><span style="font-size: 11.0pt; line-height: 150%; font-family: 'Courier New';"><span style="font-size: 12px;"> iuser = [users objectAtIndex:i];
    [MPin DeleteUser:iuser];
} </span></span></pre>
</div>
</div>