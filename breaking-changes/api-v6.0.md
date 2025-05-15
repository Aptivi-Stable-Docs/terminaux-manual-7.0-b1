---
description: Breaking changes for API v6.0
icon: up
---

# API v6.0

Here is a list of breaking changes that happened during the API v6.0 period when differing versions of Terminaux introduced breaking changes.

## From 5.4.x to 6.0.x

Between the 5.4.x and 6.0.x version range, we've made the following breaking changes:

### `ConsoleFilterInfo` class added

{% code title="ConsoleFilter.cs" lineNumbers="true" %}
```csharp
public static bool IsInFilter(string query, ConsoleFilterType type, ConsoleFilterSeverity severity, out (Regex? query, ConsoleFilterType type, ConsoleFilterSeverity severity, string justification) queryTuple)
public static bool IsInFilter(Regex query, ConsoleFilterType type, ConsoleFilterSeverity severity, out (Regex? query, ConsoleFilterType type, ConsoleFilterSeverity severity, string justification) queryTuple)
public static (Regex? query, ConsoleFilterType type, ConsoleFilterSeverity severity, string justification)[] GetFilteredQueries()
```
{% endcode %}

The `ConsoleFilterInfo` class has been added to Terminaux's console filtering feature that lists all filter info, including the filter type, the query to match, and so on. This is to make the above functions easier to use by simplifying a tuple to a class.

{% hint style="info" %}
You'll have to change how your application uses these functions by changing the appropriate calls and references.
{% endhint %}

### `WideChar` moved to Textify

{% code title="WideChar.cs" lineNumbers="true" %}
```csharp
public struct WideChar : IEquatable<WideChar>, IComparable<WideChar>
```
{% endcode %}

We've moved `WideChar` struct to the latest version of Textify that Terminaux now uses. This is to enable more applications using this structure for wide characters.

{% hint style="info" %}
Just change the `using` clause to point to `Textify.General.Structures`.
{% endhint %}

### Centered writers refactored

{% code title="CenteredTextColor.cs" lineNumbers="true" %}
```csharp
public static class CenteredTextColor
{
    public static void WriteCentered(int top, string Text, int leftMargin = 0, int rightMargin = 0, params object[] Vars) { }
    public static void WriteCenteredColor(int top, string Text, Color Color, int leftMargin = 0, int rightMargin = 0, params object[] Vars) { }
    (...)
}
```
{% endcode %}

{% code title="CenteredFigletTextColor.cs" lineNumbers="true" %}
```csharp
public static class CenteredFigletTextColor
{
    public static void WriteCenteredFiglet(int top, FigletFont FigletFont, string Text, int leftMargin = 0, int rightMargin = 0, params object[] Vars) { }
    public static void WriteCenteredFigletColor(int top, FigletFont FigletFont, string Text, Color Color, int leftMargin = 0, int rightMargin = 0, params object[] Vars) { }
    (...)
}
```
{% endcode %}

The above centered writers have been replaced by more flexible aligned writers that allow you to not only write text to the console at the center of the console, but you can also align it either to the left, to the middle, or to the right.

* `CenteredTextColor` -> `AlignedTextColor`
* `CenteredFigletTextColor` -> `AlignedFigletTextColor`

{% hint style="info" %}
If you still want to write text at the center of the console, you can use the `TextAlignment.Middle` enumeration.
{% endhint %}

### Shapes and `IGeometricShape` moved to `CyclicWriters`

{% code title="IGeometricShape.cs" lineNumbers="true" %}
```csharp
namespace Terminaux.Graphics
```
{% endcode %}

{% code title="Shape source codes" lineNumbers="true" %}
```csharp
namespace Terminaux.Graphics.Shapes
```
{% endcode %}

As part of the renderable cyclic writers that can be contained in a single `Container` instance, we've moved all the shapes and their interface, `IGeometricShape`, as both that interface and `IStaticRenderable` work similarly to each other. The shape feature and its interface was a prelude to the static renderable writers.

{% hint style="info" %}
You just need to change the `using` clause to point to `Terminaux.Writer.CyclicWriters.Shapes`. You can still tell the difference between a static renderable and a geometric shape by examining the implemented interfaces, since we don't plan to remove the geometric shape interface.
{% endhint %}

### Writer tools moved to `CyclicWriters`

```csharp
namespace Terminaux.Writer.FancyWriters.Tools
// or
namespace Terminaux.Writer.MiscWriters.Tools
```

The following writer tools have been moved to the `Terminaux.Writer.CyclicWriters.Renderer.Tools` namespace to unify all the writer tools for consistency:

* `AsciinemaRepresentation` (newly introduced)
* `BorderSettings`
* `CellOptions`
* `ChartElement`
* `FigletTextTools`
* `Keybinding`
* `PowerLineSegment`
* `PowerLineTools`
* `PredefinedBorders`
* `TextAlignment` (newly introduced)
* `TextSettings`
* `TextWriterTools`

{% hint style="info" %}
None of the above classes and enumerations are affected at the time of the move, but you'll have to change the `using` clause to point to the right namespace.
{% endhint %}

### Wrapped writer removed

{% code title="TextWriterWrappedColor.cs" lineNumbers="true" %}
```csharp
public static class TextWriterWrappedColor
```
{% endcode %}

Due to new features being introduced with the introduction of the bounded text, we've decided to remove this writer. It'll be re-introduced in a better form in one of the Terminaux releases, and we promise you with new features.

As a result, the `ListWriterColor` no longer supports wrapping, as we've removed the `Wrap` parameter. As Nitrocid KS extensively uses this feature, especially for wrapping commands, this means that Terminaux 6.x series higher than 6.0 will be used in the next few versions of Nitrocid KS.

{% hint style="warning" %}
Please be patient while we're working on a re-write of the wrapped writer in a future 6.x version of Terminaux.
{% endhint %}

### `KeybindingsWriter` refactored

{% code title="KeybindingsWriter.cs" lineNumbers="true" %}
```csharp
public static void ShowKeybindingInfoboxPlain(Keybinding[] keybindings, params object[] vars)
public static void ShowKeybindingInfoboxPlain(Keybinding[] keybindings, BorderSettings settings, params object[] vars)
public static void ShowKeybindingInfobox(Keybinding[] keybindings, params object[] vars)
public static void ShowKeybindingInfoboxColor(Keybinding[] keybindings, Color InfoBoxColor, params object[] vars)
public static void ShowKeybindingInfoboxColorBack(Keybinding[] keybindings, Color InfoBoxColor, Color BackgroundColor, params object[] vars)
public static void ShowKeybindingInfobox(Keybinding[] keybindings, BorderSettings settings, params object[] vars)
public static void ShowKeybindingInfoboxColor(Keybinding[] keybindings, BorderSettings settings, Color InfoBoxColor, params object[] vars)
public static void ShowKeybindingInfoboxColorBack(Keybinding[] keybindings, BorderSettings settings, Color InfoBoxColor, Color BackgroundColor, params object[] vars)
public static void ShowKeybindingInfoboxPlain(string title, Keybinding[] keybindings, params object[] vars)
public static void ShowKeybindingInfoboxPlain(string title, Keybinding[] keybindings, BorderSettings settings, params object[] vars)
public static void ShowKeybindingInfobox(string title, Keybinding[] keybindings, params object[] vars)
public static void ShowKeybindingInfoboxColor(string title, Keybinding[] keybindings, Color InfoBoxTitledColor, params object[] vars)
public static void ShowKeybindingInfoboxColorBack(string title, Keybinding[] keybindings, Color InfoBoxTitledColor, Color BackgroundColor, params object[] vars)
public static void ShowKeybindingInfobox(string title, Keybinding[] keybindings, BorderSettings settings, params object[] vars)
public static void ShowKeybindingInfoboxColor(string title, Keybinding[] keybindings, BorderSettings settings, Color InfoBoxTitledColor, params object[] vars)
public static void ShowKeybindingInfoboxColorBack(string title, Keybinding[] keybindings, BorderSettings settings, Color InfoBoxTitledColor, Color BackgroundColor, params object[] vars)
public static string RenderKeybindingHelpText(Keybinding[] keybindings)
```
{% endcode %}

We have moved the `KeybindingsWriter` functionality to its own cyclic writer class. Also, we've moved the above functions to the `KeybindingTools` static class.

{% hint style="info" %}
If you use these functions, consider using the `KeybindingTools` class.
{% endhint %}

### Slow writers moved to `ConsoleWriters`

{% code title="TextWriter[Where]SlowColor.cs" lineNumbers="true" %}
```csharp
namespace Terminaux.Writer.DynamicWriters
```
{% endcode %}

These dynamic writers have been moved to the normal console writers namespace, because we're cleaning up the writer base in versions between Terminaux 6.0 and a future major release of this library.

{% hint style="info" %}
Just change the `using` clause to point to `Terminaux.Writer.ConsoleWriters`.
{% endhint %}

### `Filled` property removed from `IGeometricShape`

{% code title="IGeometricShape.cs" lineNumbers="true" %}
```csharp
bool Filled { get; }
```
{% endcode %}

We have removed the above property from the geometric shape interface, because there are shapes, such as arcs, that can't have this property due to high flexibility.

{% hint style="info" %}
If you want to continue using this property, implement it in individual geometric shape classes. You won't be able to call it from a general interface variable, so you'll have to cast it to a class that has this property first.
{% endhint %}

### Changed how shapes render

Due to the new canvas class being used to render a shape, you'll notice that the shapes will appear stretched. This is due to the width not being treated as a multiple of two when creating shape instances due to canvases defaulting to full width. The following shapes are affected based on width:

* Ellipsis
* Parallelogram
* Rectangle
* Square
* Line
* Triangle
* Trapezoid

{% hint style="info" %}
Divide the width by two as in below example (adapt this to your shape instance):

```diff
-var ellipsis = new Ellipsis(40, 20, 4, 2, true, ConsoleColors.Red);
-var ellipsis2 = new Ellipsis(20, 20, 46, 2, false, ConsoleColors.Aqua);
+var ellipsis = new Ellipsis(20, 20, 4, 2, true, ConsoleColors.Red);
+var ellipsis2 = new Ellipsis(10, 20, 46, 2, false, ConsoleColors.Aqua);
```
{% endhint %}

### `NerdFontsTools` moved

```csharp
namespace Terminaux.Graphics.NerdFonts
{
    /// <summary>
    /// Nerd Fonts tools
    /// </summary>
    public static partial class NerdFontsTools
    {
        (...)
    }
}
```

As we're phasing out `Terminaux.Graphics` due to the cyclic writers being introduced to the Terminaux 6.0 line, we've decided to move this class to a new namespace, `Terminaux.Writer.CyclicWriters.Renderer.Tools`.

{% hint style="info" %}
Just change your `using` clause to point to the new namespace.
{% endhint %}

### Transformation formula interface publicized

{% code title="TransformationTools.cs" lineNumbers="true" %}
```csharp
public static Color RenderColorBlindnessAware(Color color, TransformationFormula formula, double severity)
```
{% endcode %}

{% code title="TransformationFormula.cs" lineNumbers="true" %}
```csharp
public enum TransformationFormula
```
{% endcode %}

To allow for multiple transformations to be done seamlessly, we've decided to publicize the `ITransformationFormula` interface and the `BaseTransformationFormula` class that provides the signature prototype needed for the transformation code. Because we've made these public, we've demoted the `TransformationFormula` enumeration from `public` to `internal` visibility, causing us to remove the `RenderColorBlindnessAware()` function.

{% code title="ColorSettings.cs" lineNumbers="true" %}
```csharp
public bool EnableColorTransformation { get; set; } = false;
public TransformationFormula ColorTransformationFormula { get; set; } = TransformationFormula.Protan;
public double ColorBlindnessSeverity ...
```
{% endcode %}

In addition to that, we've also removed the above properties so that you can finally specify not only a list of transformation formulas, but you can also specify their own density ranging from 0.0 to 0.1.

{% hint style="info" %}
To continue using this feature, you must change the `Transformations` value in the `Color` instance, passing it an array of transformation formula classes that you desire to use.
{% endhint %}

### `ScreenPart` obsolete functions removed

{% code title="ScreenPart.cs" lineNumbers="true" %}
```csharp
public void LeftPosition(int left)
public void TopPosition(int top)
public void Position(int left, int top)
public void ForegroundColor(Color color, bool forceTrue = false)
public void BackgroundColor(Color color, bool forceTrue = false)
public void ResetColors()
public void ResetForegroundColor()
public void ResetBackgroundColor()
```
{% endcode %}

The obsolete functions that added VT sequences to the dynamic screen part buffer have been removed, because of the introduction of the `AddDynamicText()` function.

{% hint style="info" %}
You can achieve similar results to that of executing these functions by using the appropriate functions and properties.
{% endhint %}
