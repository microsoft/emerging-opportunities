# Authentication Learnings

During our sprint we were tasked to create an app that involved .NET Core Api, Entity Framework, and GraphQL (ChilliCream's HotChocolate)

Because this app dealt with sensitive data Authentication and Authorization were key to making this secure.

I have followed tutorials here and there in the past but never really had to understand as deep as I need to now. 

First step we tried was adding EasyAuth to our azure resource (web app or functions)

## EasyAuth 

Description:
Use Azure's built in authentication to authenticate users [link](
https://docs.microsoft.com/en-us/azure/app-service/overview-authentication-authorization#:~:text=Azure%20App%20Service%20provides%20built-in%20authentication%20and%20authorization,and%20mobile%20back%20end%2C%20and%20also%20Azure%20Functions.)


### Application Registration

Application Registration is one of the most fundamental resource you should understand if you want to have any access and authentications enabled for your azure resources. 

I've written a [blog](https://www.linkedin.com/pulse/azure-app-registration-service-principal-daniel-kim/) in LinkedIn trying to explain what it is (in relation to service principal) how AAD's service principal uses it to give access to resources/users 

Here's the [official doc](https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app) on what an app registration is.

> I found this video to also be really helpful More thorough explanation on Azure App Registration [link](https://www.youtube.com/watch?v=YWvl0cIilyA)
    
### Set up in Azure Resource

  
  
**Authentication / Authorization **

Using JWT token you are able to determine all three. When your api (or any application) receives the JWT token, it can be used to authenticate (allows entry to resources), 
then it'll be used to determine authorization level (allows or disallows certain access level on the resources). It will also have information on how long this token lasts.

Resource: [Id Token / Access Token Explanation](https://www.youtube.com/watch?v=sICt5aS7wzk)

**Issues**
- Issues with graphql and EasyAuth (single page application requiring specific header for cross origin)

**Solution**
Postman and Web Api

> If you have **multifactor** enabled for your account, you MUST use (Authorization Code with PKCE)

JWT
	• Has Access Token (is this valid or not?)
		○ Yes? All Cool
		○ No? Next step
	• Has Refresh Token? (allows app to refresh without forcing user to authenticate again)
		○ Yes. Allows service to get a new access token
		○ No? Force users to authenticate again.
	• V 1.0 (Auth Url 'resource') vs v2.0 (specified tenant id and solely relies on the scope)
		○ Auth URL is where you login and will give you auth token (ID Token)
		○ AT will be used to be passed in to retrieve access token
	• Working path:
		○ UI (postman… and other) and API rego
		○ Apprego URI / Scope
			§ Add scope
		○ Add that scope to UI rego permission
		○ Add UI rego id to API rego 
		○ Error: 
		WWW-Authenticate: Bearer error="invalid_token", error_description="The signature is invalid"
		
![image](https://user-images.githubusercontent.com/78769/124014818-fe128f00-d9b1-11eb-8955-7fca979c81ae.png)
