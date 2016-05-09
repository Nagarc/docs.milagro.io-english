<div class="WordSection1">
<h1>User Management Methods</h1>
<h2>Overview</h2>
<p class="MsoNormal">This page provides a list and brief description of the User Management methods used in the Milagro MFA Mobile SDK for Android. They relate to user management operations like creating, retrieving and deleting users.</p>
<p class="MsoNormal">To view a list of all methods, refer to the <a href="#">API Reference</a> page.</p>

</div>
<div class="WordSection1">
<h1><span class="CVXCodeinText"><b><span style="font-family: 'Courier New'; font-size: 42px;">MakeNewUser</span></b></span></h1>
<h2>Description</h2>
<p class="MsoNormal">The <span class="CVXCodeinText"><b><span style="font-family: 'Courier New';">MakeNewUser</span></b></span> method creates a new <span class="CVXCodeinText"><span style="font-family: 'Courier New';">User</span></span> object where the <span class="CVXCodeinText"><span style="font-family: 'Courier New';">User</span></span> object represents an end-user of the Milagro MFA authentication. The User has its own unique identity which is passed as the <span class="CVXCodeinText"><span style="font-family: 'Courier New';">id</span></span> parameter to this method. You can also specify an optional <span class="CVXCodeinText"><span style="font-family: 'Courier New';">deviceName</span></span> as a User can have multiple devices. The <span class="CVXCodeinText"><span style="font-family: 'Courier New';">deviceId</span></span> is passed to the RPA which stores it and uses it later to determine which M-Pin ID is associated with this device. The return value is a reference to the newly created user.</p>

<div class="info" style="margin-left: 40px;">The newly created User is in an <span class="CVXCodeinText" style="line-height: 19.2000007629395px;"><span style="font-family: 'Courier New';">INVALID</span></span> state.</div>
<div class="info" style="margin-left: 40px;">For a description of the User class, see <a href="#">Understanding User States</a></div>
The Java version of the User class is as follows:
<pre class="computer_code" style="box-sizing: border-box; overflow: auto; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; font-stretch: normal; line-height: 1.45; padding: 16px; border-radius: 3px; word-wrap: normal; word-break: normal; color: #333333; background-color: #f7f7f7;"><span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">public</span> <span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">class</span> <span class="pl-en" style="box-sizing: border-box; color: #795da3;">User</span> <span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">implements</span> <span class="pl-e" style="box-sizing: border-box; color: #795da3;">Closeable</span> {

    <span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">public</span> <span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">enum</span> <span class="pl-en" style="box-sizing: border-box; color: #795da3;">State</span> {
        <span class="pl-c1" style="box-sizing: border-box; color: #0086b3;">INVALID</span>,
        <span class="pl-c1" style="box-sizing: border-box; color: #0086b3;">STARTED_REGISTRATION</span>,
        <span class="pl-c1" style="box-sizing: border-box; color: #0086b3;">ACTIVATED</span>,
        <span class="pl-c1" style="box-sizing: border-box; color: #0086b3;">REGISTERED</span>,
        <span class="pl-c1" style="box-sizing: border-box; color: #0086b3;">BLOCKED</span>
    };

    <span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">public</span> <span class="pl-smi" style="box-sizing: border-box;">String</span> <span class="pl-en" style="box-sizing: border-box; color: #795da3;">getId</span>() {
        <span class="pl-c1" style="box-sizing: border-box; color: #0086b3;">...</span>
    }

    <span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">public</span> <span class="pl-smi" style="box-sizing: border-box;">State</span> <span class="pl-en" style="box-sizing: border-box; color: #795da3;">getState</span>() {
        <span class="pl-c1" style="box-sizing: border-box; color: #0086b3;">...</span>
    }

    <span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">@Override</span>
    <span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">public</span> <span class="pl-smi" style="box-sizing: border-box;">String</span> <span class="pl-en" style="box-sizing: border-box; color: #795da3;">toString</span>() {
        <span class="pl-k" style="box-sizing: border-box; color: #a71d5d;">return</span> getId();
    }

    <span class="pl-c1" style="box-sizing: border-box; color: #0086b3;">...</span>
}</pre>
<h2>Definition</h2>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt; background: #E2EFD9; margin-left: 0in; margin-right: 0in;">
<p class="CVXAPIDefinition" style="line-height: 105%; font-family: 'Courier New';"><b>User MakeNewUser(</b>String<b> <i>id</i>)</b></p>
<p class="CVXAPIDefinition" style="line-height: 105%; font-family: 'Courier New';"><b>User MakeNewUser(</b>String<b> <i>id</i>, </b>String<b> <i>deviceName</i></b><b>)</b></p>

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
<p class="CVXAPIParameterName" style="margin-bottom: 6.0pt;"><b><i><span style="font-family: 'Courier New';">id</span></i></b></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.75pt 0in 5.75pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">String</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">Yes</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">A string that uniquely identifies the User, e.g. the end-user’s email address</p>
</td>
</tr>
<tr>
<td style="border: solid windowtext 1.0pt; border-top: none; background: #E2EFD9; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="CVXAPIParameterName" style="margin-bottom: 6.0pt;"><b><i><span style="font-family: 'Courier New';">deviceName</span></i></b></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.75pt 0in 5.75pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">String</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">No</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">A string identifying the particular end-user device. Each <span class="CVXCodeinText"><span style="font-family: 'Courier New';">deviceName</span></span> must be unique for its User.</p>
</td>
</tr>
</tbody>
</table>
<h2>Return Values</h2>
Returns an object for the new User
<h2>Example</h2>
<p class="MsoNormal">The following code snippet creates a new User identity.</p>

<div style="border: solid windowtext 1.0pt; padding: 1.0pt 1.0pt 1.0pt 1.0pt;">
<pre class="computer_code">User user = sdk.MakeNewUser("me@miracl.org");
Status status = sdk.StartRegistration(user);

if (status.getStatusCode() != Status.Code.OK) {
   // handle error
}

if (user.getState() != State.ACTIVATED) {
   // ask for verification
}

status = sdk.ConfirmRegistration(user);

if (status.getStatusCode() != Status.Code.OK) {
   // handle error
}

String pin;

/** Ask user to provide PIN or other secret here **/

status = sdk.FinishRegistration(user, pin);

if (status.getStatusCode() != Status.Code.OK) {
   // handle error
}</pre>
</div>
</div>
<div class="WordSection1">
<h1><span class="CVXCodeinText"><b><span style="font-family: 'Courier New'; font-size: 42px;">ListUsers</span></b></span></h1>
<h2>Description</h2>
The <strong>ListUsers</strong> method populates a list with all current Users, irrespective of their state.

The SDK's Users List contains a list of users in various states, which reflects their registration statuses.
<h2>Definition</h2>
<table class="MsoNormalTable" style="border-collapse: collapse;" border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td style="width: 469.8pt; border: solid windowtext 1.0pt; background: #E2EFD9; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="626">
<p class="CVXAPIDefinition"><strong><span style="line-height: 105%; font-family: 'Courier New';">void ListUsers</span></strong><b><span style="line-height: 105%; font-family: 'Courier New';">(List&lt;User&gt; </span></b><em><strong><span style="line-height: 105%; font-family: 'Courier New';">users</span></strong></em><b><span style="line-height: 105%; font-family: 'Courier New';">)</span></b></p>
</td>
</tr>
</tbody>
</table>
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
<p class="CVXAPIParameterName" style="margin-bottom: 6.0pt;"><b><i><span style="font-family: 'Courier New';">users</span></i></b></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.75pt 0in 5.75pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;">List&lt;User&gt;</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;">Yes</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;">The list of users showing their registration status</p>
</td>
</tr>
</tbody>
</table>
<h2>Return Values</h2>
None
<h2>Example</h2>
<div class="normal">The following code snippet matches a User's identity against the list of all Users and if there is a match, deletes the selected User.</div>
&nbsp;
<div style="margin-left: 4.5pt;">
<div class="computer_code">List usersList = new ArrayList(); User selectedUser;

sdk.ListUsers(usersList);

for (User user : usersList) {

if ("me@MIRACL.org".equals(user.getId())) {

selectedUser = user;

break;

}

}if (selectedUser) {

sdk.DeleteUser(selectedUser);

}

</div>
</div>
</div>
<div class="WordSection1">
<h1><span class="CVXCodeinText"><b><span style="font-family: 'Courier New'; font-size: 42px;">DeleteUser</span></b></span></h1>
<h2>Description</h2>
<p class="MsoNormal">The <span class="CVXCodeinText"><b><span style="font-family: 'Courier New';">DeleteUser</span></b></span> method deletes a User from the Users List maintained by the SDK and all the data related to this User, such as the User’s M-Pin ID, State and M-Pin Token.</p>

<div class="info">As the <span class="CVXCodeinText" style="line-height: 19.2000007629395px;"><b><span style="font-family: 'Courier New';">DeleteUser</span></b></span> method deletes all the data related to the User, a new User with the same identity can be created after that with the <a href="#"><span class="CVXCodeinText" style="line-height: 19.2000007629395px;"><span style="font-family: 'Courier New';">MakeNewUser</span></span></a> method.</div>
<h2>Definition</h2>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt; background: #E2EFD9; margin-left: 0in; margin-right: 0in;">
<p class="CVXAPIDefinition"><b><span style="line-height: 105%; font-family: 'Courier New';">void DeleteUser(</span></b><span style="line-height: 105%; font-family: 'Courier New';">User<b> <i>user</i>)</b></span></p>

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
<p class="CVXAPIParameterName" style="margin-bottom: 6.0pt;"><b><i><span style="font-family: 'Courier New';">user</span></i></b></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.75pt 0in 5.75pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal;">User</p>
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
<p class="CVXCodeExample" style="border: none; padding: 0in;"><span style="font-size: 11.0pt; line-height: 150%; font-family: 'Courier New';">List usersList = new ArrayList(); User selectedUser;

sdk.ListUsers(usersList);

for (User user : usersList) {

if ("me@MIRACL.org".equals(user.getId())) {

selectedUser = user;

break;

}

}</span></p>
if (selectedUser) {

sdk.DeleteUser(selectedUser);

}

</div>
</div>