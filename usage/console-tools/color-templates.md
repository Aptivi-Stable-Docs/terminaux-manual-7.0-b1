---
description: Colors in one group.
icon: image
---

# Color Templates

The color templates allow you to organize your colors into one group, known as a template. It allows you to group all your colors and categorize them into a template for easier organization without resorting to building your own in your application. These templates can be built from a JSON string or a file, but should be of the below format:

```json
{
    "Name": "template",
    "Components": {
        "Text": "#876543",
        "Component": "#345678",
        (...)
    }
}
```

The name and the list of components should be provided in order for the template reader to successfully parse your template and return a `TemplateInfo` class, which consists of the same read-only properties.

{% hint style="info" %}
In addition to having these two properties being set, you must implement at least the following components:

* `Text`: Neutral text color
{% endhint %}

The template reader function to parse your template JSON files is `GetTemplateFromJson()` that takes template JSON strings. You'll have to manually read the contents of the template file using `File.ReadAllText()` before using this function.

After you get a `TemplateInfo` class instance, you can use that to register it to the template manager. This way, you've added your template. This means that you can set it as a default template so that all of the functions that use your default template, such as `GetColor()`, can use it to get the colors from the template components.

You can also get a JSON representation of your template using `GetTemplateToJson()` to be able to save them to files for later use. You can also make your own template by calling a constructor of `TemplateInfo`.

## Examples

Here are the examples of how you can use this feature. Please note that these examples are sequential and don't work independently.

### Registering the template from info

{% code lineNumbers="true" %}
```csharp
// Custom template
var template = new TemplateInfo(name, new()
{
    { "Text", new("#876543") },
    { "Component", new(168555) },
});
TemplateTools.RegisterTemplate(template);
```
{% endcode %}

### Registering the template from JSON

{% code lineNumbers="true" %}
```csharp
// Custom template
string templateJson =
    $$"""
    {
        "Name": "{{name}}",
        "Components": {
            "Text": "#876543",
            "Component": "#345678"
        }
    }
    """;
var template = TemplateTools.GetTemplateFromJson(templateJson);
TemplateTools.RegisterTemplate(template);
```
{% endcode %}

### Setting the template as default

{% code lineNumbers="true" %}
```csharp
TextWriterColor.WriteColor("[Before - {0}] Hello world!", true, TemplateTools.GetColor(PredefinedComponentType.Text), TemplateTools.Exists(name));
TemplateTools.SetDefaultTemplate(name);
TextWriterColor.WriteColor("[After - Text] Hello world!", true, TemplateTools.GetColor(PredefinedComponentType.Text));
TextWriterColor.WriteColor("[After - Component] Hello world!\n", true, TemplateTools.GetColor("Component"));
```
{% endcode %}

### Unregistering a template

{% code lineNumbers="true" %}
```csharp
TextWriterColor.WriteColor("\n[Reset - {0}] Hello world!", true, TemplateTools.GetColor(PredefinedComponentType.Text), TemplateTools.Exists(name));
TemplateTools.UnregisterTemplate(name);
TextWriterColor.WriteColor("[Reset - {0}] Hello world!\n", true, TemplateTools.GetColor(PredefinedComponentType.Text), TemplateTools.Exists(name));
```
{% endcode %}
