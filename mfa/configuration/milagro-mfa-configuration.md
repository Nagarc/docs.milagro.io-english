
<div class="info">For installation and initial setup information, see&nbsp;<a hqid="1688047" href="../getting-started/milagro-mfa-developer-guide.html" style="text-decoration: none; color: rgb(126, 206, 253); transition-duration: 0.3s;">Milagro MFA Developer Guide</a>.
<br>
<br />

<h2>Configuration Files Locations</h2>

<p style="margin: 10px 0px 20px; padding: 0px; line-height: 1.6em; color: rgb(62, 69, 76); font-family: Lato, sans-serif; font-size: 1.4em;">The default locations of the configuration files are given below:</p>

<ul style="margin: 5px 0px 0px 20px; padding: 0px 0px 0px 12px; font-family: Verdana, Arial, Helvetica, sans-serif; font-size: 12px;">
	<li><strong style="font-style: inherit;">RPS</strong>:&nbsp;<span class="CVXCodeinText" style="font-family: 'Courier New';"><em style="font-weight: inherit;">&lt;installation-folder&gt;</em>/config_rps.py</span></li>
	<li><strong style="font-style: inherit;">M-Pin D-TA</strong>:&nbsp;<span class="CVXCodeinText" style="font-family: 'Courier New';"><em style="font-weight: inherit;">&lt;installation-folder&gt;</em>/config_dta.py</span></li>
	<li><strong style="font-style: inherit;">Demo site configuration</strong>:&nbsp;<span class="CVXCodeinText" style="font-family: 'Courier New';"><em style="font-weight: inherit;">&lt;installation-folder&gt;</em>/config_demo.py</span></li>
</ul>



<h2>Restarting M-Pin Services</h2>


The following are the&nbsp;stop/start commands:</p>

<ul style="margin: 5px 0px 0px 20px; padding: 0px 0px 0px 12px; font-family: Verdana, Arial, Helvetica, sans-serif; font-size: 12px;">
	<li><strong style="font-style: inherit;">All Services</strong>:

	<ul style="margin: 5px 0px 0px 20px; padding: 0px 0px 0px 12px; list-style: disc;">
		<li>Stop:&nbsp;<span class="CVXCodeinText" style="font-family: 'Courier New';"><em style="font-weight: inherit;">&lt;installation-folder&gt;</em>/mpin stop</span></li>
		<li>Start:&nbsp;<span class="CVXCodeinText" style="font-family: 'Courier New';"><em style="font-weight: inherit;">&lt;installation-folder&gt;</em>/mpin start</span></li>
	</ul>
	</li>
	<li><strong style="font-style: inherit;">RPS</strong>:
	<ul style="margin: 5px 0px 0px 20px; padding: 0px 0px 0px 12px; list-style: disc;">
		<li>Stop:&nbsp;<span class="CVXCodeinText" style="font-family: 'Courier New';"><em style="font-weight: inherit;">&lt;installation-folder&gt;</em>/mpin stop rps</span></li>
		<li>Start:&nbsp;<span class="CVXCodeinText" style="font-family: 'Courier New';"><em style="font-weight: inherit;">&lt;installation-folder&gt;</em>/mpin start rps</span></li>
	</ul>
	</li>
	<li><strong style="font-style: inherit;">D-TA</strong>:
	<ul style="margin: 5px 0px 0px 20px; padding: 0px 0px 0px 12px; list-style: disc;">
		<li>Stop:&nbsp;<span class="CVXCodeinText" style="font-family: 'Courier New';"><em style="font-weight: inherit;">&lt;installation-folder&gt;</em>/mpin stop dta</span></li>
		<li>Start:&nbsp;<span class="CVXCodeinText" style="font-family: 'Courier New';"><em style="font-weight: inherit;">&lt;installation-folder&gt;</em>/mpin start dta</span></li>
	</ul>
	</li>
</ul>

<h2><span class="CVXCodeinText" style="font-family: 'Courier New';">​</span>Configuration Options Information Location</h2>

<p>Click the links below for more information on this:</p>

<ul style="margin: 5px 0px 0px 20px; padding: 0px 0px 0px 12px; font-family: Verdana, Arial, Helvetica, sans-serif; font-size: 12px;">
	<li><a href="../configuration/milagro-mfa-rps-configuration.html" style="text-decoration: none; color: rgb(126, 206, 253); transition-duration: 0.3s;">RPS Configuration Options Reference</a></li>
	<li><a href="../configuration/milagro-mfa-d-ta-configuration.html" style="text-decoration: none; color: rgb(126, 206, 253); transition-duration: 0.3s;">D-TA (Customer) Configuration Options Reference</a></li>
</ul>
