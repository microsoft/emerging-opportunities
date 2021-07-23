# Side Projects

In this folder you will find some of our one-off projects.

### [**PowerOrgChart**](./org-charg)

We've all seen the slide deck in a quarterly kickoff or other corporate presentation that shows the little pictures of all of the people on the team. This can be a great way to show appreciation for people in our new virtual setting and to help communicate the size and scale of a large organization. When you do this with a team of five people, it's not too hard to just drag pictures from a folder onto a PowerPoint deck, but when your organization is hundreds of people, this too often becomes an administrative assistant's entire weekend! This is the problem I was asked to solve this week.

Initially, I thought this would be a very trivial effort. I'd create a PowerApp that crawls through Active Directory and scrapes photos of all employees under a specific person. The following is a recount of my actual adventure through the still primordial world of low-code.

# Graph API
The one thing I knew I wanted to use for my data source was the Microsoft Graph API. (I kinda hate this name because 'Graph' is too vague.) The Microsoft Graph API does a lot of things, but I knew it was a trusted data source for our organization hierarchy. This data already shows up in places like Outlook and Microsoft Teams.

# Power App
