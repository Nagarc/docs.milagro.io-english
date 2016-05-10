---
currentMenu: milagro-mfa-logging-services
---

##Logging Services
<!-- MsoSubtitle -->

If you want to log the Services for troubleshooting, set the level of detail of logged messages for all the services to **Debug.**

You will need to restart the services.

To set the level of detail of logged messages to **Debug.**

<ol>
	<li>Set the&nbsp;<name style="font-style: italic;">logLevel</name>&nbsp;option of each service to&nbsp;<name style="font-style: italic;">Debug</name>.</li>
	<li>To restart the services:</li>
</ol>

<ul style="margin: 5px 0px 0px 40px; padding: 0px 0px 0px 12px; font-family: Verdana, Arial, Helvetica, sans-serif; font-size: 12px;">
	<li>Stop the services. Run the following command:&nbsp;<span class="CVXCodeinText" style="font-family: 'Courier New';"><em style="font-weight: inherit;">&lt;installation-folder&gt;</em>/mpin stop</span></li>
	<li>Start the services. Run the following command:&nbsp;<span class="CVXCodeinText" style="font-family: 'Courier New';">&nbsp;<em style="font-weight: inherit;">&lt;installation-folder&gt;</em>/mpin start</span></li>
</ul>
The log files reside in the following locations:

<ul style="margin: 5px 0px 0px 20px; padding: 0px 0px 0px 12px; font-family: Verdana, Arial, Helvetica, sans-serif; font-size: 12px;">
	<li><strong style="font-style: inherit;">RPS</strong>:&nbsp;<span class="CVXCodeinText" style="font-family: 'Courier New';"><em style="font-weight: inherit;">&lt;installation-folder&gt;</em>/mpin-&lt;X.X&gt;/servers/rps/rps.log</span></li>
	<li><strong style="font-style: inherit;">D-TA</strong>:&nbsp;<span class="CVXCodeinText" style="font-family: 'Courier New';"><em style="font-weight: inherit;">&lt;installation-folder&gt;</em>/mpin-&lt;X.X&gt;/servers/dta/dta.log</span></li>
</ul>

where <span class="CVXCodeinText" courier="" style="line-height: 19.2px;"><em style="font-weight: inherit;">installation-folder</em></span> is the installation folder and<span class="CVXCodeinText" courier="" style="line-height: 19.2px;"> X.X;</span>. is the version, e.g. 3.5.</p>
