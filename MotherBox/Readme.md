# MotherBox Project
[![Build Status](https://dev.azure.com/HLSHack/CSU%20Backlog/_apis/build/status/MotherBoxAPI?branchName=main)](https://dev.azure.com/HLSHack/CSU%20Backlog/_build/latest?definitionId=2&branchName=main)
MotherBox is a project name created to alert our soulutions architects to unexpected spikes (or troughs) in a customer's Azure usage.

> Go Check Out Our [Starter-Kit](https://github.com/microsoft/blazor-graphql-starter-kit) for you to try building your own Blazor/GraphQL application! 

**Azure Usage Data** is collected from various systems into an Azure SQL Datawarehouse then into Azure Data Explorer for analysis. The data source for this MotherBox project is Azure Data Explorer.

### Data Flow
Azure Data Explorer --> Azure Data Factory --> Azure HyperScale SQL DB --> PowerBI

### PowerBI
PowerBI reports in our MotherBox workspace:
- Daily trends
- Weekly trends
- Monthly trends

### Notifications
The goal for notifications is to alert our customer success team of unexpected spikes (or troughs) in Azure usage units as soon as data is available in our internal data systems . Alerts could be provided in multiple ways.

- **PowerBI:** Power BI detailed reports are aggregated to Daily, Weekly, Monthly and Yearly, focus is for detailed analysis. Measures showing Week Over Week, Month Over Month and Year Over Year. Filtered to remove units that are very minor to avoid noise.
- **Email:** Email notifications to alert the specific solutions architects assigned to specific Account, on any spikes and dips. Most of this detail is available to customers, but it can be challenging for some customers to pay attention and react to this data - especially if they are new to the cloud (or still trying to make the cloud work like their on-prem data center culture).

## MotherBox technologies: 
- Front end: Blazor
- Backend: .NET Core API / GraphQL

Concepts include:
- **Applications**: logical groupings of resources/resource groups as defined by the customer
- **Iterations**: The time-based aspect of notable events in the lifecycle of an application. (e.g. initial site migration to Azure, expanding into Asia, adding bot assistant, and even planned app decommission)

Interested in the tech side of things?

[GraphQL Learnings and snippets](./GraphQL)

[.NET Authentication with HotChocolate](../.NET/Authentication)

[Azure Data Factory setup](./Data)

[Using Banana Cake Pop](./Banana%20Cake%20Pop/Readme.md)
