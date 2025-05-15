---
description: We need to highlight things to make them easier to find.
icon: flashlight
---

# Syntax Highlighting

Syntax highlighting is commonly found in code editors, code viewers, and some shells, such as zsh. We believe that syntax highlighting makes it easier to distinguish between parts of text, making it easier to read and understand the whole text, especially if you're reading a codebase, such as Terminaux's source code.

Syntax highlighting is also available on vim for code files and for configuration files for the same reason. As a result, Terminaux also provides syntax highlighting in your prompt to make the text that you've written easier to read and understand.

{% hint style="info" %}
To try this feature out, you can execute the console demo of Terminaux, passing the `PromptHighlighted` argument.
{% endhint %}

The syntax highlighting tools provide you with functions to manage your highlighters, including registering them after getting an instance of the highlighter from its JSON representation that looks like the following:

{% code title="Minimum JSON" lineNumbers="true" %}
```json
{
    "Name": "custom",
    "Components": {
        "FirstWord": {
            "ComponentMatch": "/(?:^|(?:[.!?]\\s))(\\w+)/",
            "ComponentForegroundColor": "#00FF00",
            "ComponentBackgroundColor": "#000000",
        }
    }
}
```
{% endcode %}

All of your highlighters must follow this convention above to make a useful highlighter for your syntax. If done correctly, you must be able to get a registerable instance of a `SyntaxHighlighting` instance.

Registering this instance require making either a JSON file that contains the above syntax highlighter properties, or a JSON string variable, such as in [this demo's source code](https://github.com/Aptivi/Terminaux/blob/main/Terminaux.Console/Fixtures/Cases/PromptHighlighted.cs), require getting the instance using the `GetHighlighterFromJson()` function. Afterwards, you can register it using `RegisterHighlighter()`.

{% hint style="info" %}
This registration process is necessary for your syntax highlighter to be usable in the terminal reader.
{% endhint %}

You need to keep a handy copy of the instance of your highlighter so that you can use it in the terminal reader settings like this:

{% code title="Demo source code" lineNumbers="true" %}
```csharp
var settingsCustom = new TermReaderSettings()
{
    SyntaxHighlighterEnabled = true,
    SyntaxHighlighter = template,
};
```
{% endcode %}

After that, you must pass the settings instance to the `Read()` function to be able to recognize your highlighter. You can also use the global settings to do the same thing. You can read more about how the reader settings works here:

{% content-ref url="reader-settings.md" %}
[reader-settings.md](reader-settings.md)
{% endcontent-ref %}

{% hint style="info" %}
If you need to get your highlighter in another function, or if you start the reader in another function, you can use the `GetHighlighter()` function, passing it the name of your highlighter defined in the `name` part of its JSON contents, as long as it's registered.
{% endhint %}

If you want to unregister a highlighter, you can use the `UnregisterHighlighter()` function. Be sure that you're really done with the highlighter before trying to call this function.

You can also save your highlighter to a JSON string which you can then save to a file using `GetHighlighterToJson()`. You can later read it using the `GetHighlighterFromJson()` function.
