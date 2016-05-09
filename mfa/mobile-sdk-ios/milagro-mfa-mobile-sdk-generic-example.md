<div class="WordSection1">
<h1>Generic App Code Example</h1>
<h2>Overview</h2>
<p class="MsoNormal">This page provides a generic code example of an app for iOS to help you get started with the SDK. It demonstrates the full M-Pin User registration/authentication cycle in its correct succession: initialization, User creation and verification, and then User verification. You can use this example as a “skeleton” on which to further build your specific use cases and functionalities.</p>

<h2>Example</h2>
<div style="border: solid windowtext 1.0pt; padding: 1.0pt 4.0pt 1.0pt 4.0pt;">
<pre class="computer_code">/*
* Initializing the SDK
*/
[MPin initSDK];
MpinStatus* status = [MPin SetBackend:@"http://my.backend.com"];

if (mpinStatus.status != OK) {
    // Show error message and exit
}

/*
* Creating a User identity
*/
id iuser = [MPin MakeNewUser:@"me@domain.com"];
mpinStatus = [MPin StartRegistration:iuser];

if (mpinStatus.status != OK) {
    // Show error message and exit
}

switch ([iuser getState]) {
    case STARTED_REGISTRATION: {
        BOOL waitForCofirmation = TRUE;
        
        while (waitForCofirmation) {
            // Wait for user identity confirmation
            
            mpinStatus = [MPin ConfirmRegistration:iuser];
            
            if (mpinStatus.status == IDENTITY_NOT_VERIFIED) {
                [NSThread sleepForTimeInterval:3.0f];
                continue;
            }
                
            if (mpinStatus.status != OK) {
                // Show error message and exit
            }

            waitForCofirmation = FALSE;
        }
        break;        
    }
    case ACTIVATED: {
        mpinStatus = [MPin ConfirmRegistration:iuser];
        
        if (mpinStatus.status != OK) {
            // Show error message and exit
        }
        break;
    }
    default:
        // Something goes wrong
        // Show error message and exit
}

NSString* setupPin;
//
// Read PIN Code or secret from the user
//

mpinStatus = [MPin FinishRegistration:iuser pin:setupPin];

if (mpinStatus.status != OK) {
    // Show error message and exit
}

/*
* Retrieving the stored User identities
*/
NSArray* users = [MPin listUsers];

/*
* Authenticating the User
*/
mpinStatus = [MPin StartAuthentication:iuser];

switch (mpinStatus.status) {
    case OK:
        break;
    case REVOKED:
        // User is revoked, canot authenticate
        break;
    default:
        // Show error message and exit
        break;
}

NSString* authPin;
//
// Read PIN Code or secret from the user
//

mpinStatus = [MPin FinishAuthentication:iuser pin:authPin];

switch (mpinStatus.status) {
    case OK:
        // Authentication successful
        break;
    case INCORRECT_PIN:
        // Authentication failed
        if ([iuser getState] == BLOCKED) {
            // User is blocked and cannot authenticate anymore
        }
        break;
    default:
        // Show error message and exit
        break;
}</pre>
</div>
</div>