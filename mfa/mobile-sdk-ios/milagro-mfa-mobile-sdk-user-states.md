---
currentMenu: milagro-mfa-mobile-sdk-user-states-ios
---

<h1>Understanding User States</h1>
<h2>Overview</h2>
<p class="MsoNormal">This page explains briefly what <span style="line-height: 19.2000007629395px;">states</span><span style="line-height: 19.2000007629395px;"> </span><span style="line-height: 1.6em;">the </span><span class="CVXCodeinText" style="line-height: 1.6em;"><span style="font-family: 'Courier New';">User</span></span><span style="line-height: 1.6em;"> objects are in and when they are assigned. </span>A physical user of the Milagro MFA authentication platform is represented by a <span class="CVXCodeinText"><span style="font-family: 'Courier New';">User</span></span> object. The <span class="CVXCodeinText"><span style="font-family: 'Courier New';">User</span></span> object supports several states which shows the progress of the physical user through the stages of the registration process and their current permissions to access the system.</p>

<h2>User States</h2>
<p class="MsoNormal">The following table presents the states of the <span class="CVXCodeinText"><span style="font-family: 'Courier New';">User</span></span> object in the chronological order in which they normally are assigned to a User.</p>

<table class="MsoNormalTable" style="margin-left: -.4pt; border-collapse: collapse;" border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td style="border: solid windowtext 1.0pt; background: #F4F4F4; padding: 0in 5.75pt 0in 5.75pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;"><b><span style="color: #7f7f7f;">State</span></b></p>
</td>
<td style="border: solid windowtext 1.0pt; border-left: none; background: #F4F4F4; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;"><b><span style="color: #7f7f7f;">Description</span></b></p>
</td>
</tr>
<tr>
<td style="border: solid windowtext 1.0pt; border-top: none; padding: 0in 5.75pt 0in 5.75pt;" valign="top">
<p class="CVXAPIDefinitionNoHighlight"><span style="font-family: 'Courier New';">INVALID</span></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">The <span class="CVXCodeinText"><span style="font-family: 'Courier New';">User</span></span> object has been created, but the User registration process has not started yet; any newly created Users are in an <span class="CVXCodeinText"><span style="font-family: 'Courier New';">INVALID</span></span> state. (To begin User registration, call the <span class="CVXCodeinText"><span style="font-family: 'Courier New';">StartRegistration</span></span> method.) The <span class="CVXCodeinText"><span style="font-family: 'Courier New';">INVALID</span></span> state is also temporarily assigned to a User that has just been deleted until the User is physically deleted from memory.</p>
</td>
</tr>
<tr>
<td style="border: solid windowtext 1.0pt; border-top: none; padding: 0in 5.75pt 0in 5.75pt;" valign="top">
<p class="CVXAPIDefinitionNoHighlight"><span style="font-family: 'Courier New';">STARTED_REGISTRATION</span></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">The <span class="CVXCodeinText"><span style="font-family: 'Courier New';">User</span></span> object has been created, and the User registration process has started but not yet completed. The User’s state remains <span class="CVXCodeinText"><span style="font-family: 'Courier New';">STARTED_REGISTRATION</span></span> until the<span class="CVXCodeinText"><span style="font-family: 'Courier New';"> ConfirmRegistration</span></span> method is executed successfully. The <span class="CVXCodeinText"><span style="font-family: 'Courier New';">STARTED_REGISTRATION</span></span> state indicates that if the registration procedure needs to be done anew, you must use the <span class="CVXCodeinText"><span style="font-family: 'Courier New';">RestartRegistration</span></span> method and not the <span class="CVXCodeinText"><span style="font-family: 'Courier New';">StartRegistration</span></span> method (The <span class="CVXCodeinText"><span style="font-family: 'Courier New';">StartRegistration</span></span> method will return  a <span class="CVXCodeinText"><span style="font-family: 'Courier New';">FLOW_ERROR</span></span> in this case).</p>
</td>
</tr>
<tr>
<td style="border: solid windowtext 1.0pt; border-top: none; padding: 0in 5.75pt 0in 5.75pt;" valign="top">
<p class="CVXAPIDefinitionNoHighlight"><span style="font-family: 'Courier New';">REGISTERED</span></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">The User registration has completed successfully and the User can now authenticate to the M-Pin System.</p>
</td>
</tr>
<tr>
<td style="border: solid windowtext 1.0pt; border-top: none; padding: 0in 5.75pt 0in 5.75pt;" valign="top">
<p class="CVXAPIDefinitionNoHighlight"><span style="font-family: 'Courier New';">ACTIVATED</span></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">Temporary state for the special case in which a User can be registered without going through a verification process, e.g. in case of a demo app. In this special case, the <span class="CVXCodeinText"><span style="font-family: 'Courier New';">ACTIVATED</span></span> state is assigned to the User upon <span class="CVXCodeinText"><span style="font-family: 'Courier New';">StartRegistration</span></span>, which allows the <span class="CVXCodeinText"><span style="font-family: 'Courier New';">ConfirmRegistration</span></span> method to be called and to succeed without waiting for identity verification.</p>
</td>
</tr>
<tr>
<td style="border: solid windowtext 1.0pt; border-top: none; padding: 0in 5.75pt 0in 5.75pt;" valign="top">
<p class="CVXAPIDefinitionNoHighlight"><span style="font-family: 'Courier New';">BLOCKED</span></p>
</td>
<td style="border-top: none; border-left: none; border-bottom: solid windowtext 1.0pt; border-right: solid windowtext 1.0pt; padding: 0in 5.4pt 0in 5.4pt;" valign="top">
<p class="MsoNormal" style="margin-bottom: 6.0pt; line-height: normal;">State assigned to a User upon reaching the maximum allowed number of unsuccessful login attempts (3 by default, configurable through the <span class="CVXCodeinText"><span style="font-family: 'Courier New';">maxInvalidLoginAttempts</span></span> option the in the RPS.) Once this state is set, the end-user is blocked and should re-register.</p>
</td>
</tr>
</tbody>
</table>
<h2>The <span style="font-family: 'Courier New';">User</span> Class</h2>
The <span class="CVXCodeinText"><span style="font-family: 'Courier New';">User</span></span> class looks as follows:
<p class="CVXCodeExample" style="margin-left: 40px;"><span style="font-size: 11.0pt; line-height: 105%; font-family: 'Courier New';">typedef NS_ENUM(NSInteger, UserState)</span></p>
{

INVALID,

STARTED_REGISTRATION,

REGISTERED,

ACTIVATED,

BLOCKED

};

@protocol IUser

-(NSString*) getIdentity;

-(UserState) getState;

@end