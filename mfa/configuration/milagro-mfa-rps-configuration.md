---
currentMenu: milagro-mfa-rps-configuration
---

#RPS Configuration Options Reference

<p style="margin: 0px; padding: 0px; line-height: 1.6em; font-family: Verdana, Arial, Helvetica, sans-serif; font-size: 12px;">By default, the configuration file for the Relying Party Service (RPS) resides in:<br />
<span class="CVXCodeinText" style="font-family: 'Courier New';"><em style="font-weight: inherit;">&lt;installation-folder&gt;</em>/config_rps.py</span></p>

<p style="margin: 0px; padding: 0px; line-height: 1.6em; font-family: Verdana, Arial, Helvetica, sans-serif; font-size: 12px;">The table below lists alphabetically the available RPS configuration options. An option is considered required if its absence from the configuration file produces a system error.</p>

<table style="border-collapse: collapse; border-spacing: 0px; border: 1px dotted rgb(211, 211, 211); color: rgb(0, 0, 0); font-family: Verdana, Arial, Helvetica, sans-serif; font-size: 12px;">
	<tbody>
		<tr id="HadACAyPcW6">
			<td id="HadACAMhcUo" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><br />
			<strong style="font-style: inherit;">Option Name</strong></td>
			<td id="HadACA3AAyZ" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><br />
			<strong style="font-style: inherit;">Option Type</strong></td>
			<td id="HadACAF5wv3" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><br />
			<strong style="font-style: inherit;">Option Description</strong></td>
		</tr>
		<tr>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong style="font-style: inherit;">address</strong></td>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Optional</td>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">IP address of the local interface on which the service is listening.&nbsp;A value of&nbsp;<em style="font-weight: inherit;">0.0.0.0</em>&nbsp;means listening on all interfaces.&nbsp;The default listening interface is&nbsp;<em style="font-weight: inherit;">127.0.0.1</em>.</td>
		</tr>
		<tr id="HadACAbuejF">
			<td id="HadACAKGzkN" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong style="font-style: inherit;">accessNumberExpireSeconds</strong></td>
			<td id="HadACA3sGUu" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Optional</td>
			<td id="HadACAL3oVN" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Expatriation period in seconds for the Access Number which is displayed in the Browser PIN Pad for Mobile authentication. The default is&nbsp;<em style="font-weight: inherit;">60</em>.</td>
		</tr>
		<tr>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong>accessNumberExtendValiditySeconds</strong></td>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Optional</td>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Expatriation period in seconds for the Access Number (on top of accessNumberExpireSeconds). The default is 5.</td>
		</tr>
		<tr>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong>accessNumberUseCheckSum</strong></td>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Optional</td>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">When&nbsp;<em style="font-weight: inherit;">True</em>, the integrity of the one-time password is protected with a checksum. The default is&nbsp;<em style="font-weight: inherit;">True</em>.</td>
		</tr>
		<tr id="HadACAq0X4f">
			<td id="HadACAACue2" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong style="font-style: inherit;">address</strong></td>
			<td id="HadACAQUTsw" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Optional</td>
			<td id="HadACAoDzAs" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">IP address of the local interface on which the service is listening. A value of&nbsp;<em style="font-weight: inherit;">0.0.0.0</em>&nbsp;means listening on all interfaces. The default listening interface is 127.0.0.1.</td>
		</tr>
		<tr>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong>allowOrigin</strong></td>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Optional</td>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Sets the Access-Control-Allow-Origin header. The default is &#39;<em style="font-weight: inherit;">*&#39;</em>.</td>
		</tr>
		<tr>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong>cacheTimePermits</strong></td>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Optional</td>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">When&nbsp;<em style="font-weight: inherit;">True</em>, the M-Pin Time Permits issued for the Client by D-TAs are stored in the system cache. This allows your M-Pin Core System to take advantage of pre-generated Time Permits, which speeds up operations. When&nbsp;<em style="font-weight: inherit;">False</em>, the newly requested Time Permits are each time generated by the D-TA (instead of being retrieved from the cache.)&nbsp;The default setting is&nbsp;<em style="font-weight: inherit;">True</em>.</td>
		</tr>
		<tr>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong>configFile</strong></td>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Optional</td>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Path and name of the RPS config file. You can create as many configurations as you want, store each as a separate file, and use the&nbsp;configFile option to switch configurations as needed.&nbsp;The default path and filename is&nbsp;<em style="font-weight: inherit;">&lt;installation-folder&gt;</em>/config_rps.py.</td>
		</tr>
		<tr id="HadACARpiTF">
			<td id="HadACAsHna0" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong style="font-style: inherit;">credentialsFile</strong></td>
			<td id="HadACAu45Hh" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Optional</td>
			<td id="HadACAcWMod" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Credentials File location. The Credentials File is a JSON file containing the credentials with which the Relying Party Service (RPS) authenticates the Relying Party Application (RPA). It is issued upon RPA&rsquo;s registration in the M-Pin System. The default location of the file is the directory in which the M-Pin System is installed. Example: /opt/mpin/credentials.json</td>
		</tr>
		<tr id="HadACA6HCmr">
			<td id="HadACALVXp2" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong style="font-style: inherit;">DTALocalURL</strong></td>
			<td id="HadACAsZBME" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Required</td>
			<td id="HadACA5A1mJ" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Base URL for making requests (by the RPS) to the Customer D-TA. The default is http://127.0.0.1:8001.</td>
		</tr>
		<tr>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong>dynamicOptionsURL</strong></td>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Optional</td>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">URL from which the new set of the RPS configuration options is returned. The URL is resolved when you need to change the RPS settings dynamically (when the M-Pin Core system is operational).<br />
			<br />
			The following is a list of the&nbsp;RPS options that can be configured&nbsp;dynamically:<br />
			&nbsp;&nbsp;&nbsp;&bull;&nbsp;<strong style="font-style: inherit;">syncTime</strong><br />
			&nbsp;&nbsp;&nbsp;&bull;&nbsp;<strong style="font-style: inherit;">timePeriod</strong><br />
			&nbsp;&nbsp;&nbsp;&bull;&nbsp;<strong style="font-style: inherit;">mobileConfig</strong><br />
			&nbsp;&nbsp;&nbsp;&bull;&nbsp;<strong style="font-style: inherit;">mobileUseNative</strong></td>
		</tr>
		<tr>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong>fileStorageLocation</strong></td>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Conditional, Required</td>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Path and location of the JSON file to be used as a system storage by the RPS if file storage is used. Required if the&nbsp;<strong style="font-style: inherit;">storage</strong>&nbsp;option is set to&nbsp;<em style="font-weight: inherit;">json</em>.</td>
		</tr>
		<tr>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong style="font-style: inherit;">EntropySources</strong></td>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Optional</td>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Entropy source for the service together with the entropy size. The service needs 100 bytes of entropy for performing its authentication function. Entropy retrieval can optionally be distributed among several different sources. For each source there is&nbsp;plugin module with the same name as the source. Further entropy source plugins can be developed to accommodate other sources. The entropy plugins that are supported &quot;out of the box&quot; are the following:<br />
			<br />
			&nbsp;&nbsp;&nbsp;&bull;&nbsp;<em style="font-weight: inherit;">dev_random</em>&nbsp;&ndash; reads from&nbsp;the local /dev/random device. It is a good source but might be slow, especially on a virtual machine.<br />
			<br />
			&nbsp;&nbsp;&nbsp;&bull;&nbsp;<em style="font-weight: inherit;">dev_urandom</em>&nbsp;&ndash; reads from the local /dev/urandom device. This source is not as good as the local /dev/random device but still reliable enough and doesn&#39;t suffer from performance issues.<br />
			<br />
			&nbsp;&nbsp;&nbsp;&bull;&nbsp;<em style="font-weight: inherit;">MIRACL</em>&nbsp;&ndash; reads from the MIRACL entropy server.<br />
			<br />
			The following example configures distributed retrieval of 40 bytes of entropy from the MIRACL server and 60 bytes from the local /dev/random source:&nbsp;<em style="font-weight: inherit;">MIRACL:40,dev_urandom:60</em>.<br />
			<br />
			The default setting is&nbsp;<em style="font-weight: inherit;">dev_urandom:100</em>.</td>
		</tr>
		<tr id="HadACAyhnLH">
			<td id="HadACAvgK1W" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong style="font-style: inherit;">logLevel</strong></td>
			<td id="HadACARGJZ4" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Optional</td>
			<td id="HadACANE0yk" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Level of detail for the messages logged to the service&#39;s log file. Increasing the level of detail might be necessary for the development/integration of the Relying Party Application (RPA). The valid settings (in increasing level of detail) are&nbsp;<em style="font-weight: inherit;">ERROR</em>,&nbsp;<em style="font-weight: inherit;">WARN</em>,&nbsp;<em style="font-weight: inherit;">INFO</em>,&nbsp;<em style="font-weight: inherit;">DEBUG</em>. The default is&nbsp;<em style="font-weight: inherit;">ERROR</em>.</td>
		</tr>
		<tr id="HadACAKMm2B">
			<td id="HadACAiFcDl" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong style="font-style: inherit;">logoutURL</strong></td>
			<td id="HadACAVYLFa" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Required</td>
			<td id="HadACARNEGo" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Logout URL for the Mobile App; enables logging out end-users remotely. The logout functionality is entirely customer-implemented as it depends on the RPA&#39;s session management mechanism and, therefore, is typically an RPA endpoint. If provided, in order to log-out the end-user, the Mobile App will make a request to this endpoint. Example setting: http://127.0.0.1:8005/logout.</td>
		</tr>
		<tr id="HadACAtopbz">
			<td id="HadACAuXXea" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong style="font-style: inherit;">maxInvalidLoginAttempts</strong></td>
			<td id="HadACAhcduL" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Optional</td>
			<td id="HadACAIHSdQ" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Maximum number of allowed invalid login attempts. Once this limit is reached, the end-user is blocked and should re-register. (The counter of the invalid attempts is reset after a successful login.) The default is 3.</td>
		</tr>
		<tr>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong>mobileUseNative</strong></td>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Optional</td>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">When&nbsp;<em style="font-weight: inherit;">True</em>, the native Mobile App is used; when&nbsp;<em style="font-weight: inherit;">False</em>&nbsp;&ndash;&nbsp;the Javascript client.&nbsp;The default is&nbsp;<em style="font-weight: inherit;">False</em>.</td>
		</tr>
		<tr id="HadACA1yCtC">
			<td id="HadACAmk6Gv" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong style="font-style: inherit;">port</strong></td>
			<td id="HadACAfIfRJ" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Optional</td>
			<td id="HadACAEQZlz" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Port on which the service is listening. The default port is 8011.</td>
		</tr>
		<tr id="HadACAlynsb">
			<td id="HadACA7Mewz" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong style="font-style: inherit;">redisDB</strong></td>
			<td id="HadACA10PW2" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Conditional, Required</td>
			<td id="HadACASrGXj" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Redis database to use, indicated as an integer. Example:&nbsp;<em style="font-weight: inherit;">0</em>.&nbsp;<br />
			Required if the&nbsp;<strong style="font-style: inherit;">storage</strong>&nbsp;option is set to&nbsp;<em style="font-weight: inherit;">redis</em>.</td>
		</tr>
		<tr id="HadACAEW6Zt">
			<td id="HadACAHobe8" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong style="font-style: inherit;">redisHost</strong></td>
			<td id="HadACAXeKX3" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Conditional, Required</td>
			<td id="HadACAk8bun" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">IP address of the Redis storage. Example:&nbsp;<em style="font-weight: inherit;">127.0.0.1</em>.&nbsp;<br />
			Required if the&nbsp;<strong style="font-style: inherit;">storage</strong>&nbsp;option is set to&nbsp;<em style="font-weight: inherit;">redis</em>.</td>
		</tr>
		<tr id="HadACAWAxWo">
			<td id="HadACA07sX6" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong style="font-style: inherit;">redisPassword</strong></td>
			<td id="HadACAKFXtr" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Conditional, Required</td>
			<td id="HadACA78XzI" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Password for the Redis connection. For no password, set to&nbsp;<em style="font-weight: inherit;">None</em>.&nbsp;<br />
			Required if the&nbsp;<strong style="font-style: inherit;">storage</strong>&nbsp;option is set to&nbsp;<em style="font-weight: inherit;">redis</em>.</td>
		</tr>
		<tr id="HadACAS7FA9">
			<td id="HadACAbD4wn" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong style="font-style: inherit;">redisPort</strong></td>
			<td id="HadACAAT36Q" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Conditional, Required</td>
			<td id="HadACAekTVf" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Communication port of the Redis storage. Example: 6379.&nbsp;<br />
			Required if the&nbsp;<strong style="font-style: inherit;">storage</strong>&nbsp;option is set to&nbsp;<em style="font-weight: inherit;">redis</em>.</td>
		</tr>
		<tr id="HadACAs5MTz">
			<td id="HadACAojB46" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong style="font-style: inherit;">redisPrefix</strong></td>
			<td id="HadACAQYbpb" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Conditional, Required</td>
			<td id="HadACADRKp4" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Data transfer prefix indicating that the element should be routed to the Redis storage. The default is&nbsp;<em style="font-weight: inherit;">mpin</em>.&nbsp;<br />
			Required if the&nbsp;<strong style="font-style: inherit;">storage</strong>&nbsp;option is set to&nbsp;<em style="font-weight: inherit;">redis</em>.</td>
		</tr>
		<tr id="HadACAU2KPi">
			<td id="HadACAJTS2e" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong style="font-style: inherit;">RegisterForwardUserHeaders</strong></td>
			<td id="HadACAqAFns" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Required</td>
			<td id="HadACAu2lGN" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">List of headers to be forwarded. Used together with the RPAVerifyUserURL property to verify whether the end-user hasn&rsquo;t already been authenticated through another authentication platform (if multiple authentication are supported by your system). The list is in CSV format. To disable headers forwarding, leave an empty string (default); to forward all headers, use the star character(*).</td>
		</tr>
		<tr>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong>RequestOTP</strong></td>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Optional</td>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">When&nbsp;<em style="font-weight: inherit;">True</em>, two-factor authentication is enabled (in the form of on-time password send to the user&#39;s mobile device) as an option. This allows end-users to choose whether to authenticate with their M-Pin only or use&nbsp;two-factor authentication.&nbsp;The default setting is&nbsp;<em style="font-weight: inherit;">False</em>.</td>
		</tr>
		<tr id="HadACAMoj7x">
			<td id="HadACArNQQe" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong style="font-style: inherit;">RPAAuthenticateUserURL</strong></td>
			<td id="HadACAHR2WB" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Required</td>
			<td id="HadACAl543Z" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Endpoint of the Relying Party Application (RPA) for end-user authentication validation. Example: /mpinAuthenticate.</td>
		</tr>
		<tr id="HadACAwI5Wg">
			<td id="HadACAyTP1n" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong style="font-style: inherit;">RPAPermitUserURL</strong></td>
			<td id="HadACA3kXKH" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Required</td>
			<td id="HadACAP9FCL" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Endpoint of the Relying Party Application (RPA) for end-user revocation. Example: http://192.168.10.138:8005/mpinPermitUser.</td>
		</tr>
		<tr id="HadACAfkH6b">
			<td id="HadACAcvs1B" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong style="font-style: inherit;">RPAVerifyUserURL</strong></td>
			<td id="HadACA90xSn" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Required</td>
			<td id="HadACARtTGL" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Endpoint of the Relying Party Application (RPA) for end-user identity verification. Example: http://192.168.10.138:8005/mpinVerify.</td>
		</tr>
		<tr id="HadACAZmBLu">
			<td id="HadACA5zhAL" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong style="font-style: inherit;">rpsBaseURL</strong></td>
			<td id="HadACAqWL6Y" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Required</td>
			<td id="HadACAoC6TR" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Base URL of the RPS service. This URL is used to assemble the correct URLs for the client settings provided to the Client. The default is http://127.0.0.1:8011.</td>
		</tr>
		<tr id="HadACAodyWy">
			<td id="HadACAie14p" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong style="font-style: inherit;">rpsPrefix</strong></td>
			<td id="HadACAChZam" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Optional</td>
			<td id="HadACAXPzNF" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Prefix for the &quot;external&quot; requests to the RPS. (&ldquo;External&rdquo; requests are those that come from the Client to the RPA and are supposed to be re-routed by the RPA to the RPS.) The Proxy must be configured to forward requests with this prefix to the RPS. The default setting is&nbsp;<em style="font-weight: inherit;">rps</em>.</td>
		</tr>
		<tr>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong>seedValueLength</strong></td>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Optional</td>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Length (in number of characters) of the seed for the Client. (Used for entropy generation.) The default is&nbsp;<em style="font-weight: inherit;">100</em>.</td>
		</tr>
		<tr id="HadACA4pcDe">
			<td id="HadACAz3aCM" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong style="font-style: inherit;">setDeviceName</strong></td>
			<td id="HadACAWhKK0" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Optional</td>
			<td id="HadACAinZn2" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">When&nbsp;<em style="font-weight: inherit;">True</em>, the Client allows setting of a Device Name together with the end-user Identity. This setting is sent to the Client through the client settings.<br />
			<br />
			If&nbsp;<em style="font-weight: inherit;">True</em>, the Client will obtain a default device name and will display it to the end-user who will be able to optionally modify it. The device name is then sent to the RPS together with the registration request and the RPS feeds it to the RPA within the end-user verification request. The RPA uses this information to map end-users to their devices (i.e. to map M-Pin IDs to Device Names).<br />
			<br />
			The default setting is&nbsp;<em style="font-weight: inherit;">False</em>.</td>
		</tr>
		<tr id="HadACAMviJQ">
			<td id="HadACAB4jYY" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong style="font-style: inherit;">storage</strong></td>
			<td id="HadACATlBi4" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Optional</td>
			<td id="HadACAoHRWL" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">
			<p><span style="font-family: Verdana, Arial, Helvetica, sans-serif; font-size: 12px; background-color: rgb(255, 255, 255);">Indicates the kind of Storage used by the RPS. (The RPS uses the Storage to keep Time Permits and some temporary authentication tokens). The valid settings are:</span></p>

			<ul>
				<li><span style="font-family: Verdana, Arial, Helvetica, sans-serif; font-size: 12px; background-color: rgb(255, 255, 255);"><em>json</em> - the RPS stores its content in a JSON file. (The file path and name are specified in the <strong>fileStorageLocation</strong> option).&nbsp;</span></li>
				<li><span style="font-family: Verdana, Arial, Helvetica, sans-serif; font-size: 12px; background-color: rgb(255, 255, 255);"><em>memory</em> (default) - the RPS stores its contents in the machine&#39;s RAM.</span></li>
				<li><span style="font-family: Verdana, Arial, Helvetica, sans-serif; font-size: 12px; background-color: rgb(255, 255, 255);"><em>redis</em> <span style="font-family: Verdana, Arial, Helvetica, sans-serif; font-size: 12px; background-color: rgb(255, 255, 255);">(recommended) - the RPS stores its content in a Redis database. (Redis storage provides solutions suitable for High Availability Deployments and for scaling up an existing deployment). This setting makes all options beginning with <strong>redis</strong>, required.&nbsp;</span></span></li>
			</ul>
			</td>
		</tr>
		<tr>
			<td id="HadACAB4jYY" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong style="font-style: inherit;">syncTime</strong></td>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Optional</td>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">When&nbsp;<em style="font-weight: inherit;">True</em>, the service&nbsp;syncs its time&nbsp;with the MIRACL&#39;s servers; if syncronization fails, the an attemp will be made each 5 seconds until success is achievd. When&nbsp;<em style="font-weight: inherit;">False</em>&nbsp;(recommended), this time synchronization is disabled and the service will rely on the system time.&nbsp;The default is&nbsp;<em style="font-weight: inherit;">False.</em>
			<div class="warning" style="margin: 0px; padding: 5px 30px; line-height: 1.6em; background: url(&quot;/images/warning.png&quot;) 5px 50% no-repeat rgb(255, 237, 235);">Time synchronization is needed to perform time-based verification. Therefore, if you disable the syncing of the service with the&nbsp;MIRACL&#39;s servers, you should be then syncing your system with an NTP server to ensure that correct and precise system time is&nbsp;maintained.</div>
			</td>
		</tr>
		<tr>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong>timePeriod</strong></td>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Conditional, Required</td>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Time interval (in ms) at which the service syncs with the MIRACL&#39;s time servers. Required if the&nbsp;<strong style="font-style: inherit;">syncTime</strong>&nbsp;option is enabled. The default setting is&nbsp;<em style="font-weight: inherit;">86400000</em>, which amounts to one synchronization a day.</td>
		</tr>
		<tr>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong>VerifyUserExpireSeconds</strong></td>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Optional</td>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Time interval (in seconds) after which the User verification expires due to inactivity of the User.&nbsp;The default is&nbsp;<em style="font-weight: inherit;">3600&nbsp;</em>(1 hour).</td>
		</tr>
		<tr>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong>waitForLoginResult</strong></td>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Optional</td>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">When&nbsp;<em style="font-weight: inherit; line-height: 19.2px;">True</em>, the Mobile App will wait for browser login confirmation before showing the Done/Logout button. When&nbsp;<em style="font-weight: inherit;">False</em>, the&nbsp;the Done/Logout button is displayed irrespective of the User&#39;s.</td>
		</tr>
		<tr>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong style="font-style: inherit;">certivoxServerSecret parameter</strong></td>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Optional</td>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><a hqid="1658592" href="#" style="color: rgb(39, 137, 177); text-decoration: none;">M-Pin Core Configuration - Manually Applying a Server Secret</a></td>
		</tr>
	</tbody>
</table>
