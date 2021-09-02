# EventGrid? Serverless? Why?

## Our Story

**Our legacy API (Hackathon registration service)** 

As more requirements were being asked the more code we shoved into our codebase. Our codebase was at a state where we had to change other parts of the code that were unneccesary when we try add a functionality. 

We want to decouple what we currently have into separate _components_. Components that are essential to the business logic and components that are ad-hoc and modifiable. This removes the need to bake unneccessary code into our base business logic. We decided to take a spike and design out how we can accomplish that using out of the box Azure services.  

## What does this have to do with me?

Though above is a small example we believe componentizing your architecture is a big step towards modernizing your architecture. 

We as developers believe in [Clean Code](https://dev.to/danialmalik/a-brief-guide-to-clean-code-functions-104h#:~:text=A%20Brief%20Guide%20to%20Clean%20Code%3A%20Functions%201,of%20the%20system%20while%20classes%20are%20the%20nouns.). We have to think software architecture, similarly. Each small components doing only what they are supposed to and pass it along to another. This helps us to architect cleaner and sensible solutions in the cloud. 

So, whether you are already on the cloud or thinking of modernizing your current architecture this article will hopefully give you a decent grasp of how you can go about approaching it the right way. 

## Options Options Options

### App Service
One of the quickest way to modernize your software is using App Service. VM is of course another route but going back to our reasoning we want to make sure things are small and manageable. This way you allow Azure to handle all the networking and security for you. Here are some great ways to secure your App Services! 
- [App Service Private Endpoint](https://docs.microsoft.com/en-us/azure/app-service/networking/private-endpoint)
- [App Service Access Restriction](https://docs.microsoft.com/en-us/azure/app-service/app-service-ip-restrictions)
- [App Service Environment](https://docs.microsoft.com/en-us/azure/app-service/environment/intro)

You can either host all your messy application in the App Service, OR you can refactor like mentioned above and put them into separate App Services and this gets into the territory of [Microservices](https://www.martinfowler.com/microservices/).

Did we mention the cost can be significantly cheaper?

### Serverless 
One step further than an app service route is the Serverless ([Azure Functions](https://docs.microsoft.com/en-us/azure/azure-functions/functions-overview))route. This is where Azure dynamically manages the allocation and provisioning of servers. All the benefit of the App Service but with added bonus of being only charged when it's invoked. Scott Guthrie calls it the '_invocation model_' where you are only responsible for chargers when the resource is called.

Now... the fun(?) part!

### Events and Messages 


![eventgrid_diagram](./images/diagram.png)

### Lesson to be learnt
In hindsight I guess we got to this point because we didn't have a good design discussion when the api was being created. But I'm sure lot of development shops do similar things. In order to push code out the design you think that's going to last don't really do you any good. OR you just write code without designing at all! 


