---
description: More control in your TUIs!
icon: browser
---

# Textual UI

This feature is the new form of interactive TUIs that not only allow you to make an interactive TUI based on a set of data for either a single pane or two panes, but you can also make your own interactive applications seamlessly by separating the rendering code and the key handling code into small functions. This achieves the goal of making textual UI code maintenance easier, while providing the most dynamic UI setup along with support for resize thanks to the [screen](console-screen.md) feature.

To get started using this awesome feature, you can create a new class that implements the `TextualUI` abstract class and overrides the `Render()` function. Inside the function, you can return a string that consists of VT sequences resulting from several console writers, especially the renderables. You can find out more about the renderables here.

{% content-ref url="../console-writers/cyclic-writers/" %}
[cyclic-writers](../console-writers/cyclic-writers/)
{% endcontent-ref %}

{% hint style="info" %}
Before this feature has been implemented, the interactive TUI feature consisted of just data arrays with two panes, which made cases that required something outside that scope unsolvable. The new feature promises to remove this limitation. Meanwhile, you can still use the older interactive TUI, which was first implemented in the Nitrocid KS 0.1.0 milestones in 2022, [here](interactive-tui.md).
{% endhint %}

In the class, there are several properties that you can modify at your discretion, such as the name and the refresh delay. You can use the following properties:

* `Guid`: Unique ID for the textual UI (reserved for future use)
* `State`: State of the textual UI, which is one of the following:
  * `Ready`: This textual UI is ready, but hasn't started yet.
  * `Rendering`: This textual UI is waiting for the render code to complete.
  * `Waiting`: This textual UI is waiting for user input.
  * `Busy`: This textual UI is busy because it's processing user input.
  * `Bailing`: This textual UI is about to exit and go back to the `Ready` state.
* `Name`: Display name of the textual UI (reserved for future use)
* `RefreshDelay`: Sets the refresh delay in milliseconds. If set to zero or less than zero, this TUI doesn't refresh.
* `Keybindings`: List of keybindings that you can use within the TUI.
* `Fallback`: Fallback binding in case a key doesn't bind to anything.
* `Renderables`: List of renderables that get rendered on top of what the `Render()` function has rendered.

If you want the TUI to refresh in the next render, you'll have to call the `RequireRefresh()` function, which calls the refresh requirement function on the screen instance.

{% hint style="info" %}
You can edit the `Keybindings` property to add your custom keybindings, but it's preferrable to either place them in a constructor or in the overridden value, and to define the delegates in separate private functions inside the UI class. Also, make sure that you don't place conflicting keybindings when trying to add them.
{% endhint %}

In addition to that, you can also access the `TextualUITools` class to perform the following operations:

* `RunTui()`: Starts the TUI main loop, clears the screen, waits for user input, and processes it until the TUI has been requested to exit.
* `ExitTui()`: Sets the state of the interactive TUI to `Bailing` so that the TUI can exit gracefully.

## Examples

There are two examples as defined in the test application bundled with the source code of Terminaux:

{% tabs %}
{% tab title="Simple" %}
This example provides you with a simple interactive TUI showing three boxes that you can control using the keybindings defined in the constructor of the interactive TUI.

{% @github-files/github-code-block url="https://github.com/Aptivi/Terminaux/blob/main/Terminaux.Console/Fixtures/Cases/CaseData/TextualUiSimpleTestData.cs" %}

Here's the companion code to start the interactive TUI for the above class:

{% @github-files/github-code-block url="https://github.com/Aptivi/Terminaux/blob/main/Terminaux.Console/Fixtures/Cases/Tui/TestScreenPartVisibilityTui.cs" %}

Here's the resulting picture of the interactive TUI:

<figure><img src="../../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Refreshing" %}
This example provides you with a refreshing interactive TUI showing three boxes, one of which is constantly changing color according to the number of frames rendered, that you can control using the keybindings defined in the constructor of the interactive TUI.

{% @github-files/github-code-block url="https://github.com/Aptivi/Terminaux/blob/main/Terminaux.Console/Fixtures/Cases/CaseData/TextualUiRefreshTestData.cs" %}

Here's the companion code that executes the above TUI class:

{% @github-files/github-code-block url="https://github.com/Aptivi/Terminaux/blob/main/Terminaux.Console/Fixtures/Cases/Tui/TestScreenPartVisibilityRefreshTui.cs" %}

Here's the resulting picture for the TUI:

<figure><img src="../../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

## Defining Keybindings

When defining keybindings, it's recommended to do so from either the constructor of the interactive TUI or in the overridden value of the Keybindings list, except if you want this keybinding list to always change during the runtime of the textual UI, such as the color selector. We also recommend to define their actions in separate private functions, passing in the parameters as needed.

* To define a keybinding in your interactive TUI, use the `Keybindings.Add()` statement to pass in a tuple of the following two variables:
  * A [`Keybinding`](../../input-reader/other-input/keybindings.md) instance that matches the key and its modifiers (mouse or keyboard) that you want to bind a specific action to.
  * An action delegate or lambda function that tells the interactive TUI what to do. The following four arguments are optional for lambda expressions, but required for delegates:
    * Interactive TUI instance that specifies the running TUI.
    * Keyboard press info defined by the [ConsoleKeyInfo](https://learn.microsoft.com/en-us/dotnet/api/system.consolekeyinfo) struct.
    * Mouse event info defined by the [PointerEventContext](../../input-reader/pointer-events.md) class.
* To remove a keybinding in your interactive TUI, use the `Keybindings.RemoveAt()` function.
* To remove all keybindings in your interactive TUI, use the `Keybindings.Clear()` function.
