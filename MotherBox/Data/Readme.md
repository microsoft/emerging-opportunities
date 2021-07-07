
## Overview
The Motherbox application is composed of a couple of key artifacts that are responsible for
sourcing, processing and landing data from the AIP system:

- Azure Data Factory
- Azure KeyVault
- Azure SQL Database (Hyperscale)

In this section will provide an overview of how the application is architected and built.

### Data Overview
Motherbox data is stored in a traditional star schema. There's are two fact tables that store current year (GlobalUsageDaily) and previous year (GlobalUsageDailyPrevYear) usage data. Supporting these tables are four dimension tables for Customer, Subscription, Service Hierachy and Date data.

<img src="SQL_Data_Model.png" alt="SQLDB Model Overview" width="400"/>

Given the large dataset, the database is built on Azure SQLDB HyperScale. The database is dynamically scaled up just before the data load in order to minimize load times and then when the load is complete it's scaled back down.

### Security
All credentials used by ADF to connect to the AIP system as well to the database are stored in Azure Keyvault. Azure Managed Identities are used to grant ADF permissions to manage Azure resources as needed.

### ADF Overview
The data is extracted from the AIP system using Kusto queries and it's initially stored in staging tables on the Azure SQLDB database. The data is then aggregated and moved to the final tables. This task is accomplished by an ADF job that's implemented as a series of pipelines. The core/master pipeline is designed as follows:

<img src="ADF_Pipeline_Overview.png" alt="ADF Master Pipeline Overview" width="400"/>

### Azure DevOps Overview

In order to simplify the deployment and operational maintenance, we built an Azure Devops
pipeline that deploys changes committed to the git repository. We built a multi-stage pipeline
that builds out the complete infrastructure.The overview below shows the various tasks used to build out the pipeline.

<img src="DevOps_Pipeline_Overview.png" alt="DevOps Pipeline Overview" width="400"/>