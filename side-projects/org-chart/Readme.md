# Power OrgChart
Initially, I thought this would be a very trivial effort. I'd create a PowerApp that crawls through Active Directory and scrapes photos of all employees under a specific person. The following is a recount of my actual adventure through the still primordial world of low-code.

## Graph API
The one thing I knew I wanted to use for my data source was the Microsoft Graph API. (I kinda hate this name because 'Graph' is too vague.) The Microsoft Graph API does a lot of things, but I knew it was a trusted data source for our organization hierarchy. This data already shows up in places like Outlook and Microsoft Teams.
<div>
  <img src="https://github.com/microsoft/emerging-opportunities/blob/main/side-projects/org-chart/OutlookOrgChartExample.png" height="200" />
  <img src="https://github.com/microsoft/emerging-opportunities/blob/main/side-projects/org-chart/TeamsOrgChartExample.png" height="200" />
 </div>

## Power App
Now I needed a presentation UI. For seemingly simple projects like this, I always default to Power Apps. And since I know there's already a Power Apps Graph Connector, I figured this would be straightforward - and for the most part, it was.
