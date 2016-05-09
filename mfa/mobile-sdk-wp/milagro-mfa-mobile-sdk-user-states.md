<h1>Understanding User States</h1>

<h2>Summary</h2>

<p class="MsoNormal">This page explains briefly the various&nbsp;<span style="line-height: 19.2000007629395px;">states</span><span style="line-height: 19.2000007629395px;">&nbsp;of&nbsp;</span><span style="line-height: 1.6em;">the </span><span class="CVXCodeinText" style="line-height: 1.6em;"><span style="font-family:&quot;Courier New&quot;">User</span></span><span style="line-height: 1.6em;"> objects and when they are assigned. &nbsp;</span></p>

<h2>Overview</h2>

<p class="MsoNormal">A physical user of the Milagro Platform is represented by a <span class="CVXCodeinText"><span style="font-family:&quot;Courier New&quot;">User</span></span> object. The <span class="CVXCodeinText"><span style="font-family:&quot;Courier New&quot;">User</span></span> object supports several states showing&nbsp;the progress of the&nbsp;physical user through the stages of the registration process and their current permissions to access the system.</p>

<h2>User States</h2>

<p class="MsoNormal">The following table presents the states of the <span class="CVXCodeinText"><span style="font-family:&quot;Courier New&quot;">User</span></span> object in the chronological order in which they are normally&nbsp;assigned to a User:</p>

<table border="0" cellpadding="0" cellspacing="0" class="MsoNormalTable" style="margin-left:-.4pt;border-collapse:collapse">
	<tbody>
		<tr>
			<td style="border:solid windowtext 1.0pt;background:#F4F4F4;
  padding:0in 5.75pt 0in 5.75pt" valign="top">
			<p class="MsoNormal" style="margin-bottom:6.0pt;line-height:normal"><b><span style="color:#7F7F7F">State</span></b></p>
			</td>
			<td style="border:solid windowtext 1.0pt;border-left:none;
  background:#F4F4F4;padding:0in 5.4pt 0in 5.4pt" valign="top">
			<p class="MsoNormal" style="margin-bottom:6.0pt;line-height:normal"><b><span style="color:#7F7F7F">Description</span></b></p>
			</td>
		</tr>
		<tr>
			<td style="border:solid windowtext 1.0pt;border-top:none;
  padding:0in 5.75pt 0in 5.75pt" valign="top">
			<p class="CVXAPIDefinitionNoHighlight"><span style="font-family:&quot;Courier New&quot;">Invalid</span></p>
			</td>
			<td style="border-top:none;border-left:none;border-bottom:solid windowtext 1.0pt;
  border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt" valign="top">
			<p class="MsoNormal" style="margin-bottom:6.0pt;line-height:normal">The <span class="CVXCodeinText"><span style="font-family:&quot;Courier New&quot;">User</span></span> object has been created, but the User registration process has not started yet; any newly created Users are in an&nbsp;<span class="CVXCodeinText"><span style="font-family:&quot;Courier New&quot;">Invalid</span></span>&nbsp;state. To begin User registration, call the <span class="CVXCodeinText"><span style="font-family:
  &quot;Courier New&quot;">StartRegistration</span></span> method.&nbsp;The <span class="CVXCodeinText"><span style="font-family:&quot;Courier New&quot;">Invalid</span></span>&nbsp;state&nbsp;is also temporarily assigned to a User that has just been deleted until the User is physically deleted from memory.</p>
			</td>
		</tr>
		<tr>
			<td style="border:solid windowtext 1.0pt;border-top:none;
  padding:0in 5.75pt 0in 5.75pt" valign="top">
			<p class="CVXAPIDefinitionNoHighlight"><span style="font-family:&quot;Courier New&quot;">StartedRegistration</span></p>
			</td>
			<td style="border-top:none;border-left:none;border-bottom:solid windowtext 1.0pt;
  border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt" valign="top">
			<p class="MsoNormal" style="margin-bottom:6.0pt;line-height:normal">The <span class="CVXCodeinText"><span style="font-family:&quot;Courier New&quot;">User</span></span> object has been created, and the User registration process has started but not yet completed. The User&rsquo;s state&nbsp;remains <span class="CVXCodeinText"><span style="font-family:&quot;Courier New&quot;">StartedRegistration</span></span>&nbsp;until the<span class="CVXCodeinText"><span style="font-family:&quot;Courier New&quot;"> ConfirmRegistration</span></span> method is executed successfully. The <span class="CVXCodeinText"><span style="font-family:&quot;Courier New&quot;">StartedRegistration</span></span>&nbsp;state&nbsp;indicates that if the registration procedure needs to be done anew, you must use the <span class="CVXCodeinText"><span style="font-family:&quot;Courier New&quot;">RestartRegistration</span></span> method and not the <span class="CVXCodeinText"><span style="font-family:&quot;Courier New&quot;">StartRegistration</span></span> method. The <span class="CVXCodeinText"><span style="font-family:&quot;Courier New&quot;">StartRegistration</span></span> method will return <span class="CVXCodeinText"><span style="font-family:&quot;Courier New&quot;">FlowError</span></span> in this case).</p>
			</td>
		</tr>
		<tr>
			<td style="border:solid windowtext 1.0pt;border-top:none;
  padding:0in 5.75pt 0in 5.75pt" valign="top">
			<p class="CVXAPIDefinitionNoHighlight"><span style="font-family:&quot;Courier New&quot;">Registered</span></p>
			</td>
			<td style="border-top:none;border-left:none;border-bottom:solid windowtext 1.0pt;
  border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt" valign="top">
			<p class="MsoNormal" style="margin-bottom:6.0pt;line-height:normal">The User registration has completed successfully and the User can now authenticate to the M-Pin System.</p>
			</td>
		</tr>
		<tr>
			<td style="border:solid windowtext 1.0pt;border-top:none;
  padding:0in 5.75pt 0in 5.75pt" valign="top">
			<p class="CVXAPIDefinitionNoHighlight"><span style="font-family:&quot;Courier New&quot;">Activated</span></p>
			</td>
			<td style="border-top:none;border-left:none;border-bottom:solid windowtext 1.0pt;
  border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt" valign="top">
			<p class="MsoNormal" style="margin-bottom:6.0pt;line-height:normal">A temporary state&nbsp;for the special case in which a User can be registered without going through a verification process, e.g. in the case of a demo app. In this special case, the <span class="CVXCodeinText"><span style="font-family:&quot;Courier New&quot;">Activated</span></span>&nbsp;state is assigned to the User upon <span class="CVXCodeinText"><span style="font-family:&quot;Courier New&quot;">StartRegistration</span></span>, which allows the <span class="CVXCodeinText"><span style="font-family:&quot;Courier New&quot;">ConfirmRegistration</span></span> method to be called and to succeed without waiting for identity verification.</p>
			</td>
		</tr>
		<tr>
			<td style="border:solid windowtext 1.0pt;border-top:none;
  padding:0in 5.75pt 0in 5.75pt" valign="top">
			<p class="CVXAPIDefinitionNoHighlight"><span style="font-family:&quot;Courier New&quot;">Blocked</span></p>
			</td>
			<td style="border-top:none;border-left:none;border-bottom:solid windowtext 1.0pt;
  border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt" valign="top">
			<p class="MsoNormal" style="margin-bottom:6.0pt;line-height:normal">State assigned to a User upon reaching the maximum allowed number of unsuccessful login attempts (three&nbsp;by default, configurable through the <span class="CVXCodeinText"><span style="font-family:&quot;Courier New&quot;">maxInvalidLoginAttempts</span></span> option the in the RPS.) Once this state is set, the end-user is blocked and should re-register.</p>
			</td>
		</tr>
	</tbody>
</table>

<h2>The <span style="font-family:&quot;Courier New&quot;">User</span> Class</h2>

<p>The <span class="CVXCodeinText"><span style="font-family:&quot;Courier New&quot;">User</span></span> class is&nbsp;as follows:</p>

<pre class="computer_code" style="box-sizing: border-box; overflow: auto; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; font-stretch: normal; line-height: 1.45; padding: 16px; border-radius: 3px; word-wrap: normal; word-break: normal; color: rgb(51, 51, 51); background-color: rgb(247, 247, 247);">
<span class="pl-k" style="box-sizing: border-box; color: rgb(167, 29, 93);">public</span> <span class="pl-k" style="box-sizing: border-box; color: rgb(167, 29, 93);">class</span> <span class="pl-en" style="box-sizing: border-box; color: rgb(121, 93, 163);">User</span> : <span class="pl-k" style="box-sizing: border-box; color: rgb(167, 29, 93);">IDisposable</span>
{
    <span class="pl-k" style="box-sizing: border-box; color: rgb(167, 29, 93);">public</span> <span class="pl-k" style="box-sizing: border-box; color: rgb(167, 29, 93);">enum</span> <span class="pl-en" style="box-sizing: border-box; color: rgb(121, 93, 163);">State</span>
    {
        <span class="pl-c" style="box-sizing: border-box; color: rgb(150, 152, 150);">/// &lt;<span class="pl-ent" style="box-sizing: border-box; color: rgb(99, 163, 92);">summary</span>&gt;</span>
        <span class="pl-c" style="box-sizing: border-box; color: rgb(150, 152, 150);">/// The &lt;<span class="pl-ent" style="box-sizing: border-box; color: rgb(99, 163, 92);">see</span> <span class="pl-e" style="box-sizing: border-box; color: rgb(121, 93, 163);">cref</span>=<span class="pl-s" style="box-sizing: border-box; color: rgb(24, 54, 145);"><span class="pl-pds" style="box-sizing: border-box;">&quot;</span>User<span class="pl-pds" style="box-sizing: border-box;">&quot;</span></span>/&gt; object has been created, but the registration process has not started yet; any newly created Users are in Invalid state. (To begin User registration, call the StartRegistration method). The Invalid state is also temporarily assigned to a User that has just been deleted until the User is physically deleted from memory.</span>
        <span class="pl-c" style="box-sizing: border-box; color: rgb(150, 152, 150);">/// &lt;/<span class="pl-ent" style="box-sizing: border-box; color: rgb(99, 163, 92);">summary</span>&gt;</span>
        Invalid,
        <span class="pl-c" style="box-sizing: border-box; color: rgb(150, 152, 150);">/// &lt;<span class="pl-ent" style="box-sizing: border-box; color: rgb(99, 163, 92);">summary</span>&gt;</span>
        <span class="pl-c" style="box-sizing: border-box; color: rgb(150, 152, 150);">/// The &lt;<span class="pl-ent" style="box-sizing: border-box; color: rgb(99, 163, 92);">see</span> <span class="pl-e" style="box-sizing: border-box; color: rgb(121, 93, 163);">cref</span>=<span class="pl-s" style="box-sizing: border-box; color: rgb(24, 54, 145);"><span class="pl-pds" style="box-sizing: border-box;">&quot;</span>User<span class="pl-pds" style="box-sizing: border-box;">&quot;</span></span>/&gt; object has been created, and the User registration process has started but not yet completed. The User&rsquo;s state remains StartedRegistration until the FinishRegistration method is executed successfully. The StartedRegistration state indicates that if the registration procedure needs to be done again, you must use the RestartRegistration method and not the StartRegistration method (the StartRegistration method will return FlowError in this case.).</span>
        <span class="pl-c" style="box-sizing: border-box; color: rgb(150, 152, 150);">/// &lt;/<span class="pl-ent" style="box-sizing: border-box; color: rgb(99, 163, 92);">summary</span>&gt;</span>
        StartedRegistration,
        <span class="pl-c" style="box-sizing: border-box; color: rgb(150, 152, 150);">/// &lt;<span class="pl-ent" style="box-sizing: border-box; color: rgb(99, 163, 92);">summary</span>&gt;</span>
        <span class="pl-c" style="box-sizing: border-box; color: rgb(150, 152, 150);">///  A temporary state for a special case in which a &lt;<span class="pl-ent" style="box-sizing: border-box; color: rgb(99, 163, 92);">see</span> <span class="pl-e" style="box-sizing: border-box; color: rgb(121, 93, 163);">cref</span>=<span class="pl-s" style="box-sizing: border-box; color: rgb(24, 54, 145);"><span class="pl-pds" style="box-sizing: border-box;">&quot;</span>User<span class="pl-pds" style="box-sizing: border-box;">&quot;</span></span>/&gt; can be registered without going through a verification process, e.g. in case of a demo app. In this special case, the Activated state is assigned to the User upon StartRegistration, which allows the FinsihRegistration method to be called and to succeed without waiting for identity verification.</span>
        <span class="pl-c" style="box-sizing: border-box; color: rgb(150, 152, 150);">/// &lt;/<span class="pl-ent" style="box-sizing: border-box; color: rgb(99, 163, 92);">summary</span>&gt;</span>
        Activated,
        <span class="pl-c" style="box-sizing: border-box; color: rgb(150, 152, 150);">/// &lt;<span class="pl-ent" style="box-sizing: border-box; color: rgb(99, 163, 92);">summary</span>&gt;</span>
        <span class="pl-c" style="box-sizing: border-box; color: rgb(150, 152, 150);">/// The &lt;<span class="pl-ent" style="box-sizing: border-box; color: rgb(99, 163, 92);">see</span> <span class="pl-e" style="box-sizing: border-box; color: rgb(121, 93, 163);">cref</span>=<span class="pl-s" style="box-sizing: border-box; color: rgb(24, 54, 145);"><span class="pl-pds" style="box-sizing: border-box;">&quot;</span>User<span class="pl-pds" style="box-sizing: border-box;">&quot;</span></span>/&gt; registration has completed successfully and the User can now authenticate to the M-Pin System.</span>
        <span class="pl-c" style="box-sizing: border-box; color: rgb(150, 152, 150);">/// &lt;/<span class="pl-ent" style="box-sizing: border-box; color: rgb(99, 163, 92);">summary</span>&gt;</span>
        Registered,
        <span class="pl-c" style="box-sizing: border-box; color: rgb(150, 152, 150);">/// &lt;<span class="pl-ent" style="box-sizing: border-box; color: rgb(99, 163, 92);">summary</span>&gt;</span>
        <span class="pl-c" style="box-sizing: border-box; color: rgb(150, 152, 150);">/// A state assigned to a &lt;<span class="pl-ent" style="box-sizing: border-box; color: rgb(99, 163, 92);">see</span> <span class="pl-e" style="box-sizing: border-box; color: rgb(121, 93, 163);">cref</span>=<span class="pl-s" style="box-sizing: border-box; color: rgb(24, 54, 145);"><span class="pl-pds" style="box-sizing: border-box;">&quot;</span>User<span class="pl-pds" style="box-sizing: border-box;">&quot;</span></span>/&gt; upon reaching the maximum allowed number of unsuccessful login attempts (3 by default, configurable through the maxInvalidLoginAttempts option the in the RPS.) Once this state is set, the end-user is blocked and should re-register.</span>
        <span class="pl-c" style="box-sizing: border-box; color: rgb(150, 152, 150);">/// &lt;/<span class="pl-ent" style="box-sizing: border-box; color: rgb(99, 163, 92);">summary</span>&gt;</span>
        Blocked
    };

    <span class="pl-k" style="box-sizing: border-box; color: rgb(167, 29, 93);">public</span> String <span class="pl-en" style="box-sizing: border-box; color: rgb(121, 93, 163);">Id</span> { <span class="pl-k" style="box-sizing: border-box; color: rgb(167, 29, 93);">get</span> { ... } }
    <span class="pl-k" style="box-sizing: border-box; color: rgb(167, 29, 93);">public</span> State <span class="pl-en" style="box-sizing: border-box; color: rgb(121, 93, 163);">UserState</span> { <span class="pl-k" style="box-sizing: border-box; color: rgb(167, 29, 93);">get</span> { ... } }

    <span class="pl-k" style="box-sizing: border-box; color: rgb(167, 29, 93);">public</span> <span class="pl-k" style="box-sizing: border-box; color: rgb(167, 29, 93);">override</span> <span class="pl-k" style="box-sizing: border-box; color: rgb(167, 29, 93);">string</span> <span class="pl-en" style="box-sizing: border-box; color: rgb(121, 93, 163);">ToString</span>()
    {
        <span class="pl-k" style="box-sizing: border-box; color: rgb(167, 29, 93);">return</span> <span class="pl-c1" style="box-sizing: border-box; color: rgb(0, 134, 179);">this</span>.Id;
    }
    ....
}</pre>
