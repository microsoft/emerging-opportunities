# Recursively Create Blazor Component

Rendering a Questionnaire(link) component isn't as simple as creating a normal HTML form as each Item(link) component can both be a parent element or a child element. 

Item can be a type of string, textarea, choice, bool, date... etc.... These are easy enough. But an Item can also be a type of Group, which can have the usual types mentioned before AND zero or more Group type.

This makes the rendering of Questionnaire's json object a little bit tricky.

## RenderFragments


## Recursion to save the day

What we've come up with was combine RenderFragments and recursion to keep on traversing go down the tree until it finds an item type that is not of Group. Then render from bottom up.

Appending to our RenderFragment along the way.

`protected override async Task OnInitializedAsync()
        {
            try
            {
                RenderComponent(QResponse.Item);
                .
                .
                
`

