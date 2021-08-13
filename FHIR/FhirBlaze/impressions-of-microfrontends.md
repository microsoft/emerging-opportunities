# What are MicroFrontends
[This video gives a fantastic introduction to microfrontends in Blazor](https://www.youtube.com/watch?v=npff2NjVXEE&list=PLdo4fOcmZ0oVWop1HEOml2OdqbDs6IlcI&index=51)

# How we used MicroFrontends
We used MicroFrontends to accelerate our agiligty.  In the [FhirBlaze repo](https://github.com/microsoft/FhirBlaze), the FhirBlaze project is the shell and each other project represents a Microfrontend.  
Our Blazor app [implements lazy loading](https://github.com/microsoft/FhirBlaze/blob/main/FhirBlaze/App.razor) to only load the modules required for each route.

# Our Impressions
We did not see much value from microfrontends _in this project_. 

## Parallel Development
For ease of sharing, we structured all content into one solution, one repositoty. Because we're using git everyone was able to work at once, but didn't see any parallel development benfits beyond what we got from git.  In a highly microfrontend development environment each module would have been its own solution- allowing a team to build/debug/publish a single small project.  Contrast this to our a]roach, in which every dev had to build/debug/run all modules.

## Modularity
In this app, all components had a common backend and a connector to that backend.    Because of this we ended up with [a Shared Component](https://github.com/microsoft/FhirBlaze/tree/main/FhirBlaze.SharedComponents) that is required for all components to work.  Contrast this with a microfrontend in which product data is in a backend, patient information is in another backend, provider locations are in another location, and billing information is in another location.   In this case- none of the microfrontends representing billing, patient, provider, and product need to share any libraries or connections. 

# Our Recommendations

* MicroFrontends accelerating parallel development.  If you won't have many teams working at once consider not using a Microfront end approach.  If or if 
* Microfrontends work well with modular or micro-serviced backends.  If your app has many common, or shared dependencies then a microfrontend will provide you little value.
* Microfront ends with Blazor need to be in multiple solutions and multiple repositories.
* The App Shell needs to have strict contracts- don't have an intelligent App Shell for some components and a dumb shell for others
* Microfront ends will show little benefit for less than 3 teams

# Reference
[This article helped us decide to use Microfrontends](https://devblogs.microsoft.com/premier-developer/microfrontends-with-blazor-webassembly/)

