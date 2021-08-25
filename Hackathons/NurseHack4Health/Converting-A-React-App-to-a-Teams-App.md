We wanted to convert our TeamBuilder app into a Teams A].
Surfacing an app in Teams brings your app closer to where your users are collaborating.  
Teams apps [have rich capabilities](https://docs.microsoft.com/en-us/microsoftteams/platform/overview) and can interact with users using chat, in meetings, through tabs, or a combination of any of the above.

Prior to NH4H 2021 we exposed [TeamBuilder react app](https://github.com/microsoft/NH4H-TeamBuilder) via a Teams tab ([instructions on exposing a website via a tab](https://docs.microsoft.com/en-us/microsoftteams/platform/tabs/what-are-tabs)). But we wanted TeamBuilder to be more redistributable, and we wanted to use some built in Teams features, so we decided to convert it into a Teams App.  Final code is available: [https://github.com/microsoft/hackathon-team-builder](https://github.com/microsoft/hackathon-team-builder).

This document shows how we did it, and how you can too!

#Create Teams App Skeleton
First get started by creating a [Teams App with React.](https://docs.microsoft.com/en-us/microsoftteams/platform/get-started/first-app-react?tabs=vscode)   This entire process should take about 10-45 mins depending on your expereince and if you have to install prereqs.
Since a react app only used web content you'll only need the "tab" capability.

Make sure you app runs and that you are familiar with code structure.
For the rest of the tutorial let's assume we created an app in C:\HelloWorld and our old react app is in C:\HWReact\

#Update package.json
Now that the app is running let's import the dependencies of our old app.
Edit C:\HelloWorld\tab\package.json and add the dependencies from your exsisting a].

Note: Don't add the dependiencies to C:\HelloWorld\package.json (this file is used for the entire app)
Restart your app locally (hit F5 in Visual Studio Code) to install all the pacakges.

#Copy your old code base
Create a new folder in C:\HelloWorld\tab\src\components\
Rename that folder to your old app's name (ex: hwreact)
Now copy your old app's entire code base (everything in C:\HWReact\src) into the new folder (you don't need package.json or node_modules).

We're almost there.  
You'll need to rename App.js and the export of App to something else.  For example- let's change App.js to HWApp.js.   We'll need to change the last line of the file so that we're exporting HWApp.

You can see a finished version of process [in the teambuilder](https://github.com/microsoft/hackathon-team-builder/tree/main/hackathonTeamBuilder/tabs/src/components) folder.  Note that we renamed App.js to TBApp.


#Update Tab.js
Now all you need to do is add <HWApp/> to Tab.jsx and that's it!
Your entire app is now running inside teams

#(Optional) Update Index.html
Don't forget that in your old app you might have touched public\index.html so please make the same updates to C:\HellowWorld\tab\public\index.html.

#Next Steps

##Deploy and package to Teams
[Follow these steps to deploy and package to Teams](https://docs.microsoft.com/en-us/microsoftteams/platform/get-started/first-app-react?tabs=vscode#deploy-your-app-to-azure)

##Update the UI
Now that you're creating a Teams App you should move to FluentUI- the UI that Teams uses.
[Quickstart for using FluentUI React](https://fluentsite.z22.web.core.windows.net/0.57.0/quick-start)

##Replace MSAL
[Use this guide to replace MSAL in your app](Calling-an-OAuth-protected-API-from-a-Teams-App.md)