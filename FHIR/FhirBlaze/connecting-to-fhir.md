# Connecting to FHIR from dotnet
Healthcare devs are increasingly building apps that work against HL7 fhir APIs.

Whether you're exploring FHIR or writing an application to interact with FHIR you're going to need to connect.
In our experience it's easier to explore by developing a simple app rather than directly calling the API through Postman. Auth and complex request/response payloads make Postman cumberome option.
Refernce: [Connecting via Postman](https://docs.microsoft.com/en-us/azure/healthcare-apis/azure-api-for-fhir/access-fhir-postman-tutorial#inserting-a-patient)

## Our requirements
When we work with FHIR we only work with authentication and authorization.  In the samples below we require auth from the start.
We want to offer options in multiple languages with and without libraries.

## Languages used in this sample
We created [fhir-blaze](https://github.com/microsoft/FhirBlaze) to demo a FHIR webapp using Blazor Web Assembley for dotnet.  This sample is a frontend engine, but the code samples below should also work on a server side a]. 
The languages we prodovide samples for are: 
* dotnet
* Javascript

# Methods
NuGet Packages Required:
* Microsoft.Authentication.WebAssembly.MSAL
* Microsoft.Extensions.Http  

We have included the following methods to connect to a FHIR API.
* [HTTP Client](HTTP Client)
* [FHIRClient Fhirly Library](FHIRClient Fhirly Library)
* [FHIR.js](FHIR.js)

## HTTP Client ##
The advantage of this approach is that you're only using 1st party code (the dotnet core, MSAL, and HTTP libraries).
1. Setup MSAL.
With this code your app can now authetnicate against Azure Active Directory. 
```dotnet
 builder.Services.AddMsalAuthentication(options =>
  {
	  builder.Configuration.Bind("AzureAd", options.ProviderOptions.Authentication);
      options.ProviderOptions.DefaultAccessTokenScopes.Add(fhir.Scope);
  });
```
2. Create an HTTP Client with a HTTP Msssage Handler.
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
[Example in FHIRBlaze](https://github.com/microsoft/FhirBlaze/commit/c6fe1acae9d148355c898187874c01181f36bad3#diff-19e6dcfee81101f9a4641a689f66f4a2b124d766dc415bc625605c36875d3fc3)

## FHIRClient Fhirly Library
The Fhirly client does things like out of box deserialization and pagination support.

NuGet Packages Required:
* Microsoft.Authentication.WebAssembly.MSAL
* Microsoft.Extensions.Http  
* HL7.Fhir.R4

* Microsoft.Authentication.WebAssembly.MSAL
* Microsoft.Extensions.Http  

1. Setup MSAL
2. Create a FHIR Extension
3. Add the FHIR Client to your app.
Sample code at the [FHIRBlaze project](https://github.com/microsoft/FhirBlaze/blob/main/FhirBlaze/Program.cs)
## Fhir.js
1. Setup AddMsalAuthentication
2. Setup fhir Client
Sample code at [FHIR-React](TODO)

# What's Next
Now you should explore FHIR more and make your own app!
