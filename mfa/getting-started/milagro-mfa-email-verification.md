---
currentMenu: milagro-mfa-email-verification
---

#Configuring the Demo Site to Use Email Verification

**1** Stop all the M-Pin services by running the following command in the M-Pin installation directory (default is /opt/mpin):
```
>sudo ./mpin stop all</div>
```

You need to edit /opt/mpin/config_demo.py. 
Scroll down to the # Verification emails settings; section and amend/add the following parameters:

>*forceActivate:* change this to **False** </br>
*emailSubject:* set this to the subject you wish your verification email to have. Default is: </br>
***M-Pin demo: New user activation*** </br>
*emailSender:* set this to the email address that you want the verification email to be sent from </br>
*smtpServer:* the name of the SMTP server you are using </br>
*smtpPort:* the port of the SMTP server you are using. Default is ***25***</br>
*smtpUser:* the username of your SMTP account</br>
*smtpPassword:* the password for the above account</br>
*smtpUseTLS:* change this to **True** and uncomment it to enable it.</br>

Now start all the M-Pin services:
```
>sudo ./mpin start all
```
Visit the following URL again:

```
>http://IP ADDRESS:8005
```

Your identity already exists in the browser, so the PIN pad will immediately ask you for your PIN to login:
>As we now want to show email verification working, instead of entering your PIN, click the menu icon at the top-right of the PIN pad to display the identity management screen. </br>
>Click the pencil icon next to your identity, then **Remove identity** </br>
>Confirm it by clicking **Yes, Remove it.** </br>


>You will see the screen which prompts you to create a new identity

>Enter your email address, then **Setup M-Pin** </br>

You should get an email with an activation link.

Click that activation link in your email to confirm your identity. </br>
>Click **Confirm and activate** to activate your identity. </br>
>Once you have activated it, close this screen and go back to your Identity page and click **I confirmed my email**. </br>
>You will get next screen with your new email address indicating that it has been verified.
</br>
Now just set up your pin and knock yourselves out!

