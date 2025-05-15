---
description: We need colors!
icon: palette
---

# Color Sequences

Terminaux provides a functionality to generate color sequences with the help of the VT sequences. It allows you to generate a color with three modes:

* 16 colors
* 256 colors
* 16-bit colors (true color)

{% hint style="info" %}
Please note that some consoles don't support 256 colors and/or 16-bit colors, and some of them might implement these poorly (Terminal.app (`Apple_Terminal`) for example).

Support for 16-bit colors and 256-colors requires a compatible terminal emulator.

* Windows systems: ConEmu, Windows 10 cmd.exe with VT sequences enabled
* Linux systems: xterm, GNOME Terminal, Konsole, etc.
* macOS systems: iTerm2 only
{% endhint %}

This functionality contains several functions that you can make use of in your console application:

* Building a `Color` instance that supports RGB and 255-color modes
* Getting console color information from the 255-color mode
* Simulating color-blindness during compilation
* Applying transparency using the `Opacity` settings in the `ColorSettings` instance

More functionality is available in the right pane for conversion, parsing, and more.

## Building a `Color` instance

You can build your own `Color` instance for usage in your console application. There are various ways to build it:

```csharp
public Color(int R, int G, int B)
public Color(int R, int G, int B, ColorSettings settings)
public Color(ConsoleColors ColorDef)
public Color(ConsoleColors ColorDef, ColorSettings settings)
public Color(ConsoleColor ColorDef)
public Color(ConsoleColor ColorDef, ColorSettings settings)
public Color(int ColorNum)
public Color(int ColorNum, ColorSettings settings)
public Color(string ColorSpecifier)
public Color(string ColorSpecifier, ColorSettings settings)
```

The `ColorSpecifier` can be of the syntax:

* `<num>`
  * `<num>` should be of the range between 0 and 255
  * If `<num>` is positive and larger than 255, it describes the color code from 256 up to 16777215 for true color instances, and anything higher than it will be wrapped to `0;0;0` and counting.
* `<rrr>;<ggg>;<bbb>`
  * `<rrr>`, `<ggg>`, and `<bbb>` should be of the range between 0 and 255
* `cmyk:<ccc>;<mmm>;<yyy>;<kkk>`
  * `<ccc>`, `<mmm>`, `<yyy>`, and `<kkk>` should be of the range between 0 and 100
* `cmy:<ccc>;<mmm>;<yyy>`
  * `<ccc>`, `<mmm>`, and `<yyy>` should be of the range between 0 and 100
* `hsl:<hhh>;<sss>;<lll>`
  * `<hhh>` should be of the range between 0 and 360 in degrees and not radians
  * `<sss>` and `<lll>` should be of the range between 0 and 100
* `hsv:<hhh>;<sss>;<vvv>`
  * `<hhh>` should be of the range between 0 and 360 in degrees and not radians
  * `<sss>` and `<vvv>` should be of the range between 0 and 100
* `hwb:<hhh>;<www>;<bbb>`
  * `<hhh>` should be of the range between 0 and 360 in degrees and not radians
  * `<www>` and `<bbb>` should be of the range between 0 and 100
* `ryb:<rrr>;<yyy>;<bbb>`
  * `<rrr>`, `<yyy>`, and `<bbb>` should be of the range between 0 and 255, just like RGB.
* `yiq:<y>;<i>;<q>`
  * `<y>`, `<i>`, and `<q>` should be of the range between 0 and 255
* `yuv:<y>;<u>;<v>`
  * `<y>`, `<u>`, and `<v>` should be of the range between 0 and 255
* `xyz:<x>;<y>;<z>`
  * `<x>`, `<y>`, and `<z>` should be of the range between 0 and 100 in floating point units
* `#000000`
  * Hexadecimal representation of the color for HTML fans. You can also use the `#RGB` format, implying that the three digits represent:
    * R: Red color level converted to RR (F becomes FF)
    * G: Green color level converted to GG (F becomes FF)
    * B: Blue color level converted to BB (F becomes FF)
* `<ColorName>`
  * Color name from `ConsoleColors` enumeration

{% hint style="info" %}
You can also specify just a string, an integer, a `ConsoleColor`, or a `ConsoleColor` enumeration value when making a variable that holds the `Color` class like the following:

```csharp
Color ColorInstance = 18;
Color ColorInstance = "94;0;63";
Color ColorInstance = "#0F0F0F";
Color ColorInstance = "#F0F";
Color ColorInstance = "Magenta";
Color ColorInstance = ConsoleColors.Magenta;
Color ColorInstance = ConsoleColor.Magenta;
```
{% endhint %}

You can also get the color ID if you used color number from 0 to 255 by referencing the `ColorId` property. This property returns the nearest color ID for true color.

Additionally, you can choose whether to use your terminal emulator's color palette or to use the real colors that come from the true colors. By default, Terminaux chooses to use the terminal emulator's color palette to maintain consistency.

{% hint style="info" %}
In addition to the `PlainSequence` property, you can also use the `ToString()` function to get the same value from that property. This allows easier string interpolation, such as:

```csharp
BoxFrameTextColor.WriteBoxFrame($"Red, Green, and Blue: {selectedColor}", hueBarX, rgbRampBarY, boxWidth, boxHeight + 2);
```
{% endhint %}

### Getting RGB information

You can get the RGB information by simply calling the `RGB` property in the `Color` class. From there, you'll get an instance of `RedGreenBlue` that contains the `R`, `G`, `B`, and their normalized properties.

{% hint style="info" %}
You can also get this information from the color code using the `GetRgbFromColorCode()` function. The string representation can also be get using the `GetRgbSpecifierFromColorCode()` function.
{% endhint %}

You can also convert this color model instance to various color models, such as `RYB`, `CMY`, `YUV`, and `HSV`. In order to do this, consult the below page:

{% content-ref url="color-model-conversions.md" %}
[color-model-conversions.md](color-model-conversions.md)
{% endcontent-ref %}

### Getting color name and enumeration

You can get the color name for all the color types according to the nearest color that is selected in accordance to the X11 color map. Just use the `Name` property in a `Color` instance to get the color name.

{% hint style="info" %}
You can also get the nearest color information using either the `Color` instance, the RGB instance, or the RGB numbers using `GetNearestColor()` found in `ConsoleColorData`. Then, you can get this information to return the equivalent `Color` instance using the `Color` property.
{% endhint %}

For color enumeration, a `Color` class contains the following properties:

* `ColorEnum255`: Always populated related to the nearest matching color in the X11 color map. Can be used for `ConsoleColors` enumeration found within Terminaux.
* `ColorEnum16`: Is not populated for color IDs that exceed `15`. Can be used for `ConsoleColor` enumeration found within the C# standard library.

## Determining color brightness and contrast

You can check to see if a color is a light or a dark color using the `Brightness` property, which returns either of the following:

* `Dark`
* `Light`

There is a usage of this feature to determine the appropriate gray color, which contains a function found in the same class.

### Getting a gray color

You can get a gray color either for the current background color or for your custom background color using the `GetGray()` function. This allows you to easily get an appropriate color if you want to write something in it and you don't know what color to choose.

{% code title="ColorTools.cs" lineNumbers="true" %}
```csharp
public static Color GetGray()
public static Color GetGray(Color color)
```
{% endcode %}

## Getting console color information

You can get detailed information about the console color ranging from 0 to 255 by calling the `GetColorData()` function under the `ConsoleColorData` class:

```csharp
public static partial ConsoleColorData[] GetColorData();
```

Similarly, you can also get the web-safe color list by using the `WebSafeColors` class and the `GetColorList()` function. Properties that specify every color are also available under the same class.

## Color transformation

In order to simulate color blindness and other color transformation formulas, you can change the value of the `Transformations` property in the `Color` instance that you want to edit. This property is an array of transformation formula classes based on `BaseTransformationFormula` and `ITransformationFormula` that provide the following properties:

* `Frequency`
  * Specifies the density ranging between 0.0 and 1.0 from lowest to highest

{% hint style="info" %}
Depending on the `Render()` implementation of the transformation formula classes, it may or may not take note of the `Frequency` value. However, it's recommended to use it for general purposes, except if you can't do it for some reason.
{% endhint %}

Once the new class instance is created with the above property being populated with several transformations, you can get a transformed color.

### Getting a color contrast ratio

If you want to get a color contrast ratio, you can use the `GetContrast()` function found in the `TransformationTools` class that returns a contrast ratio in double-precision floating point value.

```csharp
public static double GetContrast(Color firstColor, Color secondColor)
```

This uses the `GetLuminance()` function, which is available in the public API. It lets you get the luminance rate for a color instance.

```csharp
public static double GetLuminance(Color color)
```

### Getting dark background of a color

If you want a darker version of your color, you can use the `GetDarkBackground()` function, passing it the source color that you want to darken in a new copy of the `Color` class. This is normally suitable for backgrounds that are responsive.

```csharp
public static Color GetDarkBackground(Color source)
```

### Getting light background of a color

If you want a lighter version of your color, you can use the `GetLightBackground()` function, passing it the source color that you want to lighten in a new copy of the `Color` class. This is normally suitable for backgrounds that are responsive.

```csharp
public static Color GetLightBackground(Color source)
```

### Saturation and Desaturation

You can saturate the color to appear lighter, and desaturate the color to appear darker. This manipulates the saturation value in the HSL representation of the color.

```csharp
public static Color Desaturate(Color source, int target)
public static Color Saturate(Color source, int target)
```

### Darkening and Lightening

You can darken the color to appear darker, and lighten the colors to appear lighter. This manipulates the lightness value in the HSL representation of the color.

```csharp
public static Color Darken(Color source, int target)
public static Color Lighten(Color source, int target)
```

### Spins and Complements

You can not only spin the color using a specified hue angle to add to the HSL angle from the color, but you can also get a complement by adding 180 to the hue angle in degrees.

```csharp
public static Color Spin(Color source, int target)
public static Color Complement(Color source)
```

## Other tools

In addition to the above features, you can also make use of the other tools below:

### Translate from X11 to ConsoleColor and back

`ConsoleColor` enumeration has an order of colors that is slightly different from the X11 colormap definitions for the first 16 colors. The following colors differ from each other:

| ConsoleColor              | X11                      |
| ------------------------- | ------------------------ |
| `ConsoleColor.DarkBlue`   | `ConsoleColors.DarkRed`  |
| `ConsoleColor.DarkCyan`   | `ConsoleColors.Olive`    |
| `ConsoleColor.DarkRed`    | `ConsoleColors.DarkBlue` |
| `ConsoleColor.DarkYellow` | `ConsoleColors.DarkCyan` |
| `ConsoleColor.Blue`       | `ConsoleColors.Red`      |
| `ConsoleColor.Cyan`       | `ConsoleColors.Yellow`   |
| `ConsoleColor.Red`        | `ConsoleColors.Blue`     |
| `ConsoleColor.Yellow`     | `ConsoleColors.Aqua`     |

In the `ColorTools` class, you can find two functions that translate between the two color mappings:

*   If you want to translate from `ConsoleColor` to X11's representation (`ConsoleColors`), use the `TranslateToX11ColorMap()` function, provided that its signature is:\


    ```csharp
    public static ConsoleColors TranslateToX11ColorMap(ConsoleColor color)
    ```
*   If you want to translate from `ConsoleColors` to .NET's representation (`ConsoleColor`), use the `TranslateToStandardColorMap()` function, provided that its signature is:\


    ```csharp
    public static ConsoleColor TranslateToStandardColorMap(ConsoleColors color)
    ```

### Correcting the `ConsoleColor` map for X11

Terminaux also provides a function that gets the correct color mapping for the specified color. The function is found under `ColorTools`, called `CorrectStandardColor()`. The signature is defined below:

```csharp
public static ConsoleColor CorrectStandardColor(ConsoleColor color)
```

### Resetting the colors and the console

Terminaux provides a console extension that allows you to perform a hard reset using the two VT sequences. When invoked, the terminal will perform two resets:

* Full reset (ESC sequence)
* Soft reset (CSI sequence)

After the reset is done, the screen will be cleared with all the colors reverted to their initial state. The signature is defined below:

```csharp
public static void ResetAll()
```

#### Resetting colors

You can reset all the colors once you're done writing text with color using the `ResetColors()` method. This resets the foreground and the background colors without resetting the whole console.

{% code title="ConsoleExtensions.cs" lineNumbers="true" %}
```csharp
public static void ResetColors()
```
{% endcode %}

If you want to reset only the foreground or the background color, you can use the following two functions:

{% code title="ConsoleExtensions.cs" lineNumbers="true" %}
```csharp
public static void ResetForeground()
public static void ResetBackground()
```
{% endcode %}

### Using settings

You can also generate colors with your specific settings, such as color transformation formula, by making a new instance of `ColorSettings` to store your own color settings.

However, by passing in your new instance of `ColorSettings`, you're affecting this color generation only once. To make it affect all generations, you'll have to change the global color settings, which can be found on `ColorTools.GlobalSettings`.

{% hint style="info" %}
Any change to a value in the global settings affects all color generations. Use your instance of `ColorSettings`, if possible.
{% endhint %}

You can also use your `ColorSettings` instance when parsing your color specifier.

### Color contrast

The color contrast tools provides you with various tools for color contrast and its manipulation functions.

#### Determining the "seeability"

{% code title="ColorContrast.cs" lineNumbers="true" %}
```csharp
public static bool IsSeeable(Color color)
public static bool IsSeeable(ColorType type, int colorLevel, int colorR, int colorG, int colorB, ColorSettings? settings = null)
```
{% endcode %}

You can determine the color "seeability" using this function. The color can be considered "seeable" if it meets the following conditions:

* The color type is either a 256- or a 16-color and not one of the following colors:
  * `ConsoleColors.Black`
  * `ConsoleColors.Grey0`
  * `ConsoleColors.Grey3`
  * `ConsoleColors.Grey7`
* The color type is a true color and all the RGB levels are above 30 out of 255.

#### Determining the color contrast with NTSC

You can get the color contrast (either black or white) using the `Y` (luma) component of the YIQ color model used by NTSC 1953 by calling the below function:

{% code title="ColorContrast.cs" lineNumbers="true" %}
```csharp
public static Color GetContrastColorNtsc(this Color color)
```
{% endcode %}

It returns either black or white, depending on the luma part of the color calculated using this formula:

$$Y = ((r * (0.299 * 1000)) + (g * (0.587 * 1000)) + (b * (0.114 * 1000))) / 1000$$

If the color luma is bigger than 128, it returns the black color for high contrast. Otherwise, white.

#### Determining the color contrast using half-white color number

You can also get the color contrast using the half-white color number method by consulting the below function:

{% code title="ColorContrast.cs" lineNumbers="true" %}
```csharp
public static Color GetContrastColorHalf(this Color color)
```
{% endcode %}

This function makes use of a formula that divides the number (`0xffffff`)  by 2, making a color number of half white. It takes a decimal version of the RGB color and compares it to that of the half-white number. If the RGB decimal is bigger than the half-white color, it gives you the black color for high contrast. Otherwise, white.

### Opacity

Whenever it comes to opacity, Terminaux attempts to simulate the transparency using your current background color of the console. However, you can override that by selecting a color that would be faded to when transparency is applied.

{% code title="ColorSettings.cs" lineNumbers="true" %}
```csharp
public int Opacity
{
    (...)
}

public Color OpacityColor
{
    (...)
}
```
{% endcode %}

When the opacity is set to 255, you're making a completely opaque color that holds just the color that you've chosen. However, when you choose any other opacity, such as 50% transparent (128), you're mixing 50% of your color with 50% of either the current console background color or your selected opacity blending color. If you choose 0%, you're essentially getting the opacity color that is opaque.

{% hint style="info" %}
Generally, it's recommended to set these two properties in a separate `ColorSettings` instance, unless you're making experiments. The color selector allows you to select the global transparency, but it may affect all the colors, even if closed.
{% endhint %}

{% hint style="warning" %}
This is not a real transparency, but a simulated one. That doesn't make text and elements rendered on top of the elements visible for the opacity that you choose. For example, you don't get to see text that is over-written by another text if you set the opacity.
{% endhint %}

### Gradients

Terminaux also supports creating a list of intermediate colors that would transition from either the source color or multiple colors to the target color. This is called gradients. This feature aims to make implementing the gradients easier than before.

Just specify the source color that you want to transition from, the target color that you want to transition to, and the number of steps needed, and call `ColorGradients`'s `GetGradients()`. You will need to assign a variable to hold an instance of `ColorGradients`.

```csharp
public static ColorGradients GetGradients(Color sourceColor, Color targetColor, int steps)
```

{% hint style="info" %}
You can enumerate through all the gradients either with the for-loop or the foreach-loop to get all their intermediate color. This ensures that it covers all the intermediate colors in exactly the number of steps that you've specified.
{% endhint %}

In addition to that, you can specify an array of target colors with their level ranging from 0.0 to 1.0, as well as specifying the end color. Use the below function to get started:

```csharp
public static ColorGradients GetGradients((double, Color)[] colors, Color ending, int steps)
```

There are types of gradients that are also implemented:

* Shades: It returns a list of colors that go from the selected color down to the black color. You can use the `GetShades()` function.
* Tints: It returns a list of colors that go from the selected color up to the white color. You can use the `GetTints()` function.
* Stage level: It returns a color that specifies the stage level of a specified number according to the stage positions. It uses the gradient function if you're using the smooth version. You can use the `StageLevelSmooth()` function.

### Color templates

Terminaux also provides a minimal theming system to allow you to categorize a color easily. The color templates allow you to use the category names to get a specified color, which you can then use it for several purposes, such as writing text with that color without having to provide the RGB specifier again.

Think of these templates as a group of shortcuts. The template management system allows you to set a template as a default one, which allows you to get a color using just a name without having to specify a template to use.

The color template management class can be found in the `TemplateTools` class, and an example code to demonstrate this feature can be found here:

{% code title="PrintTemplate.cs" lineNumbers="true" %}
```csharp
using Terminaux.Colors;
using Terminaux.Colors.Templates;
using Terminaux.Writer.ConsoleWriters;

namespace Terminaux.Console.Fixtures.Cases.Writer
{
    internal class PrintTemplate : IFixture
    {
        public void RunFixture()
        {
            string name = "template";

            // Default template
            TextWriterColor.WriteColor("[Default - {0}] Hello world!", true, TemplateTools.GetColor(PredefinedComponentType.Text), TemplateTools.Exists(name));

            // Custom template
            string templateJson =
                $$"""
                {
                    "Name": "{{name}}",
                    "Components": {
                        "Text": "#876543",
                        "Component": 168555
                    }
                }
                """;
            var template = TemplateTools.GetTemplateFromJson(templateJson);
            
            // Template registration
            TemplateTools.RegisterTemplate(template);
            TextWriterColor.WriteColor("[Before - {0}] Hello world!", true, TemplateTools.GetColor(PredefinedComponentType.Text), TemplateTools.Exists(name));
            
            // Template setting
            TemplateTools.SetDefaultTemplate(name);
            TextWriterColor.WriteColor("[After - Text] Hello world!", true, TemplateTools.GetColor(PredefinedComponentType.Text));
            TextWriterColor.WriteColor("[After - Component] Hello world!\n", true, TemplateTools.GetColor("Component"));
            
            // Colored component setting
            TemplateTools.SetColor("Component", new Color(86));
            TextWriterColor.WriteColor("[After - Component] Hello world!\n", true, TemplateTools.GetColor("Component"));
            TextWriterColor.Write(TemplateTools.GetTemplateToJson());
            
            // Resetting
            TemplateTools.ResetDefaultTemplate();
            TextWriterColor.WriteColor("\n[Reset - {0}] Hello world!", true, TemplateTools.GetColor(PredefinedComponentType.Text), TemplateTools.Exists(name));
            
            // Unregistering
            TemplateTools.UnregisterTemplate(name);
            TextWriterColor.WriteColor("[Reset - {0}] Hello world!\n", true, TemplateTools.GetColor(PredefinedComponentType.Text), TemplateTools.Exists(name));
            TextWriterColor.Write(TemplateTools.GetTemplateToJson());
        }
    }
}
```
{% endcode %}
