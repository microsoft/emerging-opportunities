# Connecting to FHIR
Healthcare devs are increasingly building apps that work against HL7 fhir APIs.

Whether you're exploring FHIR or writing an application to interact with FHIR you're going to need to connect.
In our experience it's easier to explore by developing a simple app rather than directly calling the API through Postman. Auth and complex request/response payloads make Postman a cumbersome option.
Refernce: [Connecting via Postman](https://docs.microsoft.com/en-us/azure/healthcare-apis/azure-api-for-fhir/access-fhir-postman-tutorial#inserting-a-patient)

## Our requirements
When we work with FHIR we only work with authentication and authorization.  In the samples below we require auth from the start.
We want to offer options in multiple languages with and without libraries.

## Languages used in this sample
We created [fhir-blaze](https://github.com/microsoft/FhirBlaze) to demo a FHIR webapp using Blazor Web Assembley for dotnet.  This sample is a frontend engine, but the code samples below should also work on a server side app. 
The languages we prodovide samples for are: 
* .NET C#
* Javascript

# Patterns
We have included the following patterns to connect to a FHIR API.
* [HTTP Client](#http-client)
* [Firely .NET SDK](#firely-net-sdk)
* [FHIR.js](FHIR.js)

NuGet Packages Required:
* Microsoft.Authentication.WebAssembly.MSAL
* Microsoft.Extensions.Http  

## HTTP Client
The advantage of this approach is that you're only using 1st party code (the dotnet core, MSAL, and HTTP libraries).
1. Setup MSAL.
With this code your app can now authenticate against Azure Active Directory. 
```dotnet
Program.cs

 builder.Services.AddMsalAuthentication(options =>
  {
	  builder.Configuration.Bind("AzureAd", options.ProviderOptions.Authentication);
      options.ProviderOptions.DefaultAccessTokenScopes.Add(fhir.Scope);
  });
```
2. Create an HTTP Client with a HTTP Message Handler.
The HTTP Message handler will intercept requests and fetch a token with the required scope when the authorized url are called.
```dotnet
 builder.Services.AddHttpClient<IFHIRBlazeServices, FHIRBlazeServices>
    (s =>
        s.BaseAddress = new Uri(fhir.FhirServerUri))
        	.AddHttpMessageHandler(sp => sp.GetRequiredService<AuthorizationMessageHandler>()
        		.ConfigureHandler(
                	authorizedUrls: new[] { fhir.FhirServerUri },
                	scopes: new[] { fhir.Scope }));

```
3. That's it!  Now you can make any FHIR REST call without having to worry about authorization.
[Example in FHIRBlaze](https://github.com/microsoft/FhirBlaze/blob/c6fe1acae9d148355c898187874c01181f36bad3/FhirBlaze/Program.cs#L35)

## Firely .NET SDK
The Firely library can help you get started quickly. 
The library provides:
* Class models for working with the FHIR data model using POCOs
* A REST client for working with FHIR-compliant servers
* Xml and Json parsers and serializers
* Helper classes to work with the specification metadata, and generation of differentials
* Validator to validate instances against profiles
* A lightweight in-memory terminology server

[Read the docs](https://docs.fire.ly/projects/Firely-NET-SDK/index.html) for more information, or to get started using Firely in your own application.

### Configuring Firely
NuGet Packages Required:
* Microsoft.Authentication.WebAssembly.MSAL
* Microsoft.Extensions.Http  
* HL7.Fhir.R4

In the FHIRBlaze app, we wanted to register the Firely REST client with Dependency Injection so that it will be easy to configure once and then reuse within our Blazor components. Here are the steps we used to configure and register the client:
1. Setup MSAL for Authentication and Authorization with Azure AD 
```csharp
builder.Services.AddMsalAuthentication(options =>
{
  options.ProviderOptions.DefaultAccessTokenScopes.Add("https://your-fhir-api.azurehealthcareapis.com/user_impersonation");

  builder.Configuration.Bind("AzureAd", options.ProviderOptions.Authentication);
});
```
2. Configure the Firely FHIRClient for authentication
```csharp
builder.Services.AddScoped<FhirClient>(o =>
{
    var settings = new FhirClientSettings
    {
        PreferredFormat = ResourceFormat.Json,
        PreferredReturn = Prefer.ReturnMinimal
    };
    var handler = o.GetRequiredService<AuthorizationMessageHandler>()
        .ConfigureHandler(
            authorizedUrls: new[] { "https://your-fhir-api.azurehealthcareapis.com" },
            scopes: new[] { "https://your-fhir-api.azurehealthcareapis.com/user_impersonation" }
        );
    handler.InnerHandler = new HttpClientHandler();
    return new FhirClient("https://your-fhir-api.azurehealthcareapis.com", settings, handler);
});

builder.Services.AddScoped<IFhirService, FirelyService>();
```
3. That's it! Any component that requests the `IFhirService` interface via dependency injection will now receive the configured instance of our `FirelyService`.

To streamline and consolidate your startup code, you can move the above steps to an extension method. You can see examples of this in the FHIRBlaze app.
* [Program.cs](https://github.com/microsoft/FhirBlaze/blob/2649937d591368834fb5e8872cb07987c8cfb032/FhirBlaze/Program.cs#L43)
* [FhirServiceExtensions.cs](https://github.com/microsoft/FhirBlaze/blob/main/FhirBlaze/FhirServiceExtensions.cs)

## Fhir.js
1. Setup AddMsalAuthentication
2. Setup fhir Client
Sample code at [FHIR-React](TODO)

# What's Next
Now you should explore FHIR more and make your own app!
