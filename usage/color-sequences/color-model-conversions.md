---
description: From RGB to CMYK to HSL to...
icon: palette
---

# Color Model Conversions

Terminaux provides several color models that you can convert from/to using the `Color` instance. You can use the RGB property from it to be able to start converting your color to another color model using the appropriate conversion tools for your target unit. The appropriate conversion tools are found in the `ConversionTools` class.

This class is made to facilitate the color model conversion, such as from RGB to CMY, from CMY to HSL, from HSL to RYB, and so on. This means that it's easier than before.

Color models also contain their normalized properties. Some of these models have the `Normalized` (floating point numbers) variants of the components, while some others have the `Whole` (integers) variants.

To convert your source color model, you first need to select the conversion tools according to the color model that you want to convert the source model to (a.k.a. the target color model). For example, if you want to convert RGB to HSV, you can use `ConversionTools` and call the function, `ToHsv(RedGreenBlue)`, to run the conversion. You can also specify a type of color model in both the generic and the non-generic versions of the functions.

Here's how the conversion is run:

{% code title="Somewhere in your program..." lineNumbers="true" %}
```csharp
var color = new Color(128, 255, 0);
var hsv = ConversionTools.ToHsv(color.RGB);
```
{% endcode %}

The program above converts the color that has the RGB value of `128, 255, 0` to its representation in Hue, Saturation, and Value color model. You can then consult the target's properties to see the resulting values, such as the hue, saturation, and the value variables in both the fractional form `[0.00, 1.00]` and the complete form `[0, 100]`.
