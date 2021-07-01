# Authentication Learnings

During our sprint we were tasked to create an app that involved _.NET Core Api, Entity Framework, and GraphQL_ (ChilliCream's HotChocolate)

Because this app dealt with sensitive data Authentication and Authorization were key to making this secure.

I have followed tutorials here and there in the past but never really had to understand as deep as I need to now. 

First step we tried was adding EasyAuth to our azure resource (web app or functions)

### Application Registration

Application Registration is one of the most fundamental resource you should understand if you want to have any access and authentications enabled for your azure resources. 

I've written a [blog](https://www.linkedin.com/pulse/azure-app-registration-service-principal-daniel-kim/) in LinkedIn trying to explain what it is (in relation to service principal) how AAD's service principal uses it to give access to resources/users 

Here's the [**official doc**](https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app) on what an app registration is.

> I found this [**video**](https://www.youtube.com/watch?v=YWvl0cIilyA) to also be really helpful More thorough explanation on Azure App Registration
 
 
### Authentication / Authorization

In layman's term:

- **Authentication** (ID Token) - Used to give entry to a resource based on the credentials users provide. (There are of course times when an app will authenticate, like a daemon.)

- **Authorization** (Access Token) - Used to determine what access level a user/ an app has.


AAD uses JWT token to authenticate and authorize users. When your api (or any application) receives the JWT token, it can be used to authenticate (allows entry to resources), then it'll be used to determine authorization level (allows or disallows certain access level on the resources). It will also have information on how long this token lasts.

Resource: 

[**Id Token / Access Token Explanation**](https://www.youtube.com/watch?v=sICt5aS7wzk)

## Multiple Options 

- **EasyAuth**
- **Code** (handle auth/authorization inside the code)

### EasyAuth route

**What is this?** It's leveraging the portal to enable authentication for Functions, Web apps and other resources that has easy auth capability. This way the service that hosts our apps will handle the authentication for us and allow users to access our app. You'll still need to create an app registration for this to work. (_If you don't have an app registration, you can tell the portal to create the app registration for you_)

Official doc on how to use [**Azure's built in authentication**](https://docs.microsoft.com/en-us/azure/app-service/overview-authentication-authorization#:~:text=Azure%20App%20Service%20provides%20built-in%20authentication%20and%20authorization,and%20mobile%20back%20end%2C%20and%20also%20Azure%20Functions)

**Issues** 

Graphql and EasyAuth: **SPA** (single page applications) require specific header variables when using OAuth2.0 flow. And we do not have a way of accessing how GraphQL submits it's header

As we were leveraging the EasyAuth, we ran into an issue with GraphQL not being nice with the EasyAuth.  HotChocolage (and other GraphQL)libraries ([What is HotChocolate](https://chillicream.com/docs/hotchocolate/)?) have an UI application called 'Playground' that can be accessed through an endpoint. Developers can use that to checkout the schema and test out queries. 

EasyAuth uses OAuth2.0 (OpenID) to authenticate users. Since Playground is a spa, you'd need to send certain values in the request header to by pass CORS error. However, since graphql is making a request on behalf of us, we had no way of manipulating the header request to make our oauth2 workflow work. [Reference on spa and oauth2 flow](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-oauth2-auth-code-flow#redirect-uri-setup-required-for-single-page-apps)

### Code route 

Postman and Web Api

> If you have **multifactor** enabled for your account, you MUST use (Authorization Code with PKCE)


