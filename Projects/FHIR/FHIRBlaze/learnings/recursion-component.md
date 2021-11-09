This article is written by Microsoft's Cloud Solution Architects: [@Sameer-Doshi](https://github.com/SameerDoshi) and [@Daniel-Kim](https://github.com/i-am-dan)

# Recursively Create Blazor Component

Rendering a [Questionnaire](https://www.hl7.org/fhir/questionnaire.html) component isn't as simple as creating a normal HTML form as each [Item](https://www.hl7.org/fhir/questionnaire-definitions.html#Questionnaire.item) component can both be a parent element or a child element. 

Item can be a type of string, textarea, choice, bool, date... etc.... These are easy enough. But an Item can also be a type of Group, which can have the usual types mentioned before AND zero or more Group type.

This makes the rendering of Questionnaire's json object a little bit tricky.

## [RenderFragments](https://www.syncfusion.com/faq/blazor/components/how-do-you-create-elements-dynamically-in-blazor)

It's a concept of Templated Controls. Using RenderFragments you can componentize specific portion of HTML. A `RenderFragment` represents a chunk of Razor markup that can then be rendered by the component

## Recursion to save the day

What we've come up with was combine RenderFragments and recursion to keep on traversing go down the tree until it finds an item type that is not of Group. Then we'll use the recursive function to append to our RenderFragment along the way.

On the front end:

``` C#
// HTML/Blazor Front end
<EditForm Model=@QResponse OnSubmit=@SubmitQuestionnaireAsync>
   @DynamicFragment
   .
   .
</EditForm>

// Frontend @code block
private RenderFragment DynamicFragment;
private void RenderComponent(List<ItemComponent> items)
{
    DynamicFragment += GetChildItems(items);       
}

private RenderFragment GetChildItems(List<ItemComponent> items) => __builder =>
{
    @foreach (var item in items)
    {
        @if (item.Item.Count > 0)
        {
            @GetTitle(item.Text);
            @GetChildItems(item.Item);
        }
        else
        {
            @GetAnswerDisplay(item);
        }
        <br/>
    }
};
```

As you can see we have a `DynamicFragment` inside the `EditForm` element. That is a render fragment that we'll be using the build form.

We have two key functions: `RenderComponent` and `GetChildItems`. First function updates the `RenderFragments` with html elements spewed by the second funtion.

Second function is the recursive function that goes through all the Questionnaire items and determines whether it should render an HTML element. If it finds the Item contains another Item with a count greater than 0 we know the type is of 'Group'. The recursion starts again.

**How do you kick off the render?**

On the code behind:

``` C#
protected override async Task OnInitializedAsync()
{
  try
  {
    RenderComponent(QResponse.Item);
    .
    .
}
```

During initialization you can simply call our first function `RenderComponent` with all the Questionnaire items!

_We hope this helps you as you try to tackle the complexity of Questionnaire component of FHIR._


