# MotherBox Project
MotherBox is a project name created to alert CSAs of unexpected spikes (or troughs) in Azure usage units as soon as available in source Azure Intelligence Platform (AIP). Data is delayed by at least a week in AIP Azure Data Explorer. The PowerBI link below shows data load status.

## MotherBox Data Analytics
Create insights into customer usage and telemetry data from AIP, based on usage trends, geography and patterns in data, at customer, subscription, resource group, service type and resource level.

**Azure Usage Data** is collected from various systems into Azure SQL Datawarehouse then into Azure Data Explorer for analysis. This is managed by AIP team. The data source for this MotherBox project is Azure Data Explorer.

### Data Flow
Azure Data Explorer (AIP) --> Azure Data Factory (MotherBoxADF) --> Azure HyperScale SQL DB (MotherBoxSQLDB) --> PowerBI (AIP Daily/Weekly/Monthly/Yearly)

### PowerBI
PowerBI reports in MotherBox Workspace:
- AIP Daily
- AIP Weekly
- AIP Monthly

###Notifications
The goal for notifications is to alert CSAs of unexpected spikes (or troughs) in Azure usage units as soon as data is available in AIP ADX. Alerts could be provided in multiple ways.
- **PowerBI:** Power detailed reports are aggregated to Daily, Weekly, Monthly and Yearly, focus is for detailed analysis. Measures showing Week Over Week, Month Over Month and Year Over Year. Filtered to remove units that are very minor to avoid noise.
- **Email:** Email notifications to alert the specific CSA assigned to specific Account, on any spikes and dips. The goal is to have this notification before the change shows in Azure Portal. CSA to Account assignment will happen in an Applicaton that is not covered in this document but in another in the same Repo.

## MotherBox API **Stack**: 

- Front end: Blazor
- Backend: .NET core api / GraphQL

### Description
Internal app for sellers and sales engineers. Once the app is consented by the customers, app will help customers create logical groupings of their resources (beyond resource groups)

Ideas include:

- **Applications**: logical groupings of resources/resource groups 
- **Iterations**:


Interested in the tech side of things?

[GraphQL Learnings and snippets](./GraphQL)

[.NET Authentication with HotChocolate](./.NET)

[Azure Data Factory setup](./ADF)

[Using Banana Cake Pop](./Banana%20Cake%20Pop/Readme.md)
