---
currentMenu: milagro-mfa-mobile-sdk-generic-example-wp
---

<div id="generated-toc" class="generate_from_h2"></div>


<div class="WordSection1">
<h1><span style="font-size:32px;">Generic M-Pin App Code Example - Milagro MFA Mobile SDK for Windows Phone</span></h1>

<h2>Overview</h2>

<p class="MsoNormal">This page provides a generic code example of an Milagro App for Windows phones to help you get started with the SDK. It demonstrates the full Milagro User registration/authentication cycle in its correct succession: initialization, User creation and verification, and then User verification.</p>

<p class="MsoNormal">You can use this example as a &ldquo;skeleton&rdquo; on which to further build your specific use cases and functionalities.</p>

<h2>Example - needs to be replaced by a Windows example</h2>

<div style="border:solid windowtext 1.0pt;padding:1.0pt 4.0pt 1.0pt 4.0pt">
<pre class="computer_code">
//
// Initializing the SDK for the first time
//
MPin sdk = new MPin();

IDictionary&lt;string, string&gt; config = new Dictionary&lt;string, string&gt;();
config.Add(&quot;backend&quot;, &quot;http://my.backend.com&quot;);

Status status = sdk.Init(config);

//
// Process service changed
//
status = sdk.SetBackend(&quot;http://my.secondBackend.com&quot;);
                
if (status.StatusCode != Status.Code.OK) 
{
    // Show error message and exit
}

//
// Creating a User identity
//
User user = sdk.MakeNewUser(@&quot;me@domain.com&quot;);
status = sdk.StartRegistration(user);

if (status != null &amp;&amp; status.StatusCode != Status.Code.OK)
{
    // Show error message and exit
}

switch (user.UserState)
{
    case User.State.StartedRegistration:
    {
        bool waitForCofirmation = true;

        while (waitForCofirmation) 
        {
            // Wait for user identity confirmation            
            status = sdk.ConfirmRegistration(user);

            if (status.StatusCode == Status.Code.IdentityNotVerified) 
            {
&nbsp;               await Task.Delay(3000);
                continue;
            }

            if (status.StatusCode != Status.Code.OK) 
            {
                // Show error message and exit
            }

            waitForCofirmation = false;
        }
        break;        
    }
    case User.State.Activated: 
    {
        status = sdk.ConfirmRegistration(user);

        if (status.StatusCode != Status.Code.OK)
        {
            // Show error message and exit
        }
        break;
    }
    default:
        // Something went wrong
        // Show error message and exit
}

string setupPin;
//
// Read PIN Code or secret from the user
//
status = sdk.FinishRegistration(user, setupPin);
if (status.StatusCode != Status.Code.OK)
{
    // Show error message and exit
}

//
// Retrieving the stored User identities
//
List&lt;User&gt; users = new List&lt;User&gt;();
sdk.ListUsers(users);

//
// Authenticating the User
//
status = sdk.StartAuthentication(user);

switch (status.StatusCode)
{
    case Status.Code.OK:
        break;
    case Status.Code.Revoked:
        // User is revoked, cannot authenticate
        break;
    default:
        // Show error message and exit
        break;
}

string authPin;
//
// Read PIN Code or secret from the user
//
status = sdk.FinishAuthentication(user, authPin);

switch (status.StatusCode) 
{
    case Status.Code.OK:
        // Authentication successful
        break;
    case Status.Code.IncorrectPIN:
        // Authentication failed
        if (user.UserState == User.State.Blocked) 
        {
            // User is blocked and cannot authenticate anymore
        }
        break;
    default:
        // Show error message and exit
        break;
}</pre>

<p class="CVXCodeExample" style="margin-top:0in;margin-right:4.5pt;margin-bottom:
8.0pt;margin-left:4.5pt"><span style="font-size:11.0pt;line-height:150%;
font-family:&quot;Courier New&quot;"><iuser> </iuser></span></p>
</div>
</div>
