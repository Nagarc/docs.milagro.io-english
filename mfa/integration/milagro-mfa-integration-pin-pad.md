---
currentMenu: milagro-mfa-integration-pin-pad
---

<div id="generated-toc" class="generate_from_h2"></div>



<h1>Integrating the PIN Pad</h1>



<p style="margin: 10px 0px 20px; padding: 0px; line-height: 1.6em; color: rgb(62, 69, 76); font-family: Lato, sans-serif; font-size: 1.4em;">The PIN Pad should be integrated into the web application (RPA) login HTML page. To do this:</p>

<ol>
	<li><strong style="font-style: inherit;">Include the PIN Pad&#39;s main module</strong>, mpin.js, by adding&nbsp;<span style="line-height: 19.2px;">a script tag similar to the following,&nbsp;</span>into the HTML head:<br />
	<span class="CVXCodeinText" style="font-family: 'Courier New';">&lt;script type=&quot;text/javascript&quot; src=&quot;{mpin-path}/mpin.js&quot; /&gt;</span></li>
	<li><strong style="font-style: inherit;">Instantiate and Initialize an mpin object.</strong>&nbsp;This is done with the following JavaScript code:<br />
	<span class="CVXCodeinText" style="font-family: 'Courier New';">new mpin( &lt;init-options&gt; );</span></li>
</ol>

<p style="margin: 10px 0px 20px; padding: 0px; line-height: 1.6em; color: rgb(62, 69, 76); font-family: Lato, sans-serif; font-size: 1.4em;">The following is a sample HTML page implementation:<span style="color: rgb(153, 153, 153); font-family: Arial, sans-serif; font-size: 1.7em; font-weight: bold; line-height: 1em;">​</span></p>

<pre style="margin-top: 0px; margin-bottom: 20px; padding: 15px; unicode-bidi: embed; border: 1px dotted; font-size: 12px;">
&lt;!DOCTYPE html PUBLIC &quot;-//W3C//DTD XHTML 1.0 Transitional//EN&quot; 
&quot;http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd&quot;&gt; 
&lt;html xmlns=&quot;http://www.w3.org/1999/xhtml&quot;&gt; 
&lt;head&gt; 
&lt;meta http-equiv=&quot;Content-Type&quot; content=&quot;text/html; charset=UTF-8&quot; /&gt; 
&lt;title&gt;M-Pin demo&lt;/title&gt; 
&lt;link href=&quot;/public/css/MIRACL.css?v=ee4d555e38d8c86110e6130f077bc6e2&quot; rel=&quot;stylesheet&quot; type=&quot;text/css&quot; /&gt; 
&lt;link href=&quot;/public/css/mpin.min.css?v=b7676587a6d88e2818ef2f1a7d1fdae6&quot; rel=&quot;stylesheet&quot; type=&quot;text/css&quot; /&gt; 
&lt;!-- Favicons 
================================================== --&gt; 
&lt;link rel=&quot;shortcut icon&quot; 
href=&quot;/public/images/favicon.ico?v=206feb63bb8d6b052afb1192d57d83a7&quot;&gt; 
&lt;!-- Fonts 
================================================== --&gt; 
&lt;link 
href=&#39;//fonts.googleapis.com/css?family=Roboto:400,400italic,700,700italic&#39; rel=&#39;stylesheet&#39; type=&#39;text/css&#39;&gt; 
&lt;script type=&quot;text/javascript&quot; 
src=&quot;https://mpin.MIRACL.net/v0.3/mpin.js?r=139539313122&quot;&gt;&lt;/script&gt; 
&lt;script type=&quot;text/javascript&quot;&gt; 
new mpin( { 
targetElement: &quot;pinHolder&quot;, clientSettingsURL: 
&quot;http://192.168.10.138:8005/rps/clientSettings&quot;, 
mobileAppFullURL: &quot;http://192.168.10.138:8005/m/index.html&quot;, 
successSetupURL: &quot;/successSetup&quot;, successLoginURL: &quot;/protected&quot;, onSuccessSetup: function(setupData, onSuccess) { 
console.log(&quot;Setup PIN successful&quot;) onSuccess() 
}, 
onSuccessLogin: function(authData) { console.log(&quot;Login successful&quot;) window.location = &quot;/protected&quot; 
}, 
onVerifySuccess: function(data){ 
}, 
identityCheckRegex: &quot;[0-9a-zA-Z]+&quot; 
}); 
&lt;/script&gt; 
&lt;/head&gt; 
&lt;body&gt; 
&lt;div id=&quot;header&quot;&gt; 
&lt;div class=&quot;container&quot;&gt; 
&lt;a href=&quot;http://MIRACL.com&quot; target=&quot;_blank&quot; 
class=&quot;logo1&quot;&gt;&lt;img src=&quot;/public/images/MIRACL-logo.jpg?v=0517e63d9febecab7894f22262f21d67&quot; alt=&quot;MIRACL Logo&quot; width=&quot;170&quot; height=&quot;33&quot; title=&quot;MIRACL Logo&quot; style=&quot;border-style: 
none&quot;&gt;&lt;/a&gt; 
&lt;a href=&quot;http://www.MIRACL.com/m-pin/&quot;, target=&quot;_blank&quot; 
class=&quot;logo2&quot;&gt;&lt;img alt=&quot;M-Pin strong authentication logo&quot; src=&quot;/public/images/m-pin-logostrong.png?v=3517e8e85a0030f3f4fad11d0e9448c9&quot; width=&quot;152&quot; height=&quot;54&quot; title=&quot;M-Pin strong authentication logo&quot; style=&quot;border-style: none&quot;&gt;&lt;/a&gt; 
&lt;/div&gt; 
&lt;div class=&quot;clear&quot;&gt;&lt;/div&gt; 
&lt;/div&gt; 
&lt;div id=&quot;content&quot;&gt; 
&lt;div class=&quot;container&quot;&gt; 
&lt;div class=&quot;nav&quot;&gt; 
&lt;ul&gt; 
&lt;li&gt;&lt;a href=&quot;/&quot; class=&quot;active&quot;&gt;Home&lt;/a&gt;&lt;/li&gt; 
&lt;li&gt;&lt;a href=&quot;http://www.MIRACL.com/mpin/&quot;, target=&quot;_blank&quot;&gt;About M-Pin&lt;/a&gt;&lt;/li&gt; 
&lt;li&gt;&lt;a href=&quot;http://www.MIRACL.com/m-pindownload&quot; target=&quot;_blank&quot;&gt;Download M-Pin&lt;/a&gt;&lt;/li&gt; 
&lt;li&gt;&lt;a href=&quot;https://MIRACL.org&quot; target=&quot;_blank&quot;&gt;Community&lt;/a&gt;&lt;/li&gt; 
&lt;/ul&gt; 
&lt;div class=&quot;clear&quot;&gt;&lt;/div&gt; 
&lt;/div&gt; 
&lt;div class=&quot;content&quot;&gt; 
&lt;h1&gt;Welcome to the M-Pin System Demo&lt;/h1&gt; 
&lt;!--action box start--&gt; 
&lt;div class=&quot;one column center grey marBot20 marTop20&quot;&gt; 
&lt;div id=&quot;pinHolder&quot; style=&quot;margin:auto; width:260px;&quot;&gt; 
Loading PinPad... 
&lt;/div&gt; 
&lt;/div&gt; 
&lt;div class=&quot;clear&quot;&gt;&lt;/div&gt; 
&lt;/div&gt; 
&lt;!--action box end--&gt; 
&lt;div id=&quot;footer&quot;&gt;&amp;copy; 2013 MIRACL UK Limited, All Rights 
Reserved.&lt;/div&gt; 
&lt;/div&gt; 
&lt;/div&gt; 
&lt;/body&gt; 
&lt;/html&gt;</pre>

<p>The source should be retrieved from GitHub and served from a location of your choice.</p>

<p> For full instructions follow this <a href="../javascript/milagro-mfa-javascript-guide.html"> link. </a> </p>
