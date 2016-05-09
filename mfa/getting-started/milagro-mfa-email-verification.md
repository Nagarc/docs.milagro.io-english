
<h1>Configuring the Demo Site to Use Email Verification</h1>

<ul>
	<li>Stop all the M-Pin services by running the following command in the M-Pin installation directory (default is /opt/mpin):
	<div class="computer_code">sudo ./mpin stop all</div>
	</li>
	<li>You need to edit /opt/mpin/config_demo.py.&nbsp;Scroll down to the &ldquo;# Verification emails settings&rdquo; section and amend/add the following parameters:
	<ul>
		<li>forceActivate &ndash; change this to &ldquo;False&rdquo;</li>
		<li>emailSubject &ndash; set this to the subject you wish your verification email to have. &nbsp; Default is &quot;M-Pin demo: New user activation&quot;</li>
		<li>emailSender &ndash; set this to the email address that you want the verification email to be sent from</li>
		<li>smtpServer &ndash; the name of the SMTP server you are using</li>
		<li>smtpPort &ndash; the port of the SMTP server you are using. &nbsp;Default is 25</li>
		<li>smtpUser &ndash; the username of your SMTP account</li>
		<li>smtpPassword &ndash; the password for the above account</li>
		<li>smtpUseTLS &ndash;&nbsp;change this to &quot;True&quot; and uncomment it to enable it.</li>
	</ul>
	</li>
	<li>Now start all the M-Pin services:
	<div class="computer_code">sudo ./mpin start all</div>
	</li>
	<li>Visit the following URL again:</li>
</ul>

<div class="computer_code">http://&lt;IP ADDRESS&gt;:8005</div>

<p>Your identity already exists in the browser, so the PIN pad will immediately ask you for your PIN to login:</p>



<div>
<ul style="margin: 5px 0px 0px 20px; padding: 0px 0px 0px 12px; font-family: Verdana, Arial, Helvetica, sans-serif; font-size: 12px;">
	<li>As we now want to show email verification working, instead of entering your PIN, click the menu icon at the top-right of the PIN pad to display the identity management screen:</li>
	<li>Click the pencil icon next to your identity, then&nbsp;<strong style="font-style: inherit;">Remove identity</strong></li>
</ul>



<ul style="margin: 5px 0px 0px 20px; padding: 0px 0px 0px 12px; font-family: Verdana, Arial, Helvetica, sans-serif; font-size: 12px;">
	<li>Confirm it by clicking&nbsp;<strong style="font-style: inherit;">Yes, Remove it.</strong></li>
</ul>


<p>You will see the following screen which prompts you to create a new identity.</p>

<ul>
	<li>Enter your email address, then&nbsp;<strong>Setup M-Pin</strong>. &nbsp;Now you will see the following screen:</li>
</ul>


<p>You should get an email with an activation link.&nbsp;</p>

<ul>
	<li>Click that activation link in your email to confirm your identity and the following screen will be displayed:</li>
</ul>


<ul>
	<li>Click <strong>Confirm and activat</strong>e to activate your identity. Once you have activated it, close this screen and go back to your&nbsp;Identity page and click <strong>I confirmed my email</strong>. You will get the following screen with your new email address indicating&nbsp;that it has been verified.</li>
</ul>


<p>Now just set up your pin and knock yourselves out!</p>

<p>&nbsp;</p>
</div>
