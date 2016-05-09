<h1>Integrating Milagro MFA in a web app</h1>
This page describes how to create a simple username and password Relying Party Application (RPA) website using Python and then shows you how to convert this application to use Milagro MFA aunthentication.
<h2>Pre-requisites</h2>
This example was built using Ubuntu 14 but should work similarly on any modern Linux or Mac OS X machine with Python 2.7. However, there are some pre-requisites that you need to install:
<ul>
	<li>PIP (Python Package Installer):</li>
</ul>
<div class="computer_code">sudo apt-get install python-pip</div>
<ul>
	<li>Python modules "flask" &amp; "requests":</li>
</ul>
<div class="computer_code">sudo pip install flask requests</div>
<ul>
	<li>CURL:</li>
</ul>
<div class="computer_code">sudo apt-get install curl</div>
<h2>Installing the server</h2>
If you have not already installed the server, see the developer guide [<span style="color: #ff0000;">link here to the server developer guide]</span>
<h2>Building the Username and Password Application</h2>
Create a file named rpa.py then in it define the Python environment, import the modules we need to build the application and create an instance of the Flask class:
<div class="computer_code">

#! /usr/bin/env python

# import required modules including the Flask web app framework

from flask import Flask, request, redirect, render_template, jsonify, make_response

from flask import send_from_directory

import json

import requests

# create Flask application

app = Flask(__name__)

</div>
<div class="info">Note that some of the modules loaded above are not required by the username and password site but will be required when we convert to Milagro MFA authentication, so we will load them all now.</div>
Next we create an endpoint for the root of the application that points to index.html (which we will create later):
<div class="computer_code">

#add root endpoint for index.html

@app.route("/")

#define index function

def index():

return render_template("index.html")

</div>
Next we create an endpoint for the login page from which we can read the submitted username and password and call a function (see later) to validate them.  If they are valid, the user is redirected to the protected page and a simple cookie is set containing the username.  If the username and password combination is not valid, then the login page is displayed again with an error message:
<div class="computer_code">

# add login page endpoint for loginform.html

@app.route("/login", methods=["GET", "POST"])

#define login function

def login():

if request.method == "POST":

#set username and password from POST request:

username = request.form["username"]

password = request.form["password"]

if validateUsername(username, password): #see below for validate function

#if the username and password are valid, set a simple cookie and redirect to the protected page

resp = make_response(redirect("/protected"))

resp.set_cookie("username", username)

return resp

else:

#if the username and password are not valid, return error message and return to login form

return render_template("loginform.html", message="INVALID USERNAME OR PASSWORD")

#if GET request, simply return the login form

else:

return render_template("loginform.html")

</div>
Now we create an endpoint for the protected page (protected.html).  If no cookie is present, the user is redirected back to the root page (index.html).

If there is a cookie present, the protected page is displayed (protected.html).

We set username to the username in the cookie which protected.html displays.
<div class="computer_code">

# add "protected" end point

@app.route("/protected")

def protected():

loggeduser = request.cookies.get("username")

# if no cookies, then redirect to the index page

if not loggeduser:

return redirect("/")

# if there is a cookie, then redirect to the protected page

else:

return render_template("protected.html", username=loggeduser)

</div>
The final endpoint we create is for the logout link on the protected page.  This deletes the cookie and redirects the user back to the root page:
<div class="computer_code">

# add "logout" endpoint - deletes cookie and redirects to the home page

@app.route("/logout")

def logout():

resp = make_response(redirect("/"))

resp.delete_cookie("username")

return resp

</div>
We now create a function to verify the entered username and password.   Note that in reality, this function would likely lookup the user and (hashed) password in a database or LDAP directory, but for the sake of simplicity, we simply hard code the acceptable usernames and password into the Python code.
<div class="computer_code"># simple validate user function

def validateUsername(username, password):                return username == "john" and password == "123"

</div>
Finally we run the application defining the IP address and port we want the application to run on, and set the debug mode.
<div class="computer_code">

# run the app on localhost port 8005

app.run(host="0.0.0.0", port=8005, debug=True)

</div>
<h2>Building the Username &amp; Password Web Pages</h2>
Here we create the three web pages referenced by the RPA.  Note that these should be saved into the \templates subfolder of the directory that the RPA Python app is saved to.
<h3>Index Page (index.html)</h3>
First we create a simple index page that tells the user that they are not logged in and gives them a link to the login page:
<div class="computer_code">&lt;!DOCTYPE HTML&gt;

&lt;html&gt;

&lt;head&gt;

&lt;/head&gt;

&lt;body&gt;

&lt;h1&gt;Hello. You are not logged in&lt;/h1&gt;

&lt;p&gt;You need to &lt;a href="/login"&gt;login&lt;/a&gt;&lt;/p&gt;

&lt;/body&gt;

&lt;/html&gt;</div>
<h3>Login Page (loginform.html)</h3>
Next we create the login page with a placeholder for error messages and a form to allow the user to enter their username and password:
<div class="computer_code">&lt;!DOCTYPE HTML&gt;

&lt;html&gt;

&lt;body&gt;

&lt;p style="color:red"&gt;{{ message }}&lt;/p&gt;

&lt;form method="POST"&gt;

&lt;label&gt;Username: &lt;/label&gt;&lt;input type="text" name="username" /&gt;&lt;br/&gt;

&lt;label&gt;Password: &lt;/label&gt;&lt;input type="password" name="password" /&gt;&lt;br/&gt;

&lt;input type="submit" name="submit" /&gt;

&lt;/form&gt;

&lt;/body&gt;

&lt;/html&gt;</div>
<h3>Protected Page (protected.html)</h3>
Finally we create the protected page that tells the user that they are logged in and provides a logout link:
<div class="computer_code">&lt;!DOCTYPE HTML&gt;

&lt;html&gt;

&lt;body&gt;

&lt;h1 style="color:green"&gt;You are logged in as {{ username }}&lt;/h1&gt;

&lt;a href="/logout"&gt;Logout&lt;/a&gt;

&lt;/body&gt;

&lt;/html&gt;</div>
<h2>Running the Username &amp; Password RPA</h2>
We can start the RPA from the directory into which it has been saved by making rpa.py executable and running it as follows:
<div class="computer_code">chmod +x rpa.py

./rpa.py</div>
Next open a browser on the same machine and visit the following address:
<div class="computer_code">http://0.0.0.0:8005</div>
You should see the following page:

<img class="alignnone size-full wp-image-25759542" src="https://trecugggine.files.wordpress.com/2016/05/2015_01_05_17_15_181.png" alt="2015_01_05_17_15_181" width="709" height="240" />

&nbsp;

Clicking "Login" takes you to the login form where you can enter the username and password hardcoded above:

<img class="alignnone size-full wp-image-25759545" src="https://trecugggine.files.wordpress.com/2016/05/2015_01_05_17_17_122.png" alt="2015_01_05_17_17_122" width="709" height="240" />

&nbsp;

If you enter an incorrect username or password, an error message is displayed:

<img class="alignnone size-full wp-image-25759548" src="https://trecugggine.files.wordpress.com/2016/05/2015_01_05_17_18_073.png" alt="2015_01_05_17_18_073" width="709" height="240" />

&nbsp;

If the username and password are valid, you will be redirected to the protected page and your username will be displayed:

<img class="alignnone size-full wp-image-25759551" src="https://trecugggine.files.wordpress.com/2016/05/2015_01_05_17_19_064.png" alt="2015_01_05_17_19_064" width="709" height="240" />

&nbsp;
<h2>Converting the RPA to use M-Pin</h2>
Now we have a fully working username and password RPA, we can convert it to use Milagro MFA instead.
<h3>New Login Page (loginform.html)</h3>
First we need to edit loginform.html and add a reference in the header of the login page to the Javascript that runs the PIN pad.

<strong>Note:</strong> <span style="text-decoration: underline;">In this case we are using an instance hosted by MIRACL.com but you can build the <a href="https://github.com/miracl/milagro-mfa-js-client" target="_blank">Milagro MFA JavaScript Client</a>. For directions, see the developer guide <span style="color: #ff0000; text-decoration: underline;">[link to the developer guide for the javascript client].</span></span>

We initialize the PIN pad by setting the targetElement (where it should be displayed), clientSettingURL (the URL on the M-Pin server that it will get the parameters it needs to run from), mobileAppFullURL (location of the mobile application) &amp; successLoginURL (the URL to redirect the user to upon successful authentication):
<div class="computer_code">&lt;script type="text/javascript" src="https://mpin.miracl.com/v4/mpin.js"&gt;&lt;/script&gt;

&lt;script&gt;

new mpin({

targetElement: "pinHolder",

clientSettingsURL: "http://127.0.0.1:8011/rps/clientSettings",

mobileAppFullURL: "http://127.0.0.1:8005/m",

successLoginURL: "/protected"

})

&lt;/script&gt;</div>
Next we can remove the code for the username and password form and replace it with a div tag to hold the PIN pad:
<div class="computer_code">            &lt;div id="pinHolder" style="width:260px;"&gt;

Loading PinPad...

&lt;/div&gt;</div>
<h3>Milagro MFA Enabled RPA</h3>
Now we can update the Python RPA (rpa.py) by inserting the following code snippets before the validate user function.  First we add an endpoint to verify that the user is authorized to register with Milagro MFA.  We extract the userID from the request and display it at the console.  Finally we return “forceActivate” to allow the user to create their PIN immediately.  (In a production deployment, you would typically lookup the userID in your own directory to check that they are authorised in which case the user would be sent an email with a verification link allowing them to prove that they are who they claim to be).
<div class="computer_code">

# add verify endpoint

@app.route("/mpinVerify", methods=["POST"])

def mpinVerify():

# get data from POST request

data = json.loads(request.stream.read())

# get username from data

print "User trying to register: ", data["userId"]

# verification process would go here - e.g. send email

# forceActivate allows the user to create their PIN immediately

return jsonify({"forceActivate": True})

</div>
Next we add the authentication endpoint:
<div class="computer_code">

# add authenticate end point

@app.route("/mpinAuthenticate", methods=["POST"])

def mpinAuthenticate():

</div>
Then we read the data from the POST request to this endpoint:
<div class="computer_code">

#read data from POST request

data = json.loads(request.stream.read())

</div>
When a user authenticates with the M-Pin server, a one-time-token (authOTT) is generated and returned to the PIN pad.  The same token is also sent to the Milagro MFA Relying Party Service (RPS) along with the result of the authentication attempt.  We therefore need to extract the authOTT from the request:
<div class="computer_code">

#extract auth one time token from PIN pad

authOTT = data["mpinResponse"]["authOTT"]

</div>
Next we send the authOTT to the RPS to get the result of the authentication attempt:
<div class="computer_code">#check auth one time token with the RPS



rpsurl = "http://127.0.0.1:8011/authenticate"

reqData = {

"authOTT": authOTT

}</div>
Then we get the result back from the RPS and extract the result of the authentication attempt along with the username:
<div class="computer_code">

#get result from RPS

result = requests.post(rpsurl, data=json.dumps(reqData), headers={"content-type": "application/json"})

#extract data from result

rpsData = json.loads(result.text)

#extract username and authentication status

userId = rpsData.get("userId")

status = rpsData.get("status")

</div>
We then print the name of the user attempting to authenticate to the console:
<div class="computer_code">

#print username of user trying to authenticate

print "User tries to authenticate: ", userId

</div>
Then we check whether the authentication attempt was successful and if so, set the cookie as before and redirect the user to the protected page:
<div class="computer_code">

#display message and set cookie if authentication successful

if status == 200:

print "Successfull authentication for ", userId

resp = make_response("")

resp.set_cookie("username", userId)

return resp, 200

</div>
If the authentication attempt is unsuccessful, we print an error message:
<div class="computer_code">

#display error if authentication attempt unsuccessful

else:

print "Authentication failed: ", rpsData.get("message")

resp = make_response("")

return resp, status

</div>
The M-Pin Core server installation includes the static files for the mobile site.  These files must be hosted somewhere, so in this demonstration we will host them as part of the RPA.  Therefore we need to create an endpoint for these files:
<div class="computer_code">

#create end point for mobile app

@app.route('/m')

def serveMobileIndex():

return redirect("/m/index.html")

@app.route('/m/&lt;path:filename&gt;')

def serveMobile(filename):

return send_from_directory('/opt/mpin/mobile/', filename)

</div>
Finally we need to create an endpoint for the client settings which the PIN pad needs to access when it is initialized:
<div class="computer_code">

#create end point for PIN pad client settings

@app.route('/rps/clientSettings')

def serveRPSSettings():

return requests.get("http://127.0.0.1:8011/rps/clientSettings").text

</div>
&nbsp;
<h2>Running the Milagro-Enabled RPA</h2>
When you save changes to rpa.py it will automatically restart itself so there is no need to do this yourself.  Visit the same URL on which the RPA is running and you will see the same root page:

<img class="alignnone size-full wp-image-25759563" src="https://trecugggine.files.wordpress.com/2016/05/2015_01_06_10_26_551.png" alt="2015_01_06_10_26_551" width="709" height="227" />

&nbsp;

Now, clicking "login" displays the M-Pin PIN pad instead of the username and password form:

<img class="alignnone size-full wp-image-25759566" src="https://trecugggine.files.wordpress.com/2016/05/2015_01_06_10_28_222.png" alt="2015_01_06_10_28_222" width="709" height="569" />

&nbsp;

Select "Sign in from here":

<img class="alignnone size-full wp-image-25759570" src="https://trecugggine.files.wordpress.com/2016/05/2015_01_06_10_29_4731.png" alt="2015_01_06_10_29_4731" width="709" height="569" />

&nbsp;

Enter your email address and click "Setup M-Pin":

<img class="alignnone size-full wp-image-25759573" src="https://trecugggine.files.wordpress.com/2016/05/2015_01_06_10_30_424.png" alt="2015_01_06_10_30_424" width="709" height="569" />

&nbsp;

Enter a 4-digit PIN and click "Setup":

<img class="alignnone size-full wp-image-25759578" src="https://trecugggine.files.wordpress.com/2016/05/2015_01_06_10_31_1451.png" alt="2015_01_06_10_31_1451" width="709" height="569" />

&nbsp;

Click "Sign in now":

<img class="alignnone size-full wp-image-25759581" src="https://trecugggine.files.wordpress.com/2016/05/2015_01_06_10_31_536.png" alt="2015_01_06_10_31_536" width="709" height="569" />

&nbsp;

Enter your PIN and click "Login".  You will now see the same protected page as before:

<img class="alignnone size-full wp-image-25759584" src="https://trecugggine.files.wordpress.com/2016/05/2015_01_06_10_32_357.png" alt="2015_01_06_10_32_357" width="709" height="262" />

&nbsp;

&nbsp;