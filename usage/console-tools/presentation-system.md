---
description: Presenting your things to the kernel!
icon: presentation-screen
---

# Presentation System

This API provides you the presentation system used for presenting something to your users in the full-screen view. It's like a presentation in steroids.

## How to present

To present your presentation to your users, you must implement a `Presentation` class instance, which must assign the following variables in the constructor:

* `Name`
  * Presentation name
* `Pages`
  * Presentation pages (List of `PresentationPage` instances)

To implement the `PresentationPage` instances, you must call its constructor with the following variables:

* `Name`
  * Presentation page name
* `Pages`
  * Presentation page elements (List of `IElement` instances)

To implement the page elements, make new instances of the elements. Base elements that Nitrocid KS implements are:

* `TextElement`
  * Static text.
  * The first argument in the element `Arguments` is the string to be printed.
* `DynamicTextElement`
  * Dynamic text.
  * The first argument in the element `Arguments` is the action to which it generates the string, for example, `TimeDateRenderers.Render()`.

{% hint style="info" %}
You can also make your custom `IElement` in your code, and no registration is needed.
{% endhint %}

### Controls

The presentation viewer has the following controls:

* `ENTER` / `Left-click (mouse)`
  * Advances to the next page
* `ESC`
  * Bails out from the presentation
  * Has no effect on kiosk and modal presentations

### Input

In addition to the presentation elements, you can also add input to your presentation to interact with your users more. Just create a new instance of the `PresentationInputInfo` class and provide the title, the description, and a new instance of the input module class that implements the `InputModule` class.

```csharp
internal static PresentationInputInfo input =
    new("Second multiple choice", "Asks the user to select one or more of the names (larger)",
        new MultiComboBoxModule()
        {
            Name = "Second multiple choice",
            Description = "Ultricies mi eget mauris pharetra sapien et ligula:",
            Choices = GetCategories(data2)
        }, true
    );
```

Then, in the `PresentationPage` constructor, you must add your input instance to the second argument that represents an array of `InputInfo` class instances, like this:

```csharp
new PresentationPage("Fifth page - Debugging choice input",
    [
        new TextElement()
        {
            Arguments = [
                "Tincidunt nunc pulvinar sapien et ligula ullamcorper malesuada proin."
            ]
        },
    ],
    [
        input2,
        input3,
    ]
),
```

{% hint style="info" %}
In order to be able to get the input, it's recommended to put the `PresentationInputInfo` instances in their own variables so that you can act according to the input value.

You can also specify whether the input is required in the constructor. Currently, the input is not required, but you can pass `true` to the fourth argument to make it required, such as in the example above.
{% endhint %}

The presentation system checks the page to see if there are any input instances. If true, you'll be presented with an informational box telling you to select an input to fill. The asterisk next to the number denotes the required input. This means that users should fill in such input before being able to go on. Those without the asterisk means that it's fully optional.

{% hint style="info" %}
To learn more about input modules, consult the below page:

<a href="../input-reader/other-input/input-modules.md" class="button primary">Input Modules</a>
{% endhint %}

### Appearance

You can customize how your slideshow looks using the following properties:

* `BorderSettings`: Customizes your presentation's borders
* `FrameColor`: Customizes your presentation's border frame color
* `BackgroundColor`: Customizes your presentation's background color
