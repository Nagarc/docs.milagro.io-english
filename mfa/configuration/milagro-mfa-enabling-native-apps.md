<h1>Enabling Native Apps</h1>
<!-- MsoSubtitle -->


<p style="margin: 10px 0px 20px; padding: 0px; line-height: 1.6em; color: rgb(62, 69, 76); font-family: Lato, sans-serif; font-size: 1.4em;">You can enable authentication from a native mobile app manually by following the steps below:</p>

<ul>
	<li><strong style="font-style: inherit;">Edit</strong>&nbsp;&lt;instllation directory&gt;/config_demo.py</li>
	<li><strong>Add</strong> the following entries:</li>
</ul>

<pre style="margin-top: 0px; margin-bottom: 20px; margin-left: 40px; padding: 15px; unicode-bidi: embed; border: 1px dotted; font-size: 12px;">
mobileUseNative = True

mobileConfigURL = &#39;&lt;URL&gt;/rps/mobileConfig&#39; </pre>
<p> where &lt;URL&gt; is the public URL fro which your webapp (RPA) is served </p>
<ul>
	<li>Then <strong>restart</strong> the M-Pin Services.
	</li>
</ul>
