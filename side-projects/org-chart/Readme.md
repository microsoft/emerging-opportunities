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

## Iteration 1 Steps
1. **Create canvas Power App.**

There's nothing fancy needed here - just a blank canvas app. I chose tablet/desktop format because I belong to a large organization!

3. **Add connection to Graph.**
 
In the left navigation pane, click **Data**, **Add Data**, and then search for "Office 365 Users" and add a connection to it.

4. **Add a button.** 

I use a refresh/load button to initiate the call to the Office 365 Users connector. I put this in the bottom left-corner where it is least likeliest to overlap my data later.

6. **Set the button's OnSelect formula.** 

```
ClearCollect(varOrg, Office365Users.DirectReportsV2("mymanager@microsoft.com")`
```

When the button is clicked, this formula creates a variable called varOrg. It then retrieves the direct reports for the specified email address from the Microsoft Graph and assigns the results of that API call to the variable.

5. **Add a gallery control.**

From the **Insert** menu, select **Gallery** and then **Blank vertical**. Position the gallery as desired.

6. **Set the gallery's Items formula.**

```
varOrg`
```

This is pretty simple. We are just binding the results of our Graph API call to the gallery.

6. **Add image to template.**

With the item template of the gallery control selected, from the **Insert** menu, select **Media** and then **Image**.

7. **Set the image's Image formula.**

```
If(!IsBlank(ThisItem.upn), 
    Office365Users.UserPhotoV2(ThisItem.upn)
)
```

8. **Run the app!**

Run the app in 'play' mode, click your button and watch the pretty pictures of people come in.

## Iteration 2 Steps
All of the above will get you to a working app, but if your organization is 800+ people like mine, then you have a bit more work to do. :)

1. **Fetch organization hierarchy.**

I first thought about doing this in Power Automate, but my Flow timed out due to organization size. :( So, I went back to Power Apps and set my button's OnSelect formula to the following.

```
Clear(varLevel1Directs);
Clear(varLevel2Directs);
Clear(varLevel3Directs);
Clear(varLevel4Directs);

ClearCollect(varPattysDirects, 
    RenameColumns(Distinct(Office365Users.DirectReportsV2("mymanager@microsoft.com", {'$select': "userPrincipalName"}).value, userPrincipalName), "Result", "upn0"));
ForAll(varPattysDirects, 
    Collect(varLevel1Directs, 
        RenameColumns(Distinct(Office365Users.DirectReportsV2(upn0, {'$select': "userPrincipalName"}).value, userPrincipalName), "Result", "upn1"));
);
ForAll(varLevel1Directs, 
    Collect(varLevel2Directs, 
        RenameColumns(Distinct(Office365Users.DirectReportsV2(upn1, {'$select': "userPrincipalName"}).value, userPrincipalName), "Result", "upn2"));
);
ForAll(varLevel2Directs, 
    Collect(varLevel3Directs, 
        RenameColumns(Distinct(Office365Users.DirectReportsV2(upn2, {'$select': "userPrincipalName"}).value, userPrincipalName), "Result", "upn3"));
);
ForAll(varLevel3Directs, 
    Collect(varLevel4Directs, 
        RenameColumns(Distinct(Office365Users.DirectReportsV2(upn3, {'$select': "userPrincipalName"}).value, userPrincipalName), "Result", "upn4"));
);
    
ClearCollect(varEou, RenameColumns(varPattysDirects, "upn0", "upn"));
Collect(varEou, RenameColumns(varLevel1Directs, "upn1", "upn"));
Collect(varEou, RenameColumns(varLevel2Directs, "upn2", "upn"));
Collect(varEou, RenameColumns(varLevel3Directs, "upn3", "upn"));
Collect(varEou, RenameColumns(varLevel4Directs, "upn4", "upn"));

RemoveIf(varEou, Office365Users.UserPhotoMetadata(upn).HasPhoto = false);
```

2. **Wrap images**

A gallery control allows you to display it's items vertically or horizontally - or both! Select your gallery control and, in the right pane, change the **Wrap Count** to 10.

3. **Display even more images!**


