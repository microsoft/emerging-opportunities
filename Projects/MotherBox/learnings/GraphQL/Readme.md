# GraphQL Learnings

## What is GraphQL?

GraphQL is a query language for APIs and a runtime for fulfilling those queries with your existing data. GraphQL provides a complete and understandable description of the data in your API, gives clients the power to ask for exactly what they need and nothing more, makes it easier to evolve APIs over time, and enables powerful developer tools. (Source: [GraphQL.org](https://graphql.org/))

## Learning Resources:

1. [Hot Chocolate v11 Documenation](https://chillicream.com/docs/hotchocolate)
2. [Getting started with GraphQL on ASP.NET Core and Hot Chocolate - Workshop](https://github.com/ChilliCream/graphql-workshop)
3. [GraphQL API with .NET 5 and Hot Chocolate](https://youtu.be/HuN94qNwQmM)
4. [Banana Cake Pop](https://github.com/microsoft/emerging-opportunities/tree/main/MotherBox/Banana%20Cake%20Pop)
5. [Blazor GraphQL Starter Kit](https://github.com/microsoft/blazor-graphql-starter-kit)

## Components that make up GraphQL:

1. Schema and Types
   1. `Query` - Query root type is used for query opperations.
   1. `Mutation` - Mutation root type is used for create, update, delete opperations.

    ###### Query & Mutation can be extended by adding the following attributes to a class definition: [ExtendObjectType(typeof(Query))] or [ExtendObjectType(typeof(Mutation))]
   
2. Startup
    1. Configure GraphQL services to be able to use the defined Schema Types: ConfigureServices() method w/ .AddGraphQLServer()
    1. Register root types and extended types need to be added using: .AddQueryType<QueryType>();

3. Authentication/Authoration
    1. [.NET Authentication with HotChocolate](https://github.com/microsoft/emerging-opportunities/tree/main/.NET/Authentication)
  
## Sample Query:
  
Sample query that will return the first record (using Paging) and also data from 2 related tables (using Projection).

Optional attributes that can be added to the definition:  [UsePaging()], [UseProjection()], [UseFiltering()] 

```GraphQL
query{
 applications(first:1){
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
   
Running the query in [Banana Cake Pop](https://github.com/microsoft/emerging-opportunities/tree/main/MotherBox/Banana%20Cake%20Pop) returns:
```GraphQL
{
  "data": {
    "applications": {
      "nodes": [
        {
          "applicationId": 1,
          "applicationName": "Sample Application",
          "businessPurpose": "Support the sales department.",
          "applicationArtifacts": [],
          "iterations": [
            {
              "iterationName": "VM Batch 1 Migration"
            },
            {
              "iterationName": "VM Batch 2 Migration"
            }
          ]
        }
      ]
    }
  }
}
```

## Mutations
 
Mutations are the equivalent to POST, PUT, PATCH and DELETE in HTTP/REST speak.  We'll use a mutations to create a new Application Artifact and return the new Artifact Id and description.
   
```GraphQL
mutation{
  addApplicationArtifact(
    description:"sample artifact"
    uRI:"http://localhost"
    applicationId:1)
    {
       applicationArtifactId
       description
    }
}   
```
  
Running the mutations returns the following:
   
```GraphQL
{
  "data": {
    "addApplicationArtifact": {
      "applicationArtifactId": 2,
      "description": "sample artifact"
    }
  }
}
```

## Variables
   
Variables can be used in place of hard coded values.  This is usefull in simulating an HTTP query string or request body.

Sample Variables in [Banana Cake Pop](https://github.com/microsoft/emerging-opportunities/tree/main/MotherBox/Banana%20Cake%20Pop)
   
![Sample Variables in Banana Cake Pop](https://github.com/microsoft/emerging-opportunities/blob/main/MotherBox/GraphQL/Variables.png)

