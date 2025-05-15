---
description: Breaking changes for API v2.0
icon: up
---

# API v2.0

Here is a list of breaking changes that happened during the API v2.0 period when differing versions of Terminaux introduced breaking changes.

## From 1.12.x to 2.0.x

Between the 1.12.x and 2.0.x version range, we've made the following breaking changes:

### Removed `Terminaux.Figgle`

Figgle was not maintained by the original developer for a long time, so we've forked this library to create Figletize, and its documentation can be found here:

{% content-ref url="https://app.gitbook.com/o/fj052nYlsxW9IdL3bsZj/s/ImPNBShiE2aqA6pDyeiZ/" %}
[Figletize - Manual](https://app.gitbook.com/o/fj052nYlsxW9IdL3bsZj/s/ImPNBShiE2aqA6pDyeiZ/)
{% endcontent-ref %}

{% hint style="info" %}
It's advisable to use the built-in Figlet tools instead of using Terminaux.Figgle as it's considered legacy.
{% endhint %}

### Removed the old color wheel

The old color wheel wasn't updated to benefit from the latest Terminaux improvements, so we had to remove the old color wheel to reduce the maintenance burden.

{% hint style="info" %}
It's advisable to use the newer color selector as it's more up to date.
{% endhint %}

### Implemented a proper console wrapper

{% code title="ConsoleWrappers.cs" lineNumbers="true" %}
```csharp
public static class ConsoleWrappers
```
{% endcode %}

A proper console wrapper was needed to effortlessly call the console wrapper functions that Terminaux uses to delegate the `Console` functions so that appropriate writing methods are used. This is done in an attempt to achieve consistency in behavior across all the Terminaux functions.

Although the action-based console wrappers can still be set, you can no longer call them from your application. Instead, you must use the newer `ConsoleWrapper` class to more accurately represent the properties and the functions and to avoid confusion.

{% hint style="info" %}
To be able to achieve a successful migration, you must replace the following calls (left is `ConsoleWrapperTools`, and right is `ConsoleWrapper`):

* `ActionCursorLeft` -> `CursorLeft`
* `ActionSetCursorLeft` -> `CursorLeft`
* `ActionCursorTop` -> `CursorTop`
* `ActionSetCursorTop` -> `CursorTop`
* `ActionBufferHeight` -> `BufferHeight`
* `ActionCursorVisible` -> `CursorVisible`
* `ActionKeyAvailable` -> `KeyAvailable`
* `ActionClear` -> `Clear`
* `ActionSetCursorPosition` -> `SetCursorPosition`
* `ActionBeep` -> `Beep`
* `ActionReadKey` -> `ReadKey`
* `ActionWriteChar` -> `Write`
* `ActionWriteString` -> `Write`
* `ActionWriteParameterized` -> `Write`
* `ActionWriteLine` -> `WriteLine`
* `ActionWriteString` -> `WriteLine`
* `ActionWriteLineParameterized` -> `WriteLine`
{% endhint %}

### Textify is used for VT sequence feature

{% code title="Affected classes" lineNumbers="true" %}
```csharp
public static class ApcSequences
public static class C1Sequences
public static class CsiSequences
public static class DcsSequences
public static class EscSequences
public static class OscSequences
public static class PmSequences
public static class VtSequenceBasicChars
public static class VtSequenceBuilderTools
public enum VtSequenceSpecificTypes
public static class VtSequenceRegexes
public static class VtSequenceTools
public enum VtSequenceType
```
{% endcode %}

Since Textify was released as a brand new library for .NET, which was a library that moved all text-related tools from various libraries of our own, we've decided to move these classes to Textify, removing them from Terminaux entirely. This is to allow diversity of development for the two libraries and to allow interoperability.

{% hint style="info" %}
Terminaux will pull Textify as a dependency when you install the 2.0 version, so you just have to change the usings to Textify's namespace before you can use the above classes again.

If you're impatient for the next version of Terminaux, you can install Textify manually and use these functions. Be aware that you may need to resolve the conflicts.
{% endhint %}

### Moved `Inputs` to the root namespace

{% code title="Affected files" lineNumbers="true" %}
```csharp
namespace Terminaux.Reader.Inputs
```
{% endcode %}

`Inputs` hosted several of the input tools to allow you to ask users a question in several of the forms, including the selection choices, the modal infoboxes, and so on.

However, we've moved the entire `Inputs` namespace to `Terminaux.Inputs` as it just uses the console reader that Terminaux implements and not modifies it.

{% hint style="info" %}
None of the classes and their functions have changed. You just have to update the imports to use `Terminaux.Inputs` instead of the old namespace shown above.
{% endhint %}

### Figlet selector moved to `Inputs.Styles`

{% code title="FigletSelector.cs" lineNumbers="true" %}
```csharp
namespace Terminaux.Figlet
```
{% endcode %}

Since the legacy Figlet code has been removed from Terminaux and the figlet selector was considered as an input method to select a Figlet font, we've decided to move the figlet selector to `Inputs.Styles`. This is to allow better organization.

{% hint style="info" %}
None of the functions have changed during this movement. You need to update your imports to point to `Terminaux.Inputs.Styles`.
{% endhint %}

### Removed `ColorSeqException`

{% code title="ColorSeqException.cs" lineNumbers="true" %}
```csharp
internal class ColorSeqException
```
{% endcode %}

ColorSeq was replaced by Terminaux, because the latter library works on managing your terminal applications by providing you several of the nice terminal tools, such as the efficient management of colors, input reading, and much more.

We've removed `ColorSeqException` as an internal class, but we need to put this change here to tell the developers that they can finally handle the `Color` errors easily by catching all `TerminauxException` errors.

{% hint style="info" %}
You no longer need to use reflection to find out the type name of the removed exception, because you can catch `TerminauxException`, which the color management system now uses.
{% endhint %}

### `ConsolePlatform`'s `NewLine`

{% code title="ConsolePlatform.cs" lineNumbers="true" %}
```csharp
public static string NewLine
```
{% endcode %}

From now on, this property has been removed as it isn't used except the console checker. Also, the usage of Textify in the v2.0 version of Terminaux means that you need not to resort to cryptic hacks to get the new lines working properly.

{% hint style="info" %}
If you still make use of this property, replace its call with either the `\n` string literal (which represents a new line and is platform-agnostic), or use `Environment.NewLine` if you want to use platform-specific newlines.
{% endhint %}

### Relocated color model conversion tools

{% code title="Color.cs" lineNumbers="true" %}
```csharp
public CyanMagentaYellowKey CMYK =>
    RGB.ConvertToCmyk();
(...)
```
{% endcode %}

The color model conversion tools have been reworked to become easier to use than the Terminaux v1.x version series, which use constructors that do the conversion. It was discovered that it was not so easy to maintain, so we've decided to relocate these to their own dedicated classes, such as CMY conversion tools (`CmyConversionTools`), so that they can be used by Terminaux v2.0 applications.

They are also titled appropriately so that you can better understand what is the source and what is the target unit being used to convert the source color model to. More documentation is found in its appropriate page.

{% hint style="info" %}
Change all the calls to the color model-specific properties to refer to the conversion tools that focus on a target that you want. For example, converting RGB to CMY requires usage of the `CmyConversionTools` class.
{% endhint %}

### Reworked transformation method switch

{% code title="ColorTools.cs" lineNumbers="true" %}
```csharp
public static bool EnableSimpleColorTransformation { get; set; } = false;
```
{% endcode %}

The above switch doesn't explain the motive of enabling or disabling except "simple," which means a simple way of transforming the color. However, it doesn't explain what formula does Terminaux use unless you use the API documentation.

So, we've decided to remove this and replace it with the `TransformationMethod` enumeration to make things more clear.

{% hint style="info" %}
Replace all calls to the above boolean property with the `ColorTransformationMethod` property.

```csharp
public static TransformationMethod ColorTransformationMethod { get; set; } = TransformationMethod.Brettel1997;
```
{% endhint %}

### Removed `IsDark/Bright` for `ConsoleColorsInfo`

{% code title="ConsoleColorsInfo.cs" lineNumbers="true" %}
```csharp
public bool IsBright { get; }
public bool IsDark { get; }
```
{% endcode %}

We've removed `IsDark/Bright` for the above class because they are just repeat properties for the color brightness that the `Color` instance would have exposed properly, so we've decided to replace it with a `Color` property to get access to such flag.

{% hint style="info" %}
In order to get access to this data, you need to access the `Color` property and get the value of `Brightness`.
{% endhint %}

### Renamed color blindness type

{% code title="Deficiency.cs" lineNumbers="true" %}
```csharp
public enum Deficiency
```
{% endcode %}

We've renamed the color blindness deficiency type enumeration to better represent the type of formula that is going to be used. This is to allow more formulas to be more accurately represented.

Initially, it was touted to be a color deficiency type of either protan, deutan, or tritan. However, more color transformation formulas were added, such as monochromacy and inverted, which is why we've renamed the color blindness type to `TransformationFormula`.

{% hint style="info" %}
The color blindness type enumeration name has been changed, along with its namespace. You need to update the following:

* Imports: `Terminaux.Colors.Accessibility` -> `Transformation`
* References: `Deficiency` -> `TransformationFormula`
{% endhint %}

## From 2.0.x to 2.1.x

Between the 2.0.x and 2.1.x version range, we've made the following breaking changes:

### Titled variants of infoboxes merged

```csharp
public static class InfoBoxTitledButtonsColor
public static class InfoBoxTitledColor
public static class InfoBoxTitledInputColor
public static class InfoBoxTitledProgressColor
public static class InfoBoxTitledSelectionColor
public static class InfoBoxTitledSelectionMultipleColor
```

The titled variants of all informational box types have been moved to a completely different place, which is their parent class, like `InfoBoxColor`. This ensures that maintenance is not a burden when it comes to maintaining them.

We've also done a refactor so that the infobox code occurs only once to reduce the amount of bugs and regressions that may emerge when updating related code.

{% hint style="info" %}
To continue using the titled variants, you'll have to remove the "Titled" word from both the class reference and the function reference, like this:

* `InfoBoxTitledButtonsColor.WriteInfoBoxTitledButtons()` -> `InfoBoxButtonsColor.WriteInfoBoxButtons()`

You'll have to replace `Terminaux.Inputs.Styles.InfoboxTitled` in your usings with `Terminaux.Inputs.Styles.Infobox`.
{% endhint %}

### Border and box frame color writers refactored

```csharp
public static class BorderTextColor
public static class BoxFrameTextColor
```

When we wanted to make the titled borders and box frames, we wanted to make titled informational boxes. However, after making several types of informational boxes and their titled variants, we've discovered that there were a lot of repeated code for different situations.

So, we've decided to do the same thing to the two classes as we've done to the infoboxes in the past release; condense them to a single class and refactor them to reduce the maintenance burden.

{% hint style="info" %}
Usually, you'll only have to change all references to the two above classes to their normal classes:

* `BorderTextColor` -> `BorderColor`
* `BoxFrameTextColor` -> `BoxFrameColor`

In case you see unexpected rendering behavior, adjust the parameters as necessary.
{% endhint %}

### Specifier parser function signature changed

{% code title="ParsingTools.cs" lineNumbers="true" %}
```csharp
public static RedGreenBlue ParseSpecifier(string specifier)
```
{% endcode %}

In completion of the specifier parser implementation and refactoring, we've decided to change the signature of this function to satisfy the recent changes done to various parsing functions, thus further simplifying the `Color` constructor to its bare minimum.

{% hint style="info" %}
You don't have to change the parameters. However, you'll need to get the two values, depending on your stance:

* `rgb`: For the RGB component of the parsed color
* `cci`: For color information for 256 and 16 color modes
{% endhint %}

### Implemented color settings class

```csharp
public static bool EnableColorTransformation { get; set; } = false;
public static bool UseTerminalPalette { get; set; } = true;
public static TransformationFormula ColorTransformationFormula { get; set; } = TransformationFormula.Protan;
public static TransformationMethod ColorTransformationMethod { get; set; } = TransformationMethod.Brettel1997;
public static double ColorBlindnessSeverity (...)
```

For simplification of the color management code, instead of using the color tools as a state machine, we need to actually make this part of Terminaux settings-agnostic to reduce complications related to this part.

As a result, we had to spray the settings argument everywhere to allow Terminaux programs to either set their own settings for colors when making a new color instance or to use the global settings that can be manipulated with by the user program.

{% hint style="info" %}
You'll have to either use the global settings property from `ColorTools`, `GlobalSettings`, or make a new `ColorSettings` instance with your own settings. If you use the latter, pass it with your settings instance when creating a new `Color` instance.
{% endhint %}

## From 2.1.x to 2.2.x

Between the 2.1.x and 2.2.x version range, we've made the following breaking changes:

### Removed non-standalone char write wrapper

{% code title="ConsoleWrapperTools.cs" lineNumbers="true" %}
```csharp
public static Action<char, TermReaderSettings> ActionWriteCharNonStandalone
```
{% endcode %}

The non-standalone character writer wrapper has been removed because the terminal reader doesn't make any use of it as part of the recent refactors that were done in the 2.0.0 development cycle. This resulted in this character writer being useless.

So, we've removed this wrapper as a result to reduce complexity.

{% hint style="info" %}
You can no longer set up a wrapper for this kind of writer.
{% endhint %}

### Highlighted text writer moved

{% code title="TextWriterColor.cs" lineNumbers="true" %}
```csharp
public static void Write(string Text, bool Line, bool Highlight, params object[] vars)
public static void WriteColor(string Text, bool Line, bool Highlight, ConsoleColors color, params object[] vars)
public static void WriteColorBack(string Text, bool Line, bool Highlight, ConsoleColors ForegroundColor, ConsoleColors BackgroundColor, params object[] vars)
public static void WriteColor(string Text, bool Line, bool Highlight, Color color, params object[] vars)
public static void WriteColorBack(string Text, bool Line, bool Highlight, Color ForegroundColor, Color BackgroundColor, params object[] vars)
public static void WriteForReaderPlain(string Text, TermReaderSettings settings, params object[] vars)
public static void WriteForReaderPlain(string Text, TermReaderSettings settings, bool Line, params object[] vars)
public static void WriteForReader(string Text, TermReaderSettings settings, bool Line, bool Highlight, params object[] vars)
public static void WriteForReaderColor(string Text, TermReaderSettings settings, bool Line, bool Highlight, ConsoleColors color, params object[] vars)
public static void WriteForReaderColorBack(string Text, TermReaderSettings settings, bool Line, bool Highlight, ConsoleColors ForegroundColor, ConsoleColors BackgroundColor, params object[] vars)
public static void WriteForReaderColor(string Text, TermReaderSettings settings, bool Line, bool Highlight, Color color, params object[] vars)
public static void WriteForReaderColorBack(string Text, TermReaderSettings settings, bool Line, Color ForegroundColor, Color BackgroundColor, params object[] vars)
public static void WriteForReaderColorBack(string Text, TermReaderSettings settings, bool Line, bool Highlight, Color ForegroundColor, Color BackgroundColor, params object[] vars)
```
{% endcode %}

The highlighted text writer has been moved to its own class to reduce complexity and allow for simplicity. This reduces the maintenance burden for future Terminaux releases.

Also, we've made changes as to how to handle color resetting at the end of the write so that your app doesn't have to manually call the `ResetColors()` function.

{% hint style="info" %}
If you want to use the highlighted writer, you can use the brand new class, `TextWriterHighlightedColor`.
{% endhint %}

## From 2.2.x to 2.4.x

Between the 2.2.x and 2.4.x version range, we've made the following breaking changes:

### Color contrast class added

{% code title="ColorTools.cs" lineNumbers="true" %}
```csharp
public static bool IsSeeable(ColorType type, int colorLevel, int colorR, int colorG, int colorB)
```
{% endcode %}

We've moved the `IsSeeable` function as part of the addition of the color contrast tools to the `ColorContrast` static class so that it becomes part of the color contrast tools.

{% hint style="info" %}
The functionality of the function hasn't changed. You just need to change the reference to this function from `ColorTools` to `ColorContrast`.
{% endhint %}

### Moved ConsoleColors\[Info] to Colors.Data

{% code title="ConsoleColors.cs" lineNumbers="true" %}
```csharp
namespace Terminaux.Colors
```
{% endcode %}

{% code title="ConsoleColorsInfo.cs" lineNumbers="true" %}
```csharp
namespace Terminaux.Colors
```
{% endcode %}

We've moved the two classes, `ConsoleColors` and its associated `Info` class, to `Terminaux.Colors.Data` as they're part of the console colors information gathering for both 16-color and 256-color information.

## From 2.4.x to 2.5.x

Between the 2.4.x and 2.5.x version range, we've made the following breaking changes:

### YIQ values changed

{% code title="LumaChromaUv.cs" lineNumbers="true" %}
```csharp
public double Luma { get; private set; }
public double ChromaU { get; private set; }
public double ChromaV { get; private set; }
```
{% endcode %}

{% code title="LumaInPhaseQuadrature.cs" lineNumbers="true" %}
```csharp
public double Luma { get; private set; }
public double InPhase { get; private set; }
public double Quadrature { get; private set; }
```
{% endcode %}

The values in the YIQ color model have been changed to store natural integer numbers that range from 0 to 255 instead of the more-accurate double-precision floating system. This is to shorten the specifiers for the YIQ values. The three values used to hold the following ranges:

* Luma: `0.0` -> `0.1`
* In-phase: `-0.5957` -> `0.5957`
* Quadrature: `-0.5226` -> `0.5226`

{% hint style="info" %}
You'll have to re-write the specifiers so that all the components range from `0` to `255`. In-phase and quadrature values of `0` are `128` in the new range implemented in Terminaux 2.5.0 and higher.
{% endhint %}

### Moved X11-related functions to `ConversionTools`

{% code title="ColorTools.cs" lineNumbers="true" %}
```csharp
public static ConsoleColors TranslateToX11ColorMap(ConsoleColor color)
public static ConsoleColor TranslateToStandardColorMap(ConsoleColors color)
public static ConsoleColor CorrectStandardColor(ConsoleColor color)
```
{% endcode %}

These functions used to reside on `ColorTools` before they're moved to `ConversionTools`, which is a new class that Terminaux 2.5.0 introduced. `ConversionTools` was meant to hold general color conversion tools.

{% hint style="info" %}
The functionality for these functions has not changed. You'll have to update the references to `ConversionTools`.
{% endhint %}

### Moved `RenderColorBlindnessAware()`

{% code title="ColorTools.cs" lineNumbers="true" %}
```csharp
public static Color RenderColorBlindnessAware(Color color, TransformationFormula formula, double severity, TransformationMethod method = TransformationMethod.Brettel1997)
```
{% endcode %}

The `RenderColorBlindnessAware` function got implemented during Terminaux 1.x to simplify making new `Color` instances with the color blindness (or transformation) applied according to the manually-selected color transformation formula and their options.

This function, however, has been moved to `TransformationTools` instead of `ColorTools` to more accurately describe the purpose of this function.

{% hint style="info" %}
The functionality for this function has not changed. You'll have to update the references to `TransformationTools`.
{% endhint %}

### Removed obsolete functions

{% code title="ColorTools.cs" lineNumbers="true" %}
```csharp
public static string ConvertFromHexToRGB(string Hex)
public static string ConvertFromRGBToHex(string RGBSequence)
public static string ConvertFromRGBToHex(int R, int G, int B)
```
{% endcode %}

These three obsolete functions became obsolete when better solutions were implemented during the whole Terminaux development lifetime, which resulted in properties like Color's `Hex` and `PlainSequence` dynamically returning appropriate values according to the specified specifier.

{% hint style="info" %}
To migrate away from the three functions, you'll have to follow the migration steps:

* For the first function, create a new `Color` instance with the specified `Hex` value and call this instance's `PlainSequence` property.
* For the second and the third functions, create a new `Color` instance with either the specified `RGBSequence` value or the three RGB values and call this instance's `Hex` property.
{% endhint %}

## From 2.5.x to 2.6.x

Between the 2.5.x and 2.6.x version range, we've made the following breaking changes:

### Removed R, G, and B properties (and normalized) from `Color`

{% code title="Color.cs" lineNumbers="true" %}
```csharp
public int R =>
    RGB.R;
public int G =>
    RGB.G;
public int B =>
    RGB.B;
public double RNormalized =>
    RGB.RNormalized;
public double GNormalized =>
    RGB.GNormalized;
public double BNormalized =>
    RGB.BNormalized;
```
{% endcode %}

To simplify the `Color` class, we've removed the above properties as they wrap against the `RGB` property, which contains the above properties. This is also done to achieve consistency.

{% hint style="info" %}
All you have to do is to change all the references to these properties so that they point to the `RGB` property instead of directly.

```diff
-int gray = (int)(mono.R * width);
+int gray = (int)(mono.RGB.R * width);
```
{% endhint %}

## From 2.6.x to 2.7.x

Between the 2.6.x and 2.7.x version range, we've made the following breaking changes:

### `ReadKeyTimeout()` no longer throws a removed exception

{% code title="Input.cs" lineNumbers="true" %}
```csharp
public static ConsoleKeyInfo ReadKeyTimeout(bool Intercept, TimeSpan Timeout)
```
{% endcode %}

{% code title="TerminauxContinuableException.cs" lineNumbers="true" %}
```csharp
public class TerminauxContinuableException
```
{% endcode %}

`ReadKeyTimeout()` no longer throws above exception when the user didn't press any key in the timely manner. Instead, it returns a default `ConsoleKeyInfo` instance (that indicates that there is no key to be pressed) with a boolean variable in the same return type as a tuple that indicates whether a key has been pressed or not.

However, as the above exception wasn't used anymore by Terminaux itself, we've decided to remove it, leaving only the `TerminauxException` class being used.

{% hint style="info" %}
You'll have to change the variable in which will hold the value of `ReadKeyTimeout()`. As a bonus, you'll get two variables in one function:

* The resulting key (`ConsoleKeyInfo`)
* Key has been pressed or not (`boolean`)
{% endhint %}

### Button infoboxes now handle choice info

{% code title="InfoBoxButtonsColor.cs" lineNumbers="true" %}
```csharp
public static int WriteInfoBoxButtonsPlain(string[] buttons, string text, params object[] vars)
public static int WriteInfoBoxButtonsPlain(string[] buttons, string text, char UpperLeftCornerChar, char LowerLeftCornerChar, char UpperRightCornerChar, char LowerRightCornerChar, char UpperFrameChar, char LowerFrameChar, char LeftFrameChar, char RightFrameChar, params object[] vars)
(...)
public static int WriteInfoBoxButtonsColorBack(string title, string[] buttons, string text, char UpperLeftCornerChar, char LowerLeftCornerChar, char UpperRightCornerChar, char LowerRightCornerChar, char UpperFrameChar, char LowerFrameChar, char LeftFrameChar, char RightFrameChar, Color InfoBoxTitledButtonsColor, Color BackgroundColor, params object[] vars)
```
{% endcode %}

The button infoboxes now handle the choice info instead of simple string array of buttons, making these infoboxes more flexible than before. On the contrary, we had to change the signature of all the functions found inside `InfoBoxButtonsColor` to hold the `InputChoiceInfo` array that stores all the possible choices.

{% hint style="info" %}
You'll have to change how to define the buttons from passing it a simple array of strings to an array of `InputChoiceInfo` instances that contain info about your choices.
{% endhint %}
