<h1>Registration Methods</h1>
<h2>Overview</h2>
<p class="MsoNormal">This section provides a list and brief description of the Registration methods used in the Milagro MFA Mobile SDK for Android. The methods detail the process of registering a new User.</p>
<p class="MsoNormal">To view all methods used, refer to the <a href="#">API Reference</a> page.</p>

<div class="WordSection1">
<h1><span class="CVXCodeinText"><b><span style="font-family: 'Courier New'; font-size: 42px;">StartRegistration</span></b></span></h1>
<h2>Description</h2>
<p style="margin-bottom: 16px; line-height: 25.6px; box-sizing: border-box; color: #333333; font-family: 'Helvetica Neue', Helvetica, 'Segoe UI', Arial, freesans, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol'; font-size: 16px;">This method initializes the registration for a User that has already been created. The SDK starts the M-Pin Setup flow, sending the necessary requests to the back-end service. The State of the User instance will change to <code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0.2em 0px; margin: 0px; border-radius: 3px; background-color: rgba(0, 0, 0, 0.0392157);">STARTED_REGISTRATION</code>. The status will indicate whether the operation was successful or not. During this call, an M-Pin ID for the end-user will be issued by the RPS and stored within the user object. The RPA can also start a user identity verification procedure, by sending a verification e-mail.</p>
<p style="margin-bottom: 16px; line-height: 25.6px; box-sizing: border-box; color: #333333; font-family: 'Helvetica Neue', Helvetica, 'Segoe UI', Arial, freesans, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol'; font-size: 16px;">The optional <code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0.2em 0px; margin: 0px; border-radius: 3px; color: #333333; background-color: rgba(0, 0, 0, 0.0392157);">activateCode</code> parameter might be provided if the registration process requires such. In cases when the user verification is done through a <em style="box-sizing: border-box; color: #333333; font-family: 'Helvetica Neue', Helvetica, 'Segoe UI', Arial, freesans, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol'; font-size: 16px; font-weight: normal; line-height: 20.48px;">One-Time-Code</em> (OTC) or through an SMS that carries such code, this OTC should be passed as the <code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0.2em 0px; margin: 0px; border-radius: 3px; color: #333333; background-color: rgba(0, 0, 0, 0.0392157);">activateCode</code> parameter. In those cases, the identity verification should be completed instantly and the User State will be set to <code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0.2em 0px; margin: 0px; border-radius: 3px; color: #333333; background-color: rgba(0, 0, 0, 0.0392157);">ACTIVATED</code>.</p>
<p style="margin-bottom: 16px; line-height: 25.6px; box-sizing: border-box; color: #333333; font-family: 'Helvetica Neue', Helvetica, 'Segoe UI', Arial, freesans, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol'; font-size: 16px;">The application can also pass additional <code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0.2em 0px; margin: 0px; border-radius: 3px; background-color: rgba(0, 0, 0, 0.0392157);">userData</code> which might help the RPA to verify the user identity. The RPA might decide to verify the identity without starting a verification process. In this case, the <code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0.2em 0px; margin: 0px; border-radius: 3px; background-color: rgba(0, 0, 0, 0.0392157);">Status</code> of the call will still be <code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0.2em 0px; margin: 0px; border-radius: 3px; background-color: rgba(0, 0, 0, 0.0392157);">OK</code>, but the User State will be set to <code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0.2em 0px; margin: 0px; border-radius: 3px; background-color: rgba(0, 0, 0, 0.0392157);">ACTIVATED</code>.</p>

<h3>What Is the Difference Between<span class="CVXCodeinText"><span style="font-family: 'Courier New';"> StartRegistration</span></span> and <span class="CVXCodeinText"><span style="font-family: 'Courier New';">RestartRegistration</span></span>?</h3>
<div class="info">The <span class="CVXCodeinText" style="line-height: 19.2000007629395px;"><span style="font-family: 'Courier New';">StartRegistration</span></span> method generates a new M-Pin ID while <a href="#"><span class="CVXCodeinText" style="line-height: 19.2000007629395px;"><span style="font-family: 'Courier New';">RestartRegistration</span></span></a> uses the ID that has already been generated for the user. So <span class="CVXCodeinText" style="line-height: 19.2000007629395px;"><span style="font-family: 'Courier New';">StartRegistration</span></span> can be called only for Users in the <span style="font-family: courier new,courier,monospace;">INVALID</span> state and <span class="CVXCodeinText" style="line-height: 19.2000007629395px;"><span style="font-family: 'Courier New';">RestartRegistration</span></span> is designed to be used for Users in the <span style="font-family: courier new,courier,monospace;">STARTED_REGISTRATION</span> state. Apart from that, both methods work basically the same, as they both cause the RPA to re-start the User identity verification.</div>
<h2>Definition</h2>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt; background: #E2EFD9; margin-left: 0in; margin-right: 0in;">
<p class="CVXAPIDefinition" style="line-height: 125%; font-family: 'Courier New';"><b>Status StartRegistration(</b>User <b><i>user</i>)</b></p>
<p class="CVXAPIDefinition" style="line-height: 125%; font-family: 'Courier New';"><b>Status StartRegistration(</b>User <b><i>user, </i></b>String<b><i> activateCode</i></b><strong><i>)</i></strong></p>
<p class="CVXAPIDefinition" style="line-height: 125%; font-family: 'Courier New';"><b>Status StartRegistration(</b>User <b><i>user, </i></b>String <b><i>activateCode, </i></b>String <b><i>userData)</i></b></p>

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
<p class="CVXAPIParameterName" style="margin-bottom: 6.0pt;"><span style="font-family: 'Courier New';"><b><i>user </i></b></span></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.75pt 0in 5.75pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">User</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">Yes</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">The ID of the User</p>
</td>
</tr>
<tr>
<td style="width: 101.35pt; border: solid windowtext 1.0pt; border-top: none; background: #E2EFD9; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="135">
<p class="CVXAPIParameterName" style="margin-bottom: 6.0pt;"><b><i><span style="font-family: 'Courier New';">activateCode</span></i></b></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.75pt 0in 5.75pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">String</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">No</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">Optional Activation Code that might be required by the RPA in order to register a user.</p>
</td>
</tr>
<tr>
<td style="width: 101.35pt; border: solid windowtext 1.0pt; border-top: none; background: #E2EFD9; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="135">
<p class="CVXAPIParameterName" style="margin-bottom: 6.0pt;"><b><i><span style="font-family: 'Courier New';">userData </span></i></b></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.75pt 0in 5.75pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">String</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">No</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">Additional User data that might be required by the RPA to verify the user’s identity</p>
</td>
</tr>
</tbody>
</table>
<h2>Return Values</h2>
<p class="MsoListParagraphCxSpFirst" style="margin-left: 0.5in; text-indent: -.25in; line-height: 105%;"><span style="font-family: Symbol;">·<span style="font: 7.0pt 'Times New Roman';">         </span></span><span class="CVXCodeinText"><span style="font-family: 'Courier New';">OK</span></span> – User registered successfully and its status set to <span class="CVXCodeinText"><span style="font-family: 'Courier New';">REGISTERED</span></span></p>
<p class="MsoListParagraphCxSpFirst" style="margin-left: 0.5in; text-indent: -.25in; line-height: 105%;"><span style="font-family: Symbol;">·<span style="font: 7.0pt 'Times New Roman';">         </span></span><span class="CVXCodeinText"><span style="font-family: 'Courier New';">IDENTITY_NOT_AUTHORIZED</span></span> – User registration refused by remote server</p>
<p class="MsoListParagraphCxSpFirst" style="margin-left: 0.5in; text-indent: -.25in; line-height: 105%;"><span style="font-family: Symbol;">·<span style="font: 7.0pt 'Times New Roman';">         </span></span><span class="CVXCodeinText"><span style="font-family: 'Courier New';">FLOW_ERROR</span></span> – the User is in the incorrect state, i.e. its state is not <span style="font-family: courier new,courier,monospace;">INVALID</span></p>

<h2>Example</h2>
<p class="MsoNormal">The following code snippet creates a new User and handles its registration process.</p>

<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt;">
<pre class="computer_code">Status status = sdk.StartRegistration(user);

if (status.getStatusCode() != Status.Code.OK) {
    // handle error
}

if (user.getState() != State.ACTIVATED) {
    int i = 0;
    
    while (user.getState() == State.STARTED_REGISTRATION) {
    
       // waiting for verification to be completed
       status = sdk.ConfirmRegistration(user); // if the verification has completed successfully, this displays the M-Pin PIN-Pad for the user to set up their PIN

       if (status.getStatusCode() != Status.Code.OK) {
          if (status.getStatusCode() == Status.Code.IDENTITY_NOT_VERIFIED) {
             //User identity has not been verified yet
             i++;
             if (i &gt;= 12) {
                status = sdk.RestartRegistration(user);

                if (status.getStatusCode() != Status.Code.OK) {
                   // handle error
                }
                i = 0;
             }
             SystemClock.sleep(10000);
          }
          else {
             // handle error
          }
       }
    }
}

status = sdk.ConfirmRegistration(user);

if (status.getStatusCode() != Status.Code.OK) {
    // handle error
}

String pin;
/** Ask the user to provide PIN or other secret here **/

status = sdk.FinishRegistration(user, pin);
if (status.getStatusCode() != Status.Code.OK) {
      // handle error
}</pre>
</div>
</div>
<div class="WordSection1">
<h1><span class="CVXCodeinText;"><b style="font-style: inherit;"><span style="font-family: 'Courier New';">RestartRegistration</span></b></span></h1>
<h2>Description</h2>
<p style="box-sizing: border-box; margin-top: 0px; margin-bottom: 16px; color: #333333; font-family: 'Helvetica Neue', Helvetica, 'Segoe UI', Arial, freesans, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol'; font-size: 16px; line-height: 25.6px; background-color: #ffffff;">This method re-initializes the registration process for a user, where registration has already started. The difference between this method and <code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0.2em 0px; margin: 0px; border-radius: 3px; background-color: rgba(0, 0, 0, 0.0392157);">StartRegistration()</code> is that it will not generate a new M-Pin ID, but will use the one that was already generated. Besides that, the methods follow the same procedures, such as getting the RPA to re-start the user identity verification procedure of sending a verification email to the user.</p>
<p style="box-sizing: border-box; margin-top: 0px; margin-bottom: 16px; color: #333333; font-family: 'Helvetica Neue', Helvetica, 'Segoe UI', Arial, freesans, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol'; font-size: 16px; line-height: 25.6px; background-color: #ffffff;">The application could also pass additional <code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0.2em 0px; margin: 0px; border-radius: 3px; background-color: rgba(0, 0, 0, 0.0392157);">userData</code> to help the RPA to verify the user identity. The RPA might decide to verify the identity without starting a verification process. In this case, the <code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0.2em 0px; margin: 0px; border-radius: 3px; background-color: rgba(0, 0, 0, 0.0392157);">Status</code> of the call will still be <code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0.2em 0px; margin: 0px; border-radius: 3px; background-color: rgba(0, 0, 0, 0.0392157);">OK</code>, but the User State will be set to <code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0.2em 0px; margin: 0px; border-radius: 3px; background-color: rgba(0, 0, 0, 0.0392157);">ACTIVATED</code>.</p>

<div class="info"><strong>Note: </strong>In a demo application, the RPA can be configured to verify identities without starting a verification process. In this case, the status of the call will still be <span class="CVXCodeinText" style="line-height: 19.2000007629395px;">OK</span>, but the User state is set to <span class="CVXCodeinText" style="line-height: 19.2000007629395px;">ACTIVATED</span>. The application might require some additional data (passed in the <span class="CVXCodeinText"><span style="font-family: 'Courier New';">userData</span></span> parameter) to verify the user’s identity.</div>
<h3>What Is the Difference Between<span class="CVXCodeinText"><span style="font-family: 'Courier New';"> StartRegistration</span></span> and <span class="CVXCodeinText"><span style="font-family: 'Courier New';">RestartRegistration</span></span>?</h3>
<div class="info"><span style="line-height: 19.2000007629395px;">The </span><a href="#"><span class="CVXCodeinText" style="line-height: 19.2000007629395px;">StartRegistration</span><span style="line-height: 19.2000007629395px;"> method</span></a> generates a new M-Pin ID while <span class="CVXCodeinText" style="line-height: 19.2000007629395px;">RestartRegistration</span><span style="line-height: 19.2000007629395px;"> uses the ID that has already been generated for the user. So </span><span style="font-family: courier new,courier,monospace;"><span class="CVXCodeinText" style="line-height: 19.2000007629395px;">StartRegistration</span></span><span style="line-height: 19.2000007629395px;"> is called only for Users in the </span><span style="font-family: courier new,courier,monospace;"><span class="CVXCodeinText" style="line-height: 19.2px;">INVALID</span></span> <span style="line-height: 19.2000007629395px;">state while </span><span style="font-family: courier new,courier,monospace;"><span class="CVXCodeinText" style="line-height: 19.2000007629395px;">RestartRegistration</span></span><span style="line-height: 19.2000007629395px;"> is called for Users in the </span><span style="font-family: courier new,courier,monospace;"><span class="CVXCodeinText" style="line-height: 19.2px;">STARTED_REGISTRATION</span></span> <span style="line-height: 19.2000007629395px;">state. Besides this, they are very similar, as they both cause the RPA to re-start the User identity verification.</span></div>
<h2>Definition</h2>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt; background: #E2EFD9; margin-left: 0in; margin-right: 0in;">
<p class="CVXAPIDefinition" style="line-height: 125%; font-family: 'Courier New';"><code style="box-sizing: border-box; font-family: Consolas,;">Status RestartRegistration(User user)</code></p>
<code style="box-sizing: border-box; font-family: Consolas,;">Status RestartRegistration(User user, String userData)</code>

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
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">The ID of the User</p>
</td>
</tr>
<tr>
<td style="width: 101.35pt; border: solid windowtext 1.0pt; border-top: none; background: #E2EFD9; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="135">
<p class="CVXAPIParameterName" style="margin-bottom: 6.0pt;"><b><i><span style="font-family: 'Courier New';">userData</span></i></b></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.75pt 0in 5.75pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">String</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">No</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">Additional User data that might be required by the RPA to verify the user’s identity</p>
</td>
</tr>
</tbody>
</table>
<h2>Return Values</h2>
<p class="MsoListParagraphCxSpFirst" style="margin-left: 0.5in; text-indent: -.25in; line-height: 105%;"><span style="font-family: Symbol;">·<span style="font: 7.0pt 'Times New Roman';">        </span></span><span class="CVXCodeinText"><span style="font-family: 'Courier New';">OK</span></span> – User registered successfully and status is set to <span class="CVXCodeinText"><span style="font-family: 'Courier New';">REGISTERED</span></span></p>
<p class="MsoListParagraphCxSpMiddle" style="margin-left: 0.5in; text-indent: -.25in; line-height: 105%;"><span style="font-family: Symbol;">·<span style="font: 7.0pt 'Times New Roman';">       </span></span><span class="CVXCodeinText"><span style="font-family: 'Courier New';">IDENTITY_NOT_AUTHORIZED</span></span> – User registration refused by remote server</p>
<p class="MsoListParagraphCxSpLast" style="margin-left: 0.5in; text-indent: -.25in; line-height: 105%;"><span style="font-family: Symbol;">·<span style="font: 7.0pt 'Times New Roman';">        </span></span><span class="CVXCodeinText"><span style="font-family: 'Courier New';">FLOW_ERROR</span></span> – the User is in the incorrect state, i.e its state is not <span style="font-family: courier new,courier,monospace;">STARTED_REGISTRATION</span></p>

<h2>Example</h2>
<p class="MsoNormal">The following code snippet demonstrates a sample implementation of restarting a User registration</p>

<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt;">
<pre class="computer_code">Status status = sdk.StartRegistration(user);

if (status.getStatusCode() != Status.Code.OK) {
    // handle error
}

if (user.getState() != State.ACTIVATED) {
    int i = 0;

    while (user.getState() == State.STARTED_REGISTRATION) {

        // waiting for verification to be completed
        status = sdk.ConfirmRegistration(user); // if the verification has completed successfully, this displays the M-Pin PIN-Pad for the user to set up their PIN

        if (status.getStatusCode() != Status.Code.OK) {
            if (status.getStatusCode() == Status.Code.IDENTITY_NOT_VERIFIED) {
                //User identity has not been verified yet
                i++;
                if (i &gt;= 12) {
                    status = sdk.RestartRegistration(user);

                    if (status.getStatusCode() != Status.Code.OK) {
                        // handle error
                    }
                    i = 0;
                }
                SystemClock.sleep(10000);
            }
            else {
            // handle error
            }
        }
    }
}

status = sdk.ConfirmRegistration(user);

if (status.getStatusCode() != Status.Code.OK) {
    // handle error
}

String pin;
/** Ask the user to provide PIN or other secret here **/

status = sdk.FinishRegistration(user, pin);
if (status.getStatusCode() != Status.Code.OK) {
    // handle error
}</pre>
</div>
</div>
<h1><span class="CVXCodeinText"><b><span style="font-size: 29pt; line-height: 106%; font-family: 'Courier New';">ComfirmRegistration</span></b></span></h1>
<h2>Description</h2>
The ConfirmRegistration method allows the application to check whether the user identity verification process has been finalized or not. The <code style="box-sizing: border-box; font-family: Consolas,;">user</code> object should be either in the <code style="box-sizing: border-box; font-family: Consolas,;">STARTED_REGISTRATION </code>or the <code style="box-sizing: border-box; font-family: Consolas,;">ACTIVATED </code>state. The latter is possible if the RPA activated the user immediately with the call to <code style="box-sizing: border-box; font-family: Consolas,;">StartRegistration</code> and no verification process is started. During the call to <code style="color: #3e454c; font-size: 16.8px; line-height: 26.88px; box-sizing: border-box;">ConfirmRegistration,</code> the SDK will try to retrieve a Client Key for the user, which will succeed if the user has already been verified/activated, but will fail otherwise. The method returns status <code style="color: #3e454c; font-size: 16.8px; line-height: 26.88px; box-sizing: border-box;">OK</code> if the Client Key is successfully retrieved and <code style="color: #3e454c; font-size: 16.8px; line-height: 26.88px; box-sizing: border-box;">IDENTITY_NOT_VERIFIED</code> if the identity is not verified. If the method is successful, the application will get the desired PIN/secret from the end-user and then call <code style="color: #3e454c; font-size: 16.8px; line-height: 26.88px; box-sizing: border-box;">FinishRegistration </code>to provide the PIN.
<div class="info">Note: <span style="font-size: 12px; line-height: 19.2px;">The application can provide a platform specific identifier for sending </span>push messages<span style="font-size: 12px; line-height: 19.2px;"> to the device by u</span><span style="line-height: 1.6em; font-size: 12px;">sing the optional parameter </span><code style="line-height: 1.6em; box-sizing: border-box; font-family: Consolas,;">pushMessageIdentifier</code><span style="line-height: 1.6em; font-size: 12px;">. The push messages can be used as an alternative to the </span><em style="line-height: 1.6em; font-size: 12px;">Access Number</em><span style="line-height: 1.6em; font-size: 12px;">, as part of the authentication flow.</span></div>
<h2>Definition</h2>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt; background: #E2EFD9; margin-left: 0in; margin-right: 0in;">
<p class="CVXAPIDefinition"><b><span style="line-height: 105%; font-family: 'Courier New';">Status ConfirmRegistration(User user)</span></b></p>
<p class="CVXAPIDefinition"><b><span style="line-height: 105%; font-family: 'Courier New';">Status ConfirmRegistration(User user, String pushMessageIdentifier)</span></b></p>

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
<p class="CVXAPIParameterName" style="margin-bottom: 6.0pt;"><b><span style="font-family: 'Courier New';">user</span></b></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.75pt 0in 5.75pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">IUser</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">Yes</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">The ID of the User</p>
</td>
</tr>
<tr>
<td style="width: 101.35pt; border: solid windowtext 1.0pt; border-top: none; background: #E2EFD9; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="135">
<p class="CVXAPIParameterName" style="margin-bottom: 6.0pt;"><b><span style="font-family: 'Courier New';">pushMessageIdentifier</span></b></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.75pt 0in 5.75pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;"><span style="font-size: 12px; font-family: inherit;">NSString</span></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">No</p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">Push Message Identifier or Token that is unique to the installed application and could be used to send push messages to it.</p>
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
<pre class="computer_code">Status status = sdk.StartRegistration(user);

if (status.getStatusCode() != Status.Code.OK) {
    // handle error
}

if (user.getState() != State.ACTIVATED) {
    int i = 0;
    
    while (user.getState() == State.STARTED_REGISTRATION) {
    
       // waiting for verification to be completed
       status = sdk.ConfirmRegistration(user); // if the verification has completed successfully, this displays the M-Pin PIN-Pad for the user to set up their PIN

       if (status.getStatusCode() != Status.Code.OK) {
          if (status.getStatusCode() == Status.Code.IDENTITY_NOT_VERIFIED) {
             //User identity has not been verified yet
             i++;
             if (i &gt;= 12) {
                status = sdk.RestartRegistration(user);

                if (status.getStatusCode() != Status.Code.OK) {
                   // handle error
                }
                i = 0;
             }
             SystemClock.sleep(10000);
          }
          else {
             // handle error
          }
       }
    }
}

status = sdk.ConfirmRegistration(user);

if (status.getStatusCode() != Status.Code.OK) {
    // handle error
}

String pin;
/** Ask the user to provide PIN or other secret here **/

status = sdk.FinishRegistration(user, pin);
if (status.getStatusCode() != Status.Code.OK) {
      // handle error
}</pre>
<div class="WordSection1">
<h1><span class="CVXCodeinText;"><b><span style="font-family: 'Courier New';">FinishRegistration</span></b></span></h1>
<h2>Description</h2>
<p class="MsoNormal">This method finalizes the user registration process. It extracts the <em style="box-sizing: border-box; color: #333333; font-family: 'Helvetica Neue', Helvetica, 'Segoe UI', Arial, freesans, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol'; font-size: 16px; font-weight: normal; line-height: 20.48px;">M-Pin Token</em> from the <em style="box-sizing: border-box; color: #333333; font-family: 'Helvetica Neue', Helvetica, 'Segoe UI', Arial, freesans, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol'; font-size: 16px; font-weight: normal; line-height: 20.48px;">Client Key </em>for the provided <code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0.2em 0px; margin: 0px; border-radius: 3px; color: #333333; background-color: rgba(0, 0, 0, 0.0392157);">pin</code> (secret), and then stores the token in the secure storage. On successful completion, the User state will be set to <code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0.2em 0px; margin: 0px; border-radius: 3px; color: #333333; background-color: rgba(0, 0, 0, 0.0392157);">REGISTERED</code> and the method will return status <code style="box-sizing: border-box; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0.2em 0px; margin: 0px; border-radius: 3px; color: #333333; background-color: rgba(0, 0, 0, 0.0392157);">OK.</code></p>

<h2>Definition</h2>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt; background: #E2EFD9; margin-left: 0in; margin-right: 0in;">
<p class="CVXAPIDefinition"><b><span style="line-height: 105%; font-family: 'Courier New';">Status FinishRegistration(</span></b><span style="font-size: 12.0pt; line-height: 105%; font-family: 'Courier New';">User<b> <i>user, </i></b><i>String</i><b><i> pin</i>)</b></span></p>

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
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">The pincode that is set up by the user when they register</p>
</td>
</tr>
</tbody>
</table>
<h2>Return Values</h2>
<p class="MsoListParagraphCxSpFirst" style="margin-left: 0.5in; text-indent: -.25in; line-height: 105%;"><span style="font-family: Symbol;">·<span style="font: 7.0pt 'Times New Roman';">       </span></span><span class="CVXCodeinText"><span style="font-family: 'Courier New';">OK</span></span> – User is registered successfully and its status is set to <span class="CVXCodeinText"><span style="font-family: 'Courier New';">REGISTERED</span></span></p>
<p class="MsoListParagraphCxSpMiddle" style="margin-left: 0.5in; text-indent: -.25in; line-height: 105%;"><span style="font-family: Symbol;">·<span style="font: 7.0pt 'Times New Roman';">       </span></span><span class="CVXCodeinText"><span style="font-family: 'Courier New';">FLOW_ERROR</span></span> – The User object is not in the incorrect state (See <a href="#">Understanding User States</a>)</p>

<h2>Example</h2>
<p class="MsoNormal">The following code snippet creates a new User identity and, if the registration process is successful, finalizes it.</p>

<div style="border: solid windowtext 1.0pt; padding: 1.0pt 1.0pt 1.0pt 1.0pt;">
<pre class="computer_code">User user = sdk.MakeNewUser("me@miracl.org");
Status status = sdk.StartRegistration(user);

if (status.getStatusCode() != Status.Code.OK) {
   // handle error
}

switch (user.GetState())
{
    case State.STARTED_REGISTRATION:
        //
        // Wait for identity confirmation
        //
        break;        
    case State.ACTIVATED:
        break;
    default:
        // Something went wrong
}

status = sdk.ConfirmRegistration(user);

if (status.getStatusCode() != Status.Code.OK) {
   // handle error
}

String setupPin;

/* Read PIN from user */

status = sdk.FinishRegistration(user, setupPin);

if (status.getStatusCode() != Status.Code.OK) {
   // handle error
}</pre>
</div>
</div>