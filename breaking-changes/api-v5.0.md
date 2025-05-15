---
description: Breaking changes for API v5.0
icon: up
---

# API v5.0

Here is a list of breaking changes that happened during the API v5.0 period when differing versions of Terminaux introduced breaking changes.

## From 4.3.x to 5.0.x

Between the 4.3.x and 5.0.x version range, we've made the following breaking changes:

### ChoiceStyle simplified

{% code title="ChoiceStyle.cs" lineNumbers="true" %}
```csharp
public static string PromptChoice(string Question, (string, string)[] Answers, ChoiceOutputType OutputType = ChoiceOutputType.OneLine, bool PressEnter = false)
public static string PromptChoice(string Question, (string, string)[] Answers, (string, string)[] AlternateAnswers, ChoiceOutputType OutputType = ChoiceOutputType.OneLine, bool PressEnter = false)
public static string PromptChoice(string Question, InputChoiceInfo[] Answers, ChoiceOutputType OutputType = ChoiceOutputType.OneLine, bool PressEnter = false)
public static string PromptChoice(string Question, InputChoiceInfo[] Answers, InputChoiceInfo[] AltAnswers, ChoiceOutputType OutputType = ChoiceOutputType.OneLine, bool PressEnter = false)
public static string PromptChoice(string Question, (string, string)[] Answers, Color questionColor, ChoiceOutputType OutputType = ChoiceOutputType.OneLine, bool PressEnter = false)
public static string PromptChoice(string Question, (string, string)[] Answers, (string, string)[] AlternateAnswers, Color questionColor, ChoiceOutputType OutputType = ChoiceOutputType.OneLine, bool PressEnter = false)
public static string PromptChoice(string Question, InputChoiceInfo[] Answers, Color questionColor, ChoiceOutputType OutputType = ChoiceOutputType.OneLine, bool PressEnter = false)
public static string PromptChoice(string Question, InputChoiceInfo[] Answers, InputChoiceInfo[] AltAnswers, Color questionColor, ChoiceOutputType OutputType = ChoiceOutputType.OneLine, bool PressEnter = false)
public static string PromptChoice(string Question, (string, string)[] Answers, Color questionColor, Color inputColor, ChoiceOutputType OutputType = ChoiceOutputType.OneLine, bool PressEnter = false)
public static string PromptChoice(string Question, (string, string)[] Answers, (string, string)[] AlternateAnswers, Color questionColor, Color inputColor, ChoiceOutputType OutputType = ChoiceOutputType.OneLine, bool PressEnter = false)
public static string PromptChoice(string Question, InputChoiceInfo[] Answers, Color questionColor, Color inputColor, ChoiceOutputType OutputType = ChoiceOutputType.OneLine, bool PressEnter = false)
public static string PromptChoice(string Question, InputChoiceInfo[] Answers, InputChoiceInfo[] AltAnswers, Color questionColor, Color inputColor, ChoiceOutputType OutputType = ChoiceOutputType.OneLine, bool PressEnter = false)
public static string PromptChoice(string Question, (string, string)[] Answers, Color questionColor, Color inputColor, Color optionColor, ChoiceOutputType OutputType = ChoiceOutputType.OneLine, bool PressEnter = false)
public static string PromptChoice(string Question, (string, string)[] Answers, (string, string)[] AlternateAnswers, Color questionColor, Color inputColor, Color optionColor, ChoiceOutputType OutputType = ChoiceOutputType.OneLine, bool PressEnter = false)
public static string PromptChoice(string Question, InputChoiceInfo[] Answers, Color questionColor, Color inputColor, Color optionColor, ChoiceOutputType OutputType = ChoiceOutputType.OneLine, bool PressEnter = false)
public static string PromptChoice(string Question, InputChoiceInfo[] Answers, InputChoiceInfo[] AltAnswers, Color questionColor, Color inputColor, Color optionColor, ChoiceOutputType OutputType = ChoiceOutputType.OneLine, bool PressEnter = false)
public static string PromptChoice(string Question, (string, string)[] Answers, Color questionColor, Color inputColor, Color optionColor, Color altOptionColor, ChoiceOutputType OutputType = ChoiceOutputType.OneLine, bool PressEnter = false)
public static string PromptChoice(string Question, (string, string)[] Answers, (string, string)[] AlternateAnswers, Color questionColor, Color inputColor, Color optionColor, Color altOptionColor, ChoiceOutputType OutputType = ChoiceOutputType.OneLine, bool PressEnter = false)
public static string PromptChoice(string Question, InputChoiceInfo[] Answers, Color questionColor, Color inputColor, Color optionColor, Color altOptionColor, ChoiceOutputType OutputType = ChoiceOutputType.OneLine, bool PressEnter = false)
public static string PromptChoice(string Question, InputChoiceInfo[] Answers, InputChoiceInfo[] AltAnswers, Color questionColor, Color inputColor, Color optionColor, Color altOptionColor, ChoiceOutputType OutputType = ChoiceOutputType.OneLine, bool PressEnter = false)
public static string PromptChoice(string Question, (string, string)[] Answers, Color questionColor, Color inputColor, Color optionColor, Color altOptionColor, Color disabledOptionColor, ChoiceOutputType OutputType = ChoiceOutputType.OneLine, bool PressEnter = false)
public static string PromptChoice(string Question, (string, string)[] Answers, (string, string)[] AlternateAnswers, Color questionColor, Color inputColor, Color optionColor, Color altOptionColor, Color disabledOptionColor, ChoiceOutputType OutputType = ChoiceOutputType.OneLine, bool PressEnter = false)
public static string PromptChoice(string Question, InputChoiceInfo[] Answers, Color questionColor, Color inputColor, Color optionColor, Color altOptionColor, Color disabledOptionColor, ChoiceOutputType OutputType = ChoiceOutputType.OneLine, bool PressEnter = false)
public static string PromptChoice(string Question, InputChoiceInfo[] Answers, InputChoiceInfo[] AltAnswers, Color questionColor, Color inputColor, Color optionColor, Color altOptionColor, Color disabledOptionColor, ChoiceOutputType OutputType = ChoiceOutputType.OneLine, bool PressEnter = false)
```
{% endcode %}

We've made a new class, `ChoiceStyleSettings`, to ease configuration of the choice style. This results in the above function overloads being removed so that all overloads take an argument of `ChoiceStyleSettings`. This argument defines the very settings that you used to define in these overloads to change how it's rendered, including the colors.

{% hint style="info" %}
You must move all the configuration, including the colors, to the `ChoiceStyleSettings` instance to be able to continue configuration.
{% endhint %}

### Table renderer re-write

{% code title="TableColor.cs" lineNumbers="true" %}
```csharp
public static void WriteTablePlain(string[] Headers, string[,] Rows, int Margin, bool SeparateRows = true, List<CellOptions>? CellOptions = null)
public static void WriteTable(string[] Headers, string[,] Rows, int Margin, bool SeparateRows = true, List<CellOptions>? CellOptions = null)
public static void WriteTable(string[] Headers, string[,] Rows, int Margin, Color SeparatorForegroundColor, Color HeaderForegroundColor, Color ValueForegroundColor, Color BackgroundColor, bool SeparateRows = true, List<CellOptions>? CellOptions = null)
public static string RenderTablePlain(string[] Headers, string[,] Rows, int Margin, bool SeparateRows = true, List<CellOptions>? CellOptions = null)
public static string RenderTable(string[] Headers, string[,] Rows, int Margin, Color SeparatorForegroundColor, Color HeaderForegroundColor, Color ValueForegroundColor, Color BackgroundColor, bool SeparateRows = true, List<CellOptions>? CellOptions = null)
```
{% endcode %}

The implementation of the table introduced in the first version of Terminaux that was taken from Nitrocid 0.0.20 wasn't in any way good and nice, so we've decided to re-write the whole renderer from scratch. As a result, our tables look nicer and more beautiful.

However, we also had to change how you call the table rendering and writing functions so that they become easier to use.

{% hint style="info" %}
You can now place your headers at the top of the rows argument and set the `enableHeader` parameter to true. You'll have to determine the left, the top, the width, and the height of the table as it no longer depends on the current cursor position.

You'll have to take application behavior into account, as applications that depend on the previous behavior will need to be re-written.
{% endhint %}

### Terminaux.Extensions removal

{% code title="EnumerableExtensions.cs" lineNumbers="true" %}
```csharp
public static class EnumerableExtensions
```
{% endcode %}

As we don't want to cause conflicts of implementations and duplicate commits for each change in the enumerable extensions, we've decided to remove Terminaux.Extensions entirely and rely on Magico to provide such extensions.

{% hint style="info" %}
Migration to Terminaux 5.0 requires that you remove Terminaux.Extensions from your NuGet dependencies and replace it with Magico.
{% endhint %}

### Input class introduced

{% code title="PointerListener.cs" lineNumbers="true" %}
```csharp
public static class PointerListener
```
{% endcode %}

While we were trying to fix the mouse listener CPU usage being 100% in all the systems, we've decided to unify the input class so that we can introduce the unified `Input` class. This is why we have to remove the `PointerListener` class as it doesn't listen, but poll.

{% hint style="info" %}
You should change your references to PointerListener so that they point to their Input class equivalents, although they usually hold the same name. However, methods that start or stop the listener have been removed, and their equivalent is a property, `EnableMouse`, that enables or disables mouse support.
{% endhint %}

### Resize listener back to Terminaux

{% code title="ConsoleResizeListener.cs" lineNumbers="true" %}
```csharp
public static class ConsoleResizeListener
```
{% endcode %}

We've restored the resize listener functions back to the base Terminaux library, albeit we've removed the POSIX listener part because we wanted consistency and our latest experiments showed that the POSIX listener is actually slower than our old way.

{% hint style="info" %}
Functions, although their names haven't changed, have been moved to another namespace and class, `Terminaux.Base.ConsoleResizeHandler`. Change your references to point to that instead.
{% endhint %}

### Interactive TUI polishing

As of Terminaux 5.0.0, the interactive TUI has been improved. As a result, the following changes have to be made:

#### Removed useless properties

{% code title="BaseInteractiveTui.cs" lineNumbers="true" %}
```csharp
public static BaseInteractiveTui<T>? Instance
public Screen? Screen
```
{% endcode %}

In order for this system to be more maintainable, we've removed the two above properties to prevent direct manipulation and as a plan to polish the interactive TUI code to be more maintainable in case of bugs that we need to fix later.

#### Overflow and underflow checking moved

{% code title="BaseInteractiveTui.cs" lineNumbers="true" %}
```csharp
public void LastOnOverflow()
public void FirstOnUnderflow()
```
{% endcode %}

These two functions are not overridable when creating a new interactive TUI, and are never meant to be, so we've decided to move them out to the `InteractiveTuiTools` class to better reflect their purpose.

#### Status properties moved to the base class

{% code title="InteractiveTuiStatus.cs" lineNumbers="true" %}
```csharp
public static int FirstPaneCurrentSelection { get; internal set; }
public static int SecondPaneCurrentSelection { get; internal set; }
public static int CurrentSelection
public static string Status { get; internal set; }
public static int CurrentPane { get; internal set; }
public static int CurrentInfoLine { get; internal set; }
public static Color BackgroundColor { get; set; }
public static Color ForegroundColor { get; set; }
public static Color PaneBackgroundColor { get; set; }
public static Color PaneSeparatorColor { get; set; }
public static Color PaneSelectedSeparatorColor { get; set; }
public static Color PaneSelectedItemForeColor { get; set; }
public static Color PaneSelectedItemBackColor { get; set; }
public static Color PaneItemForeColor { get; set; }
public static Color PaneItemBackColor { get; set; }
public static Color OptionBackgroundColor { get; set; }
public static Color KeyBindingOptionColor { get; set; }
public static Color OptionForegroundColor { get; set; }
public static Color KeyBindingBuiltinBackgroundColor { get; set; }
public static Color KeyBindingBuiltinColor { get; set; }
public static Color KeyBindingBuiltinForegroundColor { get; set; }
public static Color BoxBackgroundColor { get; set; }
public static Color BoxForegroundColor { get; set; }
```
{% endcode %}

The removal of `InteractiveTuiStatus` was necessary to make all your interactive TUIs more deterministic and to be more consistent in regards to positioning, colors, and others. Colors have been moved to `InteractiveTuiSettings` and all of the status properties have been moved to `BaseInteractiveTui`.

#### Keybinding definition changed

{% code title="BaseInteractiveTui.cs" lineNumbers="true" %}
```csharp
public virtual InteractiveTuiBinding[] Bindings { get; }
```
{% endcode %}

We've changed how you can define your keybindings. Instead of being required to provide static functions and/or properties in your binding instance while defining your key bindings, you can now define them on the fly with support for values and non-static functions and/or properties. This enables your TUIs to be more powerful and maintainable than before.

You'll have to change how you define these functions that get bound to a key or a mouse button and you'll have to add your keybindings to the instance immediately after creating a new instance of your interactive TUI class before actually opening it.

{% hint style="info" %}
You may also have to change your action code if there are two panes that are accessible.
{% endhint %}

#### Interactive TUI types are now more flexible

{% code title="BaseInteractiveTui.cs" lineNumbers="true" %}
```csharp
public int CurrentSelection
public IEnumerable<T> DataSource
```
{% endcode %}

We've removed the above properties.

{% code title="BaseInteractiveTui.cs" lineNumbers="true" %}
```csharp
public virtual IEnumerable<T> PrimaryDataSource
public virtual IEnumerable<T> SecondaryDataSource
public virtual string GetEntryFromItem(T item)
public virtual string GetInfoFromItem(T item)
public virtual string GetStatusFromItem(T item)
```
{% endcode %}

We've changed how the `T` is determined so that you can pass in two appropriate types. This makes building your interactive TUIs easier than before. The last three functions have been duplicated so that they process the secondary type, `TSecondary`.

As a result, all the functions in the InteractiveTuiTools class have been changed so that they take the two types according to your interactive TUI's definition.

#### Interactive TUI keybinding classes have become generic

{% code title="InteractiveTuiBinding.cs" lineNumbers="true" %}
```csharp
public class InteractiveTuiBinding : Keybinding, IEquatable<InteractiveTuiBinding?>
```
{% endcode %}

The interactive TUI binding class, which you use to define your own key bindings for your interactive TUI applications as per your needs, has been changed so that it's a generic class that takes either a type for single-type TUIs or duo-type TUIs. As a result, the following functions have been changed:

{% code title="BaseInteractiveTui.cs" lineNumbers="true" %}
```csharp
public List<InteractiveTuiBinding> Bindings { get; internal set; }
```
{% endcode %}

{% code title="InteractiveTuiBinding.cs" lineNumbers="true" %}
```csharp
public Action<object?, int>? BindingAction
public InteractiveTuiBinding(string bindingName, ConsoleKey bindingKeyName, Action<object?, int>? bindingAction, bool canRunWithoutItems = false)
public InteractiveTuiBinding(string bindingName, ConsoleKey bindingKeyName, ConsoleModifiers bindingKeyModifiers, Action<object?, int>? bindingAction, bool canRunWithoutItems = false)
public InteractiveTuiBinding(string bindingName, PointerButton bindingPointerButton, Action<object?, int>? bindingAction, bool canRunWithoutItems = false)
public InteractiveTuiBinding(string bindingName, PointerButton bindingPointerButton, PointerButtonPress bindingPointerButtonPress, Action<object?, int>? bindingAction, bool canRunWithoutItems = false)
public InteractiveTuiBinding(string bindingName, PointerButton bindingPointerButton, PointerButtonPress bindingPointerButtonPress, PointerModifiers bindingButtonModifiers, Action<object?, int>? bindingAction, bool canRunWithoutItems = false)
public bool Equals(InteractiveTuiBinding? other)
public static bool operator ==(InteractiveTuiBinding? left, InteractiveTuiBinding? right)
public static bool operator !=(InteractiveTuiBinding? left, InteractiveTuiBinding? right)
```
{% endcode %}

You'll now have to determine whether to use the primary and the secondary values and indexes or not when defining your own interactive TUI keybindings.

### Input choice moved to Inputs.Styles

{% code title="Terminaux.Inputs -> Terminaux.Inputs.Styles" lineNumbers="true" %}
```csharp
public class InputChoiceInfo
public static class InputChoiceTools
```
{% endcode %}

The two above classes have been moved to `Terminaux.Inputs.Styles` as the input choice is actually considered as an input style and is not part of the base input, which the `Input` class defines.

{% hint style="info" %}
Change the using clause that contain both classes to use `Terminaux.Inputs.Styles`.
{% endhint %}

### `InitializeSequences()` moved

{% code title="ConsolePositioning.cs" lineNumbers="true" %}
```csharp
public static bool InitializeSequences()
```
{% endcode %}

This function has nothing to do with cursor positioning, so we've moved it outside `CursorPositioning` to the `ConsoleMisc` extension group.

{% hint style="info" %}
We haven't changed the name of the function or its functionality, but you should change all references that point to this function to reference the `ConsoleMisc` class.
{% endhint %}

### Removed `SelectionStyleSwitches`

{% code title="SelectionStyleSwitches.cs" lineNumbers="true" %}
```csharp
public static class SelectionStyleSwitches
```
{% endcode %}

Currently, we don't have any use of this class because we've removed showing page count and choice count, so we've decided to remove this class until further notice. It'll be back in a non-static form under a different name.

{% hint style="warning" %}
It will be back in a future Terminaux release, so be patient.
{% endhint %}

### Outsourced character width tools to Textify

{% code title="ConsoleChar.cs" lineNumbers="true" %}
```csharp
public static bool UseTwoCellsForUnassignedChars { get; set; }
public static bool UseTwoCellsForAmbiguousChars { get; set; }
public static bool UseTwoCellsForPrivateChars { get; set; }
public static int GetCharWidth(int c)
public static CharWidthType GetCharWidthType(int c)
```
{% endcode %}

{% code title="CharWidthType.cs" lineNumbers="true" %}
```csharp
public enum CharWidthType
```
{% endcode %}

These functions and properties could have been implemented in Textify, but we had initially implemented them in Terminaux as we're adding support for Chinese-Japenese-Korean (CJK) text for all the console-related features. As we consider this support to be stable, we've decided to move them out of Terminaux to Textify.

{% hint style="info" %}
Refer to [Textify's manual](https://app.gitbook.com/o/fj052nYlsxW9IdL3bsZj/s/NaUWjRlaBR1k5rO42Zy8/) for more info. You'll only have to change the reference to point to `TextTools`.
{% endhint %}

## From 5.0.x to 5.3.x

Between the 5.0.x and 5.3.x version range, we've made the following breaking changes:

### Used `TermInfoValueDesc` for capabilities

{% code title="ExtendedCapabilities.cs" lineNumbers="true" %}
```csharp
public bool? GetBoolean(string key)
public int? GetNum(string key)
public string? GetString(string key)
```
{% endcode %}

{% code title="TermInfoDesc.cs" lineNumbers="true" %}
```csharp
public bool? GetBoolean(TermInfoCaps.Boolean value)
public int? GetNum(TermInfoCaps.Num value)
public string? GetString(TermInfoCaps.String value)

// and all corresponding generated capability properties
```
{% endcode %}

In order to implement the parameter extraction functionality, we had to implement both `TermInfoValueDesc` and `ParameterInfo` that allow easier parameter processing to ensure that we can store the following properties in the former class:

* `Value`
* `Name`
* `ValueType`
* `Desc`

{% code title="TermInfoCapsKind.cs" lineNumbers="true" %}
```csharp
public enum TermInfoCapsKind
```
{% endcode %}

As a consequence, we had to remove the above enumeration in order to satisfy the requirements of the two new classes introduced to Terminaux.

{% hint style="info" %}
You'll have to adjust your calls to call appropriate properties. For example, if you used to be able to access a string directly, you'll have to get a value of the `Value` property found in the `TermInfoValueDesc<string?>` string capability instance.
{% endhint %}

## From 5.3.x to 5.4.x

Between the 5.3.x and 5.4.x version range, we've made the following breaking changes:

### Infobox clarifications

{% code title="InfoBoxColor.cs" lineNumbers="true" %}
```csharp
public static class InfoBoxColor
```
{% endcode %}

Since the start of Terminaux, when we had implemented informational boxes, we kept saying "modal infoboxes" for boxes that require a user input and "non-modal infoboxes" for boxes that don't require a user input and just print themselves to the terminal, while the modality could be demonstrated by toggling the `waitForInput` parameter on or off. To clear confusion, we've decided to rename the class to indicate infobox modality

{% hint style="info" %}
* For modal infoboxes, the class name is `InfoBoxModalColor`.
* For non-modal infoboxes, the class name is `InfoBoxNonModalColor`.
{% endhint %}
