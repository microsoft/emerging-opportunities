If you're converting a react app to a Teams A] you may need to call protected resrouces.

#Add API Permissions to the Teams' App Registration
Your Team's App Registration ID can be found in .fx\env.local.data.
Add API permissions for your protected API, and grant admin consent.

#Authenticating
You're already in teams so you're already authenticated!! :)

#Dependencies
You'll need @microsoft/teamsfx but it's probably already been added to your package.json
[teamsfx sdk reference](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk)

#Get a token for the API
We'll need to import a few modules from teams' fx
```json
import {loadConfiguration , TeamsUserCredential} from "@microsoft/teamsfx";
```

Next we need to create a configuration.  You probably don't need to change the values below.
```
  loadConfiguration({
      authentication: {
        initiateLoginEndpoint: process.env.REACT_APP_START_LOGIN_PAGE_URL,
        simpleAuthEndpoint: process.env.REACT_APP_TEAMSFX_ENDPOINT,
        clientId: process.env.REACT_APP_CLIENT_ID,
      },
    });
```
Next create a TeamsCredential object and getch your token:
```json
 const scopes=['api://blahblah/user.impersonate'];
 const credential = new TeamsUserCredential(scopes);
 let token = credential.getToken();
```
That's it!

#Getting Logged In User Info
```
let userInfo = credential.getUserInfo()
let displayName=userInfo.displayName;
let email=userInfo.preferredUserName;
```

#Setup Cors
Since your teams app will be running from either an azure website or localhost you'll need to modify your API's CORS settings so that it's returning the appropriate CORS headers
For local dev: add https://localhost:3000 
For production: add <your Teams app's website> (ex: https://MyTeamsApp23seasd34dada.azurewebsites.net/)

#Refernce Code
You can see refernce code in the [teambuilder app](https://github.com/microsoft/hackathon-team-builder/blob/main/hackathonTeamBuilder/tabs/src/components/teambuilder/TBApp.js)

#Known Limitations
[Known Limitations of SSO within Teams](https://docs.microsoft.com/en-us/microsoftteams/platform/tabs/how-to/authentication/auth-aad-sso#known-limitations)