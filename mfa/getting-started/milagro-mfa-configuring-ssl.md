<div id="generated-toc" class="generate_from_h2"></div>

<h1>Configuring the Demo Site to Use SSL</h1>

<p>This page provides an&nbsp;example where you can protect your demonstration installation using SSL by using the popular open source proxy server, nginx, in front of the M-Pin demo site and related services. &nbsp;One of the consequences of configuring nginx in this manner is that it will also make your installation visible to other machines on the same network. &nbsp;These instructions assume that no changes have been made to the M-Pin configuration files. &nbsp;Therefore we recommend reverting the configuration files back to the copies made in Making the Demo Accessible Externally.<br />
This page also assumes that you already have a default installation of nginx with SSL support enabled and have an SSL certificate and key file available.</p>

<ol>
	<li>Copy your .crt &amp; .key files to &lt;installation directory&gt;/servers/demo</li>
	<li>A working sample of the nginx.conf file with all the required changes, is&nbsp;given below:​​
	<div class="computer_code">#user&nbsp; nobody;<br />
	worker_processes&nbsp; 1;<br />
	<br />
	#error_log&nbsp; logs/error.log;<br />
	#error_log&nbsp; logs/error.log&nbsp; notice;<br />
	#error_log&nbsp; logs/error.log&nbsp; info;<br />
	<br />
	#pid&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; logs/nginx.pid;<br />
	<br />
	<br />
	events {<br />
	&nbsp;&nbsp;&nbsp; worker_connections&nbsp; 1024;<br />
	}<br />
	<br />
	<br />
	http {<br />
	&nbsp;&nbsp;&nbsp; include&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; mime.types;<br />
	&nbsp;&nbsp;&nbsp; default_type&nbsp; application/octet-stream;<br />
	<br />
	&nbsp;&nbsp;&nbsp; #log_format&nbsp; main&nbsp; &#39;$remote_addr - $remote_user [$time_local] &quot;$request&quot; &#39;<br />
	&nbsp;&nbsp;&nbsp; #&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &#39;$status $body_bytes_sent &quot;$http_referer&quot; &#39;<br />
	&nbsp;&nbsp;&nbsp; #&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &#39;&quot;$http_user_agent&quot; &quot;$http_x_forwarded_for&quot;&#39;;<br />
	<br />
	&nbsp;&nbsp;&nbsp; #access_log&nbsp; logs/access.log&nbsp; main;<br />
	<br />
	&nbsp;&nbsp;&nbsp; sendfile&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; on;<br />
	&nbsp;&nbsp;&nbsp; #tcp_nopush&nbsp;&nbsp;&nbsp;&nbsp; on;<br />
	<br />
	&nbsp;&nbsp;&nbsp; #keepalive_timeout&nbsp; 0;<br />
	&nbsp;&nbsp;&nbsp; keepalive_timeout&nbsp; 65;<br />
	<br />
	&nbsp;&nbsp;&nbsp; #gzip&nbsp; on;<br />
	<br />
	&nbsp;&nbsp;&nbsp; server {<br />
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; listen&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 80;<br />
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server_name&nbsp; localhost;<br />
	<br />
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; #charset koi8-r;<br />
	<br />
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; #access_log&nbsp; logs/host.access.log&nbsp; main;<br />
	<br />
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; location / {<br />
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; root&nbsp;&nbsp; html;<br />
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; index&nbsp; index.html index.htm;<br />
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; }<br />
	<br />
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; #error_page&nbsp; 404&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /404.html;<br />
	<br />
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; # redirect server error pages to the static page /50x.html<br />
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; #<br />
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; error_page&nbsp;&nbsp; 500 502 503 504&nbsp; /50x.html;<br />
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; location = /50x.html {<br />
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; root&nbsp;&nbsp; html;<br />
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; }<br />
	<br />
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; # proxy the PHP scripts to Apache listening on 127.0.0.1:80<br />
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; #<br />
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; #location ~ \.php$ {<br />
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; #&nbsp;&nbsp;&nbsp; proxy_pass&nbsp;&nbsp; http://127.0.0.1;<br />
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; #}<br />
	<br />
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000<br />
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; #<br />
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; #location ~ \.php$ {<br />
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; #&nbsp;&nbsp;&nbsp; root&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; html;<br />
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; #&nbsp;&nbsp;&nbsp; fastcgi_pass&nbsp;&nbsp; 127.0.0.1:9000;<br />
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; #&nbsp;&nbsp;&nbsp; fastcgi_index&nbsp; index.php;<br />
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; #&nbsp;&nbsp;&nbsp; fastcgi_param&nbsp; SCRIPT_FILENAME&nbsp; /scripts$fastcgi_script_name;<br />
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; #&nbsp;&nbsp;&nbsp; include&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; fastcgi_params;<br />
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; #}<br />
	<br />
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; # deny access to .htaccess files, if Apache&#39;s document root<br />
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; # concurs with nginx&#39;s one<br />
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; #<br />
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; #location ~ /\.ht {<br />
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; #&nbsp;&nbsp;&nbsp; deny&nbsp; all;<br />
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; #}<br />
	&nbsp;&nbsp;&nbsp; }<br />
	<br />
	<br />
	&nbsp;&nbsp;&nbsp; # another virtual host using mix of IP-, name-, and port-based configuration<br />
	&nbsp;&nbsp;&nbsp; #<br />
	&nbsp;&nbsp;&nbsp; #server {<br />
	&nbsp;&nbsp;&nbsp; #&nbsp;&nbsp;&nbsp; listen&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 8000;<br />
	&nbsp;&nbsp;&nbsp; #&nbsp;&nbsp;&nbsp; listen&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; somename:8080;<br />
	&nbsp;&nbsp;&nbsp; #&nbsp;&nbsp;&nbsp; server_name&nbsp; somename&nbsp; alias&nbsp; another.alias;<br />
	<br />
	&nbsp;&nbsp;&nbsp; #&nbsp;&nbsp;&nbsp; location / {<br />
	&nbsp;&nbsp;&nbsp; #&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; root&nbsp;&nbsp; html;<br />
	&nbsp;&nbsp;&nbsp; #&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; index&nbsp; index.html index.htm;<br />
	&nbsp;&nbsp;&nbsp; #&nbsp;&nbsp;&nbsp; }<br />
	&nbsp;&nbsp;&nbsp; #}<br />
	<br />
	<br />
	&nbsp;&nbsp;&nbsp; # HTTPS server<br />
	&nbsp;&nbsp;&nbsp; #<br />
	&nbsp;&nbsp;&nbsp; server {<br />
	&nbsp;&nbsp;&nbsp;&nbsp; listen 443 ssl;<br />
	&nbsp; server_name gendemo;<br />
	&nbsp; ssl_certificate /opt/mpin/servers/demo/certificate.crt;<br />
	&nbsp; ssl_certificate_key /opt/mpin/servers/demo/certificate.key;&nbsp;&nbsp;&nbsp;<br />
	<br />
	location /mpin/ {<br />
	&nbsp;&nbsp;&nbsp; rewrite ^/mpin/(.*)&nbsp; /$1 break;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br />
	&nbsp;&nbsp;&nbsp; proxy_pass http://127.0.0.1:8002;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br />
	<br />
	<br />
	proxy_set_header Upgrade $http_upgrade;<br />
	proxy_set_header Connection &quot;upgrade&quot;;<br />
	<br />
	proxy_set_header Host $host;<br />
	proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;<br />
	proxy_set_header X-Forwarded-HTTPS 0;<br />
	&nbsp; }<br />
	location /rps/ {<br />
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; proxy_pass http://127.0.0.1:8011;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br />
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;<br />
	proxy_set_header X-Forwarded-HTTPS 0;<br />
	&nbsp;&nbsp;&nbsp; proxy_set_header Host $host;<br />
	&nbsp; }<br />
	location / {<br />
	&nbsp;&nbsp;&nbsp; proxy_pass http://127.0.0.1:8005;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br />
	&nbsp;&nbsp;&nbsp; proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;<br />
	proxy_set_header X-Forwarded-HTTPS 0;<br />
	&nbsp;&nbsp;&nbsp; proxy_set_header Host $host;<br />
	&nbsp; }<br />
	&nbsp;&nbsp;&nbsp; }<br />
	<br />
	}</div>
	</li>
	<li>Replace certificate.crt &amp; certificate.key in the above configuration file with the actual names of your certificate and key files</li>
	<li>In /opt/mpin/config_demo.py set clientSettingsURL to:
	<div class="computer_code">&quot;/rps/clientSettings&quot;</div>
	</li>
	<li>In the same configuration file set&nbsp;verifyIdentityURL to:
	<div class="computer_code">&quot;https://&lt;IP ADDRESS&gt;/mpinActivate&quot;</div>
	</li>
	<li>In the same configuration file set mobileAppFullURL to:
	<div class="computer_code">&quot;https://&lt;IP ADDRESS/m&quot;</div>
	</li>
	<li>In the same configuration file, you need to configure your SMTP server:
	<ul>
		<li>forceActivate &ndash; change this to &ldquo;False&rdquo;</li>
		<li>emailSubject &ndash; set this to the subject you wish your verification email to have. &nbsp; Default is &quot;M-Pin demo: New user activation&quot;</li>
		<li>emailSender &ndash; set this to the email address that you want the verification email to be sent from</li>
		<li>smtpServer &ndash; the name of the SMTP server you are using</li>
		<li>smtpPort &ndash; the port of the SMTP server you are using. &nbsp;Default is 25</li>
		<li>smtpUser &ndash; the username of your SMTP account</li>
		<li>smtpPassword &ndash; the password for the above account</li>
		<li>smtpUseTLS &ndash;&nbsp;change this to &quot;True&quot; and uncomment it to enable it</li>
	</ul>
	</li>
	<li>In /opt/mpin/config_rps.py set rpsBaseURL to:
	<div class="computer_code">&quot;&quot;</div>
	</li>
	<li>In /opt/mpin/config_rps.py set MPinAuthenticationServer to:
	<div class="computer_code">&quot;/mpin&quot;</div>
	</li>
	<li>Now restart nginx</li>
	<li>Restart all the M-Pin services by running the following in the M-Pin installation directory (default is /opt/mpin):
	<div class="computer_code">sudo ./mpin stop&nbsp;all</div>

	<div class="computer_code">sudo ./mpin start all</div>
	</li>
	<li>Now access the demonstration site by visiting the following URL in a browser on another machine on the same network as you M-Pin Server:
	<div class="computer_code">https://&lt;IP ADDRESS&gt;</div>
	</li>
	<li>Test out the browser client by following step 3 onward in <a hqid="226652" href="#">Testing the Automated M-Pin Core Installation Using a Browser on the M-Pin Server</a>&nbsp;and the browser client by following the instructions in <a hqid="226661" href="#">Testing the Mobile Client</a></li>
</ol>
