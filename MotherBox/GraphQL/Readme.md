# GraphQL Learnings

## What is GraphQL?

GraphQL is a query language for APIs and a runtime for fulfilling those queries with your existing data. GraphQL provides a complete and understandable description of the data in your API, gives clients the power to ask for exactly what they need and nothing more, makes it easier to evolve APIs over time, and enables powerful developer tools. (Source: [GraphQL.org](https://graphql.org/))

## Learning Resources:

1. [Getting started with GraphQL on ASP.NET Core and Hot Chocolate - Workshop](https://github.com/ChilliCream/graphql-workshop)
2. [GraphQL API with .NET 5 and Hot Chocolate](https://youtu.be/HuN94qNwQmM)

## Components that make up GraphQL:

1. Schema and Types
   1. `Query` - Query root type is used for query opperations.
   1. `Mutation` - Mutation root type is used for create, update, delete opperations.

    ###### Query & Mutation can be extended by adding the following attributes to a class definition: [ExtendObjectType(typeof(Query))] or [ExtendObjectType(typeof(Mutation))]
   
2. Startup
    1. Configure GraphQL services to be able to use the defined Schema Types: ConfigureServices() method w/ .AddGraphQLServer()
    1. Register root types and extended types need to be added using: .AddQueryType<QueryType>();

3. Authentication/Authoration
    1. [.NET Authentication with HotChocolate](../.NET)
  
## Sample Query/Mutations:
  
  ```GraphQL
  query{
    applications(first:30){
      nodes{
        applicationId
        applicationName
        businessPurpose
        applicationArtifacts{uRI}, 
        iterations{iterationName}
      }
    }
  }
  ```
