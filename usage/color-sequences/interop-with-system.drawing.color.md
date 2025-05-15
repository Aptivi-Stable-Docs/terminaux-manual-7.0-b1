---
description: Terminaux's Color meets System.Drawing's Color!
icon: paintbrush
---

# Interop with System.Drawing.Color

Since Terminaux 2.5.0, we've introduced a new way to interact with `System.Drawing`'s [`Color`](https://learn.microsoft.com/en-us/dotnet/api/system.drawing.color?view=net-8.0) struct! You can find all the tools in the `SystemColorConverter` class under `Terminaux.Colors.Interop`. The `Color` struct from `System.Drawing` represents the four color components:

* Alpha (A): Color opaqueness level. 0% means 100% transparency.
* Red (R): Red color level.
* Green (G): Green color level.
* Blue (B): Blue color level.

This class provides the following functions:

{% code title="SystemColorConverter.cs" lineNumbers="true" %}
```csharp
public static OurColor FromDrawingColor(DrawingColor drawingColor)
public static DrawingColor ToDrawingColor(OurColor ourColor)
```
{% endcode %}

Depending on your use-case, the two functions are appropriate when:

* you're looking to make an instance of Terminaux's `Color` from `System.Drawing.Color` instance. In this situation, you'll have to use the `FromDrawingColor()` function.
* you're looking to make an instance of System.Drawing's Color from Terminaux's Color instance. In this situation, you'll have to use the `ToDrawingColor()` function.

This is useful if you're interacting with applications that use `System.Drawing`'s `Color`.
