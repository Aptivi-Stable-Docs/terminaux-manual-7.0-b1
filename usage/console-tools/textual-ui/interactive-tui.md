---
description: Your apps are now interactive
icon: keyboard
---

# Interactive TUI

Terminaux allows you to build interactive terminal applications based on data sets that consist of either a single type or a double type. Using the interactive TUI feature is straightforward, but you'll need to tell the interactive TUI tool how to render your data.

You can use the down/up arrow keys to navigate items within the current pane, the `TAB` key to switch panes, `ESC` to quit, and `F` to search items with regular expressions.

This is achieved by creating a class that consists of either a single data type or a double data type:

## Preparation

Before being able to display it, you'll need to prepare a class with one or two of the data types of your choice:

* Single data type: You can implement the `BaseInteractiveTui<T>` class and the `IInteractiveTui<T>` interface in your own TUI class.
* Double data type: You can implement the `BaseInteractiveTui<TPrimary, TSecondary>` class and the `IInteractiveTui<TPrimary, TSecondary>` interface in your own TUI class.

{% hint style="warning" %}
The single data type implementation can be applied in the interactive TUIs that accept two panes, but using double data type implementation in said TUIs will result in only the primary one being used.
{% endhint %}

### Single data type interactive TUI

When working with an interactive TUI that contains only a single data type, you must implement both the `BaseInteractiveTui<T>` class and the `IInteractiveTui<T>` interface in your own TUI class so that you can choose what type your data source (list of data) will be. A simple example of an interactive TUI of this type with keybinding action functions is:

{% code lineNumbers="true" %}
```csharp
internal class CliInfoPaneTestData : BaseInteractiveTui<string>, IInteractiveTui<string>
{
    internal static List<string> strings = [];

    /// <inheritdoc/>
    public override IEnumerable<string> PrimaryDataSource =>
        strings;

    /// <inheritdoc/>
    public override bool AcceptsEmptyData =>
        true;

    /// <inheritdoc/>
    public override string GetInfoFromItem(string item)
    {
        string selected = item;

        // Check to see if we're given the test info
        if (string.IsNullOrEmpty(selected))
            return " No info.";
        else
            return $" {selected}";
    }

    /// <inheritdoc/>
    public override string GetEntryFromItem(string item)
    {
        string selected = item;
        return selected;
    }

    internal void Add(int index)
    {
        strings.Add($"[{index}] --+-- [{index}]");
    }

    internal void Remove(int index)
    {
        if (strings.Count > 0)
            strings.RemoveAt(index);
    }

    internal void RemoveLast()
    {
        if (strings.Count > 0)
            strings.RemoveAt(strings.Count - 1);
    }
}
```
{% endcode %}

This results in the console UI showing up like this:

<figure><img src="../../../.gitbook/assets/image (100).png" alt=""><figcaption></figcaption></figure>

You can also use this in an interactive TUI that accepts two data sources by overriding `SecondPaneInteractable` to true, just like this:

<pre class="language-csharp" data-line-numbers><code class="lang-csharp">internal class CliDoublePaneTestData : BaseInteractiveTui&#x3C;string>, IInteractiveTui&#x3C;string>
{
    internal static List&#x3C;string> strings = [];
    internal static List&#x3C;string> strings2 = [];

    /// &#x3C;inheritdoc/>
    public override IEnumerable&#x3C;string> PrimaryDataSource =>
        strings;

    /// &#x3C;inheritdoc/>
    public override IEnumerable&#x3C;string> SecondaryDataSource =>
        strings2;

<strong>    public override bool SecondPaneInteractable =>
</strong><strong>        true;
</strong>
    /// &#x3C;inheritdoc/>
    public override bool AcceptsEmptyData =>
        true;

    /// &#x3C;inheritdoc/>
    public override string GetStatusFromItem(string item) =>
        string.IsNullOrEmpty(item) ? "No info." : item;

    /// &#x3C;inheritdoc/>
    public override string GetEntryFromItem(string item) =>
        item;

    /// &#x3C;inheritdoc/>
    public override string GetStatusFromItemSecondary(string item) =>
        string.IsNullOrEmpty(item) ? "No info." : item;

    /// &#x3C;inheritdoc/>
    public override string GetEntryFromItemSecondary(string item) =>
        item;

    internal void Add(int index, int index2)
    {
        if (CurrentPane == 2)
            strings2.Add($"[{index2}] --2-- [{index2}]");
        else
            strings.Add($"[{index}] --1-- [{index}]");
    }

    internal void Remove(int index, int index2)
    {
        if (CurrentPane == 2)
        {
            if (index2 &#x3C; strings2.Count &#x26;&#x26; strings2.Count > 0)
                strings2.RemoveAt(index2 == 0 ? index2 : index2 - 1);
            if (SecondPaneCurrentSelection > strings2.Count)
                InteractiveTuiTools.SelectionMovement(this, strings2.Count);
        }
        else
        {
            if (index &#x3C; strings.Count &#x26;&#x26; strings.Count > 0)
                strings.RemoveAt(index == 0 ? index : index - 1);
            if (FirstPaneCurrentSelection > strings.Count)
                InteractiveTuiTools.SelectionMovement(this, strings.Count);
        }
    }

    internal void RemoveLast()
    {
        if (CurrentPane == 2)
        {
            if (strings2.Count > 0)
                strings2.RemoveAt(strings2.Count - 1);
            if (SecondPaneCurrentSelection > strings2.Count)
                InteractiveTuiTools.SelectionMovement(this, strings2.Count);
        }
        else
        {
            if (strings.Count > 0)
                strings.RemoveAt(strings.Count - 1);
            if (FirstPaneCurrentSelection > strings.Count)
                InteractiveTuiTools.SelectionMovement(this, strings.Count);
        }
    }
}
</code></pre>

### Double data type interactive TUI

Your interactive TUI can also accept two different data types, but it must accept two data sources in order for this to work. Otherwise, only the primary type is considered. When working with an interactive TUI that contains two data types, you must implement both the `BaseInteractiveTui<TPrimary, TSecondary>` class and the `IInteractiveTui<TPrimary, TSecondary>` interface in your own TUI class. A simple example of an interactive TUI of this type with keybinding action functions is:

{% code lineNumbers="true" %}
```csharp
internal class CliDoublePaneTestData : BaseInteractiveTui<string, string>, IInteractiveTui<string, string>
{
    internal static List<string> strings = [];
    internal static List<string> strings2 = [];

    /// <inheritdoc/>
    public override IEnumerable<string> PrimaryDataSource =>
        strings;

    /// <inheritdoc/>
    public override IEnumerable<string> SecondaryDataSource =>
        strings2;

    public override bool SecondPaneInteractable =>
        true;

    /// <inheritdoc/>
    public override bool AcceptsEmptyData =>
        true;

    /// <inheritdoc/>
    public override string GetStatusFromItem(string item) =>
        string.IsNullOrEmpty(item) ? "No info." : item;

    /// <inheritdoc/>
    public override string GetEntryFromItem(string item) =>
        item;

    /// <inheritdoc/>
    public override string GetStatusFromItemSecondary(string item) =>
        string.IsNullOrEmpty(item) ? "No info." : item;

    /// <inheritdoc/>
    public override string GetEntryFromItemSecondary(string item) =>
        item;

    internal void Add(int index, int index2)
    {
        if (CurrentPane == 2)
            strings2.Add($"[{index2}] --2-- [{index2}]");
        else
            strings.Add($"[{index}] --1-- [{index}]");
    }

    internal void Remove(int index, int index2)
    {
        if (CurrentPane == 2)
        {
            if (index2 < strings2.Count && strings2.Count > 0)
                strings2.RemoveAt(index2 == 0 ? index2 : index2 - 1);
            if (SecondPaneCurrentSelection > strings2.Count)
                InteractiveTuiTools.SelectionMovement(this, strings2.Count);
        }
        else
        {
            if (index < strings.Count && strings.Count > 0)
                strings.RemoveAt(index == 0 ? index : index - 1);
            if (FirstPaneCurrentSelection > strings.Count)
                InteractiveTuiTools.SelectionMovement(this, strings.Count);
        }
    }

    internal void RemoveLast()
    {
        if (CurrentPane == 2)
        {
            if (strings2.Count > 0)
                strings2.RemoveAt(strings2.Count - 1);
            if (SecondPaneCurrentSelection > strings2.Count)
                InteractiveTuiTools.SelectionMovement(this, strings2.Count);
        }
        else
        {
            if (strings.Count > 0)
                strings.RemoveAt(strings.Count - 1);
            if (FirstPaneCurrentSelection > strings.Count)
                InteractiveTuiTools.SelectionMovement(this, strings.Count);
        }
    }
}
```
{% endcode %}

This results in the double pane interactive TUI showing up like this:

<figure><img src="../../../.gitbook/assets/image (102).png" alt=""><figcaption></figcaption></figure>

## Execution

The execution process involves having to add keybindings to the interactive TUI to make it more useful and to the point, though they are completely optional in some cases, such as automatically refreshing TUIs. After that, you'll have to call the `OpenInteractiveTui()` under the `InteractiveTuiTools` class, passing it your brand new interactive TUI class instance. A simple example of this process with keybindings is like this:

{% code lineNumbers="true" %}
```csharp
public void RunFixture()
{
    var tui = new CliInfoPaneTestData();
    tui.Bindings.Add(new InteractiveTuiBinding<string>("Add", ConsoleKey.F1, (_, index, _, _) => tui.Add(index), true));
    tui.Bindings.Add(new InteractiveTuiBinding<string>("Delete", ConsoleKey.F2, (_, index, _, _) => tui.Remove(index), true));
    tui.Bindings.Add(new InteractiveTuiBinding<string>("Delete", PointerButton.Right, PointerButtonPress.Released, (_, index, _, _) => tui.Remove(index)));
    tui.Bindings.Add(new InteractiveTuiBinding<string>("Delete Last", ConsoleKey.F3, (_, _, _, _) => tui.RemoveLast(), true));
    InteractiveTuiTools.OpenInteractiveTui(tui);
}
```
{% endcode %}

The `InteractiveTuiBinding` class is a generic class that takes either a single data type or a multiple data type. However, they must match the interactive TUI pane data types so that they become easy to implement. The delegate, which dictates what a specific keybinding is going to do with your interactive TUI, has the following arguments:

* Primary item
* Primary item index
* Secondary item
* Secondary item index

{% hint style="warning" %}
If you're going to create a binding class that supports mouse, ensure that you've put a code in the binding logic function that checks to see if the mouse cursor is at the right pane so that the TUI may not have accidentally launched your action in the wrong pane. A simple example is to bail if this action is run on a wrong pane is written below as part of your action code:

{% code lineNumbers="true" %}
```csharp
// Check the pane first
if (CurrentPane != 2)
    return;
```
{% endcode %}
{% endhint %}

## Configuration

You can also configure how your interactive TUI behaves, such as automatic refreshing. For automatic refreshing, your data type will have to be dynamic (i.e. constantly changing) to be able to see live data in the interactive TUI. In order to configure the automatic refresh, you'll have to override the `RefreshInterval` property and to give it a duration of the pause between refreshes in milliseconds.

{% hint style="info" %}
All configuration must be done when implementing your interactive TUI class. However, you can globally configure the interactive TUI appearance using the `GlobalSettings` property found in the `InteractiveTuiSettings` class
{% endhint %}
