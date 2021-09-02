# EventGrid? Serverless? Why?

## Our Story

**Our legacy API (Hackathon registration service)** 

As more requirements were being asked the more code we shoved into our codebase. Our codebase was at a state where we had to change other parts of the code that were unneccesary when we try add a functionality. 

We want to decouple what we currently have into separate _components_. Components that are essential to the business logic and components that are ad-hoc and modifiable. This removes the need to bake unneccessary code into our base business logic. We decided to take a spike and design out how we can accomplish that using out of the box Azure services.  

## What does this have to do with me?

We believe componentizing your architecture is a big step towards modern architecture. Just as us developers believe in clean code (aka. [smaller functions](https://dev.to/danialmalik/a-brief-guide-to-clean-code-functions-104h#:~:text=A%20Brief%20Guide%20to%20Clean%20Code%3A%20Functions%201,of%20the%20system%20while%20classes%20are%20the%20nouns.)) we believe we have to think of our software architecture similarly. Each small components doing only what they are supposed to and pass it along to another at.   you decouple and refactor your code 
**Refactoring and Modernizing On-Prem services**
Whether you are on a cloud already or thinking of modernizing your current architecture this article will hopefully give you a decent grasp of how you can go about doing it. 

### So what do we do? 

### Hello EventGrid and Serverless

![eventgrid_diagram](./images/diagram.png)

### Lesson to be learnt
In hindsight I guess we got to this point because we didn't have a good design discussion when the api was being created. But I'm sure lot of development shops do similar things. In order to push code out the design you think that's going to last don't really do you any good. OR you just write code without designing at all! 


