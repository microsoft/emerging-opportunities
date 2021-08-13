# Overview

[**< Back to NH4H**](README.md)

Enterprise developers are increasingly using React to develop applications- but what happens when you need to add authetnication?  Reagrdless of if you're authenticating internal only, or internal/external users we hope this document will help!

The [MSAL 1.x for JavaScript](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-browser/README.md#:~:text=The%20MSAL%20library%20for%20JavaScript%20enables%20client-side%20JavaScript,Microsoft%20accounts%2C%20etc.%20through%20Azure%20AD%20B2C%20service.) will do the heavy lifting for us, but we're going to need to develop a  pattern to make this work.

# Authentication Flow 
Here's how the flow will work for a redirect login:
1. The App component will mount
2. MSAL will be initialized.
3. MSAL will check if this request is a redirect from a login request.
There will be two paths here:
### Path 1: Request is NOT a Redirect
If we're in this path then the user hasn't clicked sign in and we should consider them not signed in.  So we can render the sign in button.
When the user clicks the sign in button, MSAL will iniiate a redirect sign in request, the browser will navigate to login.microsoft.com, and when sucessful redirect to the app page. (So go back to step 1 above)

### Path 2: Request is a Redirect
Ok so if we're here, the user is logged in!
We can process the response for an id token, and any access tokens we requested.  
We should also start rendering the Logout button.

# Azure Active Directory (AAD) Setup
> Read more about creating [App Registrations in AzureAd](https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app#:~:text=Follow%20these%20steps%20to%20create%20the%20app%20registration%3A,Name%20for%20your%20application.%20...%20More%20items...%20)

**YOU DON'T NEED TO BE A GLOBAL ADMIN TO DO THIS!**
1. Create an App Registration.  
2. Redirect URL: http://localhost:3000/.auth/login/aad/callback
3. Check **both** ID and Access Tokens check boxes
4. Options:
   a. If you're authenticating internal only users then check " Accounts in this organizational directory only (Microsoft only - Single tenant)"
   b. If you're going to authenticate external users with Live, Microsoft accounts check "Accounts in any organizational directory (Any Azure AD directory - Multitenant)"
   c. If you want to authenticate users in all directories you'll have to use AzureADB2C (not covered in this document).   

# Sample Code
## Project Setup
You're going to need MSAL. So ```npm require msal```

## MSAL Configuration
```JavaScript
let msalConfig = {
      auth: {
        clientId: 'b3544b0c-1209-4fe8-b799-8f63a0179fa0',        
        authority: "https://login.microsoftonline.com/common",
      }
    };
    let msalI = new Msal.UserAgentApplication(msalConfig);
```

## Component Did Mount
```JavaScript
if (msalInstance.getAccount()) {   
      //user signed in; get token
      msalInstance.acquireTokenSilent(loginRequest)
        .then((response)=>{
          token=response.accessToken)
        });
    }else{
      let loginRequest = {
         scopes: ["user.read"] 
      };    
      msalInstance.loginRedirect(loginRequest));     
    }

```

## Logout
```JavaScript
msal.logout()
```

## Notes
Almost all msal functions return promises so consider adding logic to catch exceptions.
Consider creating a "process signin" function to keep signin logic in a single place.
A more comprehensive example with a login button can be [found here](https://github.com/microsoft/NH4H-UserReg/blob/main/src/App.js)

# Common Concerns
* If I include a client ID in my app code am I exposing a security risk?
In order to authenticate with this client ID the app must be hosted at a URL included in the list of valid redirect URLs.  (This is why it's really important to NOT include localhost on your production app registration.)
* If I use this method, am I exposed to security risks?
When you use the MSAL code- your auth. code is written by Microsoft, and is Open Source and checked by millions of developers globably.  Using this library will be much more secure than trying to write your own.

# Working Sample
You can find a working version of this app at: [NurseHack4Health](https://nursehack4health.org/registration)
Source code for this app can be found [here](https://github.com/microsoft/NH4H-UserReg)

# Using Popup Method
Don't want to implement redirect?  You can always implement popup!  Most devs will not like the idea of a popup because popup blockers can be an issue.

