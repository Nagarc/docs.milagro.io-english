<h1>D-TA Configuration Options Reference</h1>
<!-- MsoSubtitle -->

<p id="HadACAdGJ3N" style="margin: 0px; padding: 0px; line-height: 1.6em; font-family: Verdana, Arial, Helvetica, sans-serif; font-size: 12px;">The configuration file for the Customer D-TA service resides in:<br />
<span class="CVXCodeinText" style="font-family: 'Courier New';"><em style="font-weight: inherit;">&lt;installation-folder&gt;</em>/config_dta.py</span></p>

<p style="margin: 0px; padding: 0px; line-height: 1.6em; font-family: Verdana, Arial, Helvetica, sans-serif; font-size: 12px;"></p>

<p id="HadACAIhWUC" style="margin: 0px; padding: 0px; line-height: 1.6em; font-family: Verdana, Arial, Helvetica, sans-serif; font-size: 12px;">The table below lists alphabetically the available Customer D-TA configuration options.&nbsp;&nbsp;An option is considered required if its absence from the configuration file produces a system error.</p>

<table class="confluenceTable" style="border-collapse: collapse; border-spacing: 0px; border: 1px dotted rgb(211, 211, 211); color: rgb(0, 0, 0); font-family: Verdana, Arial, Helvetica, sans-serif; font-size: 12px;">
	<tbody>
		<tr>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong style="font-style: inherit;">Option Name</strong></td>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong style="font-style: inherit;">Option Type</strong></td>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong style="font-style: inherit;">Option Description</strong></td>
		</tr>
		<tr>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong style="font-style: inherit;">address</strong></td>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Required</td>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">IP address of the local interface on which the service is listening. A value of&nbsp;<em style="font-weight: inherit;">0.0.0.0</em>&nbsp;means listening on all interfaces. The default listening interface is 127.0.0.1.</td>
		</tr>
		<tr>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong style="font-style: inherit;">backup</strong></td>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Optional</td>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">When&nbsp;<em style="font-weight: inherit;">True</em>, the Customer D-TA Master Key Share is saved to a non-volatile memory storage. Not saving the Master Key Share to a non-volatile storage provides better security but entails in re-setting the Master Key each time the D-TA is restarted resulting in revocation of all end-users&#39; credentials (i.e. all users will have to register anew). The default setting is&nbsp;<em style="font-weight: inherit;">True</em>.</td>
		</tr>
		<tr>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong style="font-style: inherit;">backupFile</strong></td>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Conditional, Required</td>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Path and name of the file to which the Master Secret is to be saved.&nbsp;<br class="atl-forced-newline" />
			Required if the&nbsp;<strong style="font-style: inherit;">backup</strong>&nbsp;option is set to&nbsp;<em style="font-weight: inherit;">False</em>. The default is&nbsp;<em style="font-weight: inherit;">&lt;installation-folder&gt;</em>/backup.json.</td>
		</tr>
		<tr>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong>configFile</strong></td>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Required</td>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Path and name of the D-TA config file. You can create as many configurations as you want, store each as a separate file, and use the&nbsp;configFile option to switch configurations as needed.&nbsp;The default path and filename is&nbsp;<em style="font-weight: inherit;">&lt;installation-folder&gt;</em>/config_dta.py.</td>
		</tr>
		<tr>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong>credentialsFile</strong></td>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Required</td>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Path and name of the file&nbsp;storing the&nbsp;M-Pin Server Credentials.&nbsp;The default is&nbsp;<em style="font-weight: inherit;">&lt;installation-folder&gt;</em>/credentials.json.&nbsp;</td>
		</tr>
		<tr>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong style="font-style: inherit;">encrypt_master_secret</strong></td>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Conditional, Required</td>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">When True, a backup of&nbsp;the Master Secret is saved in encrypted form.&nbsp;Required if the&nbsp;<strong style="font-style: inherit;">backup</strong>&nbsp;option is set to&nbsp;<em style="font-weight: inherit;">True</em>.</td>
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
		<tr>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong style="font-style: inherit;">passphrase</strong></td>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Conditional, Required</td>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">A pre-set passphrase to the backup of the Master Secret if the Master Secret is to be backed up in encrypted form. The passphrase is used for generating the AES key for the Master Secret encryption. If not set (default), the M-Pin System admin will be prompted to generate the passphrase when the encryption is attempted. Pre-setting the pass-phrase is not recommended for security reasons.<br />
			<br />
			Required if the&nbsp;<strong style="font-style: inherit;">encrypt_master_secret</strong>&nbsp;option is set to&nbsp;<em style="font-weight: inherit;">True</em>.</td>
		</tr>
		<tr>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong style="font-style: inherit;">port</strong></td>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Required</td>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Port on which the service is listening. The default port is 8001.</td>
		</tr>
		<tr>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong>salt</strong></td>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Conditional, Required</td>
			<td class="confluenceTd" style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">A pre-set salt value to be used for generating the AES key for the&nbsp;encryption of the&nbsp;<span style="font-family: inherit;">Master Secret. The M-Pin Core instalation provides a randomly generated pre-set salt value, yet,</span>&nbsp;for security reasons,&nbsp;<span style="font-family: inherit;">it is strongly recommended to change that value with a randomly generated string of your own.</span><br />
			<br />
			Required if the&nbsp;<strong>encrypt_master_secret</strong>&nbsp;option is set to&nbsp;<em style="font-weight: inherit;">True</em>.</td>
		</tr>
		<tr>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong style="font-style: inherit;">syncTime</strong></td>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Optional</td>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">When&nbsp;<em style="font-weight: inherit;">True</em>, the the service&nbsp;syncs its time&nbsp;with the MIRACL&#39;s servers; if syncronization fails, the an attemp will be made each 5 seconds until success is achievd. When&nbsp;<em style="font-weight: inherit;">False</em>&nbsp;(recommended), this time synchronization is disabled and the service will rely on the system time.&nbsp;The default is&nbsp;<em style="font-weight: inherit;">False</em>.
			<div class="warning" style="margin: 0px; padding: 5px 30px; line-height: 1.6em; width: 1093.94px; background: url(&quot;/images/warning.png&quot;) 5px 50% no-repeat rgb(255, 237, 235);">Time synchronization is needed to perform time-based verification. Therefore, if you disable the syncing of the service with the&nbsp;MIRACL&#39;s servers, you should be then syncing your system with an NTP server to ensure that correct and precise system time is&nbsp;maintained.</div>
			</td>
		</tr>
		<tr>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;"><strong>timePeriod</strong></td>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Conditional, Required</td>
			<td style="margin: 0px; padding: 0.5em; font-family: inherit; border: 1px dotted rgb(211, 211, 211); vertical-align: top;">Time interval (in ms) at which the service syncs with the MIRACL&#39;s time servers. Required if the&nbsp;<strong style="font-style: inherit;">syncTime</strong>&nbsp;option is enabled. The default setting is&nbsp;<em style="font-weight: inherit;">86400000</em>, which amounts to one synchronization a day.</td>
		</tr>
	</tbody>
</table>
