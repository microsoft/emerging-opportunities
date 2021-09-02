# EventGrid? Serverless? Why?

## Backstory

**Our legacy API (Hackathon registration service)** 

### What's up? 
As more requirements were being asked the more code we shoved into our codebase. 
  - Our codebase was at a state where if we needed to add a functionality, we had to change other parts of the code that weren't even part of what we were trying to do.
  - We wanted to decouple what we currently have into separate components. Components that are essential to the business logic and components that are ad-hoc and modifiable. This removes the need to bake unneccessary code into our base business logic. We decided to take a spike and design out how we can accomplish that using out of the box Azure services.  Hello EventGrid and serverless~   
  - In hindsight I guess we got to this point because we didn't have a good design discussion when the api was being created. 
    - But I'm sure lot of shops do similar things. In order to push code out the design you think that's going to last don't really do you any good. OR you just write code without designing at all! 
- 


