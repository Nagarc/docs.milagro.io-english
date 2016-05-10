---
currentMenu: milagro-mfa-enabling-html5
---


##Enabling the HTML5 mobile authentication
<!-- MsoSubtitle -->


In the HTML page in which the Browser PIN Pad is integrated, the Browser PIN Pad should be configured with the URL for the Mobile App via the mobileAppFullURL setting:<span style="color: rgb(153, 153, 153); font-family: Arial, sans-serif; font-size: 1.7em; font-weight: bold; line-height: 1em;">​</span></p>

<pre style="margin-top: 0px; margin-bottom: 20px; padding: 15px; unicode-bidi: embed; border: 1px dotted; font-size: 12px;">
&lt;script type=&quot;text/javascript&quot;&gt; 
new mpin({ 
. . . 
mobileAppFullURL: &quot;&lt;mobile-app-base-url&gt;/index.html&quot;, 
. . . 
}); 
&lt;/script&gt; </pre>

<p>By default, the Mobile App will make a request to get its client settings to the following relative URL: /rps/clientSettings. Therefore it is required to serve the Mobile App from the RPA&#39;s domain, which will allow the AJAX request for the client settings to reach the Proxy which, in turn, will propagate the request with the rps prefix to the RPS. If this requirement is not met, the Mobile App&#39;s default settings should be modified accordingly and the App should be re-built.</p>

<p>The HTML5 mobile app should be served by your web application. To this end, you need to get the source from GitHub and serve the app from its location.<br style="color: rgb(62, 69, 76); font-family: Lato, sans-serif; font-size: 16.8px; line-height: 26.88px; background-color: rgb(255, 255, 255);" </p>

<p> For full instructions follow this <a href="../javascript/milagro-mfa-javascript-guide.html"> link. </a> </p>
