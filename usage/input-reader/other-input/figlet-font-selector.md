---
description: Select your favorite font from here!
icon: pen
---

# Figlet Font Selector

<figure><img src="../../../.gitbook/assets/image (85).png" alt=""><figcaption></figcaption></figure>

The figlet font selector allows you to flexibly select a Figlet font provided by the Figlet part of Textify, powered by the [textual UI](../../console-tools/textual-ui/) feature. It shows you a live preview of the font to show you how your selected font looks like prior to submission.

{% hint style="info" %}
`FigletTextTools` provides default figlet font settings.
{% endhint %}

You can simply invoke the selector on your interactive console application by calling the below function like so:

```csharp
string font = FigletSelector.PromptForFiglet();
```

Usually, this call is followed by getting a figlet font from the above variable and writing it using the `WriteFiglet()` function:

```csharp
var figlet = FigletTools.GetFigletFont(font);
FigletColor.WriteFiglet("Hello!", figlet, ConsoleColors.Green);
```

Additionally, you can press `S` to write the desired font name and quickly switch to that font. If you want to cancel, you can press `ESC`.

The following controls are available for the normal figlet font selector:

<table><thead><tr><th width="226">Key</th><th>Action</th></tr></thead><tbody><tr><td><code>ENTER</code></td><td>Accept font selection</td></tr><tr><td><code>ESC</code></td><td>Discard changes</td></tr><tr><td><code>H</code></td><td>Help page</td></tr><tr><td><code>LEFT</code> / <code>WHEEL UP</code></td><td>Previous font</td></tr><tr><td><code>RIGHT</code> / <code>WHEEL DOWN</code></td><td>Next font</td></tr><tr><td><code>S</code></td><td>Select font from the infobox</td></tr><tr><td><code>SHIFT</code> + <code>S</code></td><td>Write font name</td></tr><tr><td><code>C</code></td><td>Shows the individual characters with the selected font</td></tr></tbody></table>

The following controls are available for the character showcase:

<table><thead><tr><th width="226">Key</th><th>Action</th></tr></thead><tbody><tr><td><code>ENTER</code></td><td>Go back</td></tr><tr><td><code>LEFT</code> / <code>WHEEL UP</code></td><td>Previous character</td></tr><tr><td><code>RIGHT</code> / <code>WHEEL DOWN</code></td><td>Next character</td></tr></tbody></table>

More details about `WriteFiglet()` can be found in the below link:

{% content-ref url="../../console-tools/console-writers/" %}
[console-writers](../../console-tools/console-writers/)
{% endcontent-ref %}
