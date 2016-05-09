Milagro MFA JavaScript Client
=======================

The Milagro JavaSript Client is the client library for **Milagro MFA**. It is made by two components - the browser client, also called PIN pad. And the HTML5 mobile client. 


##PIN Pad

The PIN Pad is a JavaScript software component that should be integrated into the Customer's Application Web Page. The PIN Pad encapsulates all the operations and logic that needs to be performed at the front-end, in order to register and authenticate an end-user.

##HTML5 Mobile client

The Mobile App is a JavaScript application, much similar to the PIN Pad. The Mobile App also carries out the operations needed to register and authenticate an end-user, but the user is authenticated to a browser session, rather than to a session on the mobile device.

##Building the PIN Pad

1. NOTE: You might have to update your package distribution system. For Ubuntu you would need to do: `sudo apt-get update`
2. Install *Node Package Manager* and *Node*. For instance on Ubuntu you need to do:
  1. `sudo apt-get install npm`
  2. `sudo npm install -g n`
  3. `sudo n 0.10.33`. NOTE that you need *curl* installed to do this.
3. Install *grunt* and the required modules
  1. `sudo npm install -g grunt-cli`
4. Install *handlebars* and the required modules
  1. `sudo npm install -g handlebars@3.0.1`
5. Install *bower* and the required modules
  1. `sudo npm install -g bower`
6. Checkout/Clone the repository to `<work-dir>`
7. Install the locally required modules for Node
  1. `cd <work-dir>/browser` or `cd <work-dir>/mobile`
  2. `sudo npm install`
8. Create `settings.json` file
  1. `cp settings.json_build settings.json`
  2. NOTE Available templates: milagro.
9. Build the app
  1. `grunt build`

The built app should be placed in `<work-dir>/build/out/browser` or `<work-dir>/build/out/mobile`.

**NOTE** that the `settings.json` file that was created above, should be modified with the correct base URL for the PIN Pad resources and with the desired template. For more details see the bellow documentation.

<p>For further details also see the <a href="../getting-started/milagro-mfa-overview.html"> Milagro MFA Server - Developer Guide. </a> 