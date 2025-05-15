---
description: Breaking changes for API v1.0
icon: up
---

# API v1.0

Here is a list of breaking changes that happened during the API v1.0 period when differing versions of Terminaux introduced breaking changes.

## From 1.0.x to 1.1.x

Between the 1.0.x and 1.1.x version range, we've made the following breaking changes:

### Moved `FigletTools`

{% code title="FigletTools.cs" lineNumbers="true" %}
```csharp
public static class FigletTools
```
{% endcode %}

In preparation for the figlet font selector, we've decided to move this class from the `Terminaux.Writer.FancyWriters.Tools` namespace to a more appropriate place, which is `Terminaux.Figlet`.&#x20;

{% hint style="info" %}
We advice you to add a new `usings` clause in the beginning of the code file that uses `FigletTools` so that it points to the new namespace, like below:

```csharp
using Terminaux.Figlet
```
{% endhint %}

## From 1.1.x to 1.4.x

Between the 1.1.x and 1.4.x version range, we've made the following breaking changes:

### Added the signing key (a.k.a. strong name) <a href="#added-the-signing-key-a.k.a.-strong-name" id="added-the-signing-key-a.k.a.-strong-name"></a>

Nitrocid KS launched without any signing key. Originally, it was planned to come signed by us, but it didn't work. However, we used the strong naming tool to give Nitrocid KS a unique identity to avoid dependency hell.

{% hint style="info" %}
It's not necessary to strong name your mods, but we recommend you to do so using the strong naming utility (`sn.exe`) that comes with Visual Studio.

Most of the time, you don't have to do anything to your mods, since the signing key change doesn't break any API functions. If you found that your mods no longer worked, try to update to the latest version of Nitrocid, or contact the mod vendor.
{% endhint %}

### Enhanced console wrapper

{% code title="ConsoleWrapperTools.cs" lineNumbers="true" %}
```csharp
public static class ConsoleTools
```
{% endcode %}

When Terminaux shipped its first version, it had a console wrapper that was exclusive to the console reader. We've decided to make this wrapper broader, causing Terminaux to ddepend on this wrapper to call the Console functions, hence increasing its flexibility.

{% hint style="info" %}
`ConsoleTools` has been renamed to `ConsoleWrappers`, and it has been moved to the `Terminaux.Base` namespace.

None of the actions are affected.
{% endhint %}

## From 1.4.x to 1.6.x

Between the 1.4.x and 1.6.x version range, we've made the following breaking changes:

### Moved the legacy Figgle writers

{% code title="*Legacy.cs" lineNumbers="true" %}
```csharp
public static class CenteredFigletTextColorLegacy
public static class FigletColorLegacy
public static class FigletWhereColorLegacy
```
{% endcode %}

Since Figletize was made to improve the Figgle library as a fork, we've decided to move all Figgle-based figlet writers to Terminaux's separate library for Figgle-related writers and tools.

{% hint style="info" %}
If possible, merge to Figletize and use the new figlet functions to achieve more performance. If you still prefer Figgle, you can use the above classes. However, they've been moved to the below namespace:

* `Terminaux.Figgle.Writers`
{% endhint %}

## From 1.6.x to 1.8.x

Between the 1.6.x and 1.8.x version range, we've made the following breaking changes:

### Conflicting write overloads reduced

{% code title="TextWriterColor.cs and all similar writers" lineNumbers="true" %}
```csharp
public static void Write(string Text, bool Line, ConsoleColors color, params object[] vars)
public static void Write(string Text, bool Line, bool Highlight, ConsoleColors color, params object[] vars)
public static void Write(string Text, bool Line, ConsoleColors ForegroundColor, ConsoleColors BackgroundColor, params object[] vars)
public static void Write(string Text, bool Line, bool Highlight, ConsoleColors ForegroundColor, ConsoleColors BackgroundColor, params object[] vars)
public static void Write(string Text, bool Line, Color color, params object[] vars)
public static void Write(string Text, bool Line, bool Highlight, Color color, params object[] vars)
public static void Write(string Text, bool Line, Color ForegroundColor, Color BackgroundColor, params object[] vars)
public static void Write(string Text, bool Line, bool Highlight, Color ForegroundColor, Color BackgroundColor, params object[] vars)
```
{% endcode %}

Ever since Terminaux was released to the public, the `Color` class had an implicit operator which would take either an integer, a string, or a `ConsoleColors` value and create a new `Color` class based on these values. This caused us to have to fix every function call that contain strings as their first parameters, since they were mistaken for creating a new color, causing graphical artifacts.

We've recommended mod developers who suffer from this ambiguity issue append a `vars:` prefix in its appropriate place and write `new object[] { args }`, but this is a big overhead.

So, we've decided to rename function names that take colors to these variants:

* `Write()`: for plain writing in default colors
* `WriteColor()`: for writing with custom foreground colors
* `WriteColorBack()`: for writing with custom foreground and background colors

{% hint style="info" %}
You no longer need to override the vars value using the above method. Instead, you can replace these calls with one of the above functions, based on the color type.
{% endhint %}

## From 1.8.x to 1.10.x

Between the 1.8.x and 1.10.x version range, we've made the following breaking changes:

### Replaced `Color255` with deserialized colors data

{% code title="Color255.cs" lineNumbers="true" %}
```csharp
public static class Color255
```
{% endcode %}

`Color255` used to host a single variable containing the 256 console colors and their information in a single object class. However, the way it was implemented was more complicated and uses the JSON LINQ feature, which is complex.

As a result, we've decided to reduce complexity by removing the `ColorDataJson` variable from the class, ultimately resulting in the removal of this entire class.

{% hint style="info" %}
The list of all 256 console colors and their info can be accessed using the `GetColorData()` function from the `ConsoleColorData` class.
{% endhint %}
