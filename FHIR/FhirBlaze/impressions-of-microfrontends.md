# What are microfrontends
[This video gives a fantastic introduction to microfrontends in Blazor](https://www.youtube.com/watch?v=npff2NjVXEE&list=PLdo4fOcmZ0oVWop1HEOml2OdqbDs6IlcI&index=51)

# How we used Microfrontends
We used Microfrontends to accelerate our agiligty.  In the [FhirBlaze repo](https://github.com/microsoft/FhirBlaze), the FhirBlaze project is the shell and each other project represents a Microfrontend.  
Our Blazor app [implements lazy loading](https://github.com/microsoft/FhirBlaze/blob/main/FhirBlaze/App.razor) to only load the modules required for each route.

# Our Impressions

# Our Reccomendations

# Refernce
[This article helped us decide to use Microfrontends](https://devblogs.microsoft.com/premier-developer/microfrontends-with-blazor-webassembly/)