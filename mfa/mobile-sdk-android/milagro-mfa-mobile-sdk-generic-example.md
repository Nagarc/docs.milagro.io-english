<h1><span style="font-size: 32px;">Generic app code example</span></h1>
<h2>Overview</h2>
<p class="MsoNormal">This page provides a generic code example of an app for Android to help you get started with the SDK. It demonstrates the full user registration/authentication cycle in its correct succession:</p>

<ul>
    <li class="MsoNormal">Initialization</li>
    <li class="MsoNormal">User creation and verification</li>
    <li class="MsoNormal">User verification (again)</li>
</ul>
<p class="MsoNormal">You can use this example as a “skeleton” on which to further build your specific use cases and functionalities.</p>

<h2>Example</h2>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt;">
<pre class="computer_code">/*
* Initializing the SDK
*/
MPinSDK sdk = new MPinSDK();

HashMap&lt;String, String&gt; config = new HashMap&lt;String, String&gt;();
config.put(MPinSDK.CONFIG_BACKEND, "http://ec2-54-77-232-113.eu-west-1.compute.amazonaws.com");

Status status = sdk.Init(config, context);

if (status.getStatusCode() != Status.Code.OK) {
   // handle error
}

/*
* Creating a User identity
*/
User user = sdk.MakeNewUser("me@miracl.com");

status = sdk.StartRegistration(user);

if (status.getStatusCode() != Status.Code.OK) {
   // handle error and exit
}

switch (user.getState()) {
   case state.STARTED_REGISTRATION: {
       boolean waitForCofirmation = true;
       
       while (waitForCofirmation) {
           // Wait for user identity confirmation
           
           status = sdk.ConfirmRegistration(user);
           
           if (status.getStatusCode() == Status.Code.IDENTITY_NOT_VERIFIED) {
               Thread.sleep(3000);
               continue;
           }
               
           if (status.getStatusCode() != Status.Code.OK) {
               // handle error and exit
           }

           waitForCofirmation = false;
       }
       break;        
   }
   case State.ACTIVATED: {
       status = sdk.ConfirmRegistration(user);
       
       if (status.getStatusCode() != Status.Code.OK) {
           // handle error and exit
       }
       break;
   }
   default:
       // Something goes wrong
       // handle error and exit
}

String setupPin;
//
// Read PIN Code or secret from the user
//

status = sdk.FinishRegistration(user, setupPin);

if (status.getStatusCode() != Status.Code.OK) {
   // handle error and exit
}

/*
* Retrieving the stored User identities
*/
ArrayList&lt;User&gt; users = new ArrayList&lt;User&gt;();
sdk.ListUsers(users);

/*
* Authenticating the User
*/
status = sdk.StartAuthentication(user);

switch (status.getStatusCode()) {
   case Status.Code.OK:
       break;
   case Status.Code.REVOKED:
       // User is revoked, canot authenticate
       break;
   default:
       // handle error and exit
       break;
}

String authPin;
//
// Read PIN Code or secret from the user
//

status = sdk.FinishAuthentication(user, authPin);

switch (status.getStatusCode()) {
   case Status.Code.OK:
       // Authentication successful
       break;
   case Status.Code.INCORRECT_PIN:
       // Authentication failed
       if (user.getState() == State.BLOCKED) {
           // User is blocked and cannot authenticate anymore
       }
       break;
   default:
       // handle error and exit
       break;
}</pre>
</div>
</div>