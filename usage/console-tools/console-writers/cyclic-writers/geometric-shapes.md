---
description: Drawing geometric shapes to the console!
icon: triangle
---

# Geometric Shapes

Terminaux also provides a wide assortment of classes that allow you to render different geometric shapes to the console easily. You can select one of the following shapes to render to your console:

* Rectangle
* Square
* Triangle
* Trapezoid
* Parallelogram
* Circle
* Arc
* Ellipsis

They implement the `GraphicalCyclicWriter` and the `CyclicWriter` classes to allow you to iteratively render different geometric shapes from arrays of shapes that you can loop through to speed up the process and to allow you to implement your custom geometric shape.

{% hint style="info" %}
You can also store these shapes in a container and render them iteratively using the [`Container`](./) class. For line rendering, we recommend that you rely on the cyclic writer and its renderables.
{% endhint %}

To render a geometric shape, such as a rectangle, to the console, you must create a new instance of a shape class, providing the width and the height of the shape, as well as the position that tells Terminaux where to render the shape, whether to render the outline or the full shape (optional), and the selected color (optional).

{% hint style="info" %}
It's up to your shape class to have a constructor that doesn't necessarily require all the shape arguments as outlined above.
{% endhint %}

After creating a new instance, just call `Render()` on the shape instance.

{% code title="RenderRectangle.cs" lineNumbers="true" %}
```csharp
var rect = new Rectangle(7, 5, 4, 2, true, ConsoleColors.Red);
var rect2 = new Rectangle(7, 5, 21, 2, false, ConsoleColors.Aqua);
TextWriterRaw.WriteRaw(rect.Render());
TextWriterRaw.WriteRaw(rect2.Render());
```
{% endcode %}

<figure><img src="../../../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

You can render the following shapes directly to your console:

## Circle

The circle writer allows you to write a circle to the console. It also allows you to either draw just an outline or the whole filled circle.

{% tabs %}
{% tab title="Outline" %}
```csharp
var shape = new Circle(20, 2, 1);
TextWriterRaw.WriteRaw(shape.Render());
```

<figure><img src="../../../../.gitbook/assets/image (155).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Full" %}
```csharp
var shape = new Circle(20, 2, 1, true);
TextWriterRaw.WriteRaw(shape.Render());
```

<figure><img src="../../../../.gitbook/assets/image (156).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

## Arc

This writer allows you to write an arc directly to the console with some parameters, such as custom inner and outer radius, and angle ranges.

{% tabs %}
{% tab title="Partial Donut" %}
```csharp
var arc = new Arc(20, 4, 2, ConsoleColors.Red)
{
    InnerRadius = 6,
    OuterRadius = 9,
    AngleStart = 360,
    AngleEnd = 100,
};
TextWriterRaw.WriteRaw(arc.Render());
```

<figure><img src="../../../../.gitbook/assets/image (151).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Full Donut" %}
```csharp
var arc = new Arc(20, 4, 2, ConsoleColors.Red)
{
    InnerRadius = 6,
    OuterRadius = 9,
    AngleStart = 360,
    AngleEnd = 100,
};
var arc2 = new Arc(20, 4, 2, ConsoleColors.Lime)
{
    InnerRadius = 6,
    OuterRadius = 9,
    AngleStart = 150,
    AngleEnd = 300,
};
var arc3 = new Arc(20, 4, 2, ConsoleColors.Blue)
{
    InnerRadius = 6,
    OuterRadius = 9,
    AngleStart = 100,
    AngleEnd = 150,
};
TextWriterRaw.WriteRaw(arc.Render());
TextWriterRaw.WriteRaw(arc2.Render());
TextWriterRaw.WriteRaw(arc3.Render());
```

<figure><img src="../../../../.gitbook/assets/image (152).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Partial Pie" %}
```csharp
var arc = new Arc(20, 4, 2, ConsoleColors.Red)
{
    InnerRadius = 0,
    OuterRadius = 9,
    AngleStart = 170,
    AngleEnd = 120,
};
TextWriterRaw.WriteRaw(arc.Render());
```

<figure><img src="../../../../.gitbook/assets/image (153).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Full Pie" %}
```csharp
var arc = new Arc(20, 4, 2, ConsoleColors.Red)
{
    InnerRadius = 0,
    OuterRadius = 9,
    AngleStart = 170,
    AngleEnd = 120,
};
var arc2 = new Arc(20, 4, 2, ConsoleColors.Aqua)
{
    InnerRadius = 0,
    OuterRadius = 9,
    AngleStart = 120,
    AngleEnd = 170,
};
TextWriterRaw.WriteRaw(arc.Render());
TextWriterRaw.WriteRaw(arc2.Render());
```

<figure><img src="../../../../.gitbook/assets/image (154).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

## Ellipsis

This writer allows you to write an ellipsis directly to the console. It also allows you to either draw just an outline or the whole filled ellipsis.

{% tabs %}
{% tab title="Outline" %}
```csharp
var shape = new Ellipsis(20, 15, 2, 1);
TextWriterRaw.WriteRaw(shape.Render());
```

<figure><img src="../../../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Full" %}
```csharp
var shape = new Ellipsis(20, 15, 2, 1, true);
TextWriterRaw.WriteRaw(shape.Render());
```

<figure><img src="../../../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

## Parallelogram

This writer allows you to write a parallelogram to the console directly. You can specify whether to draw just the outline or the whole shape.

{% tabs %}
{% tab title="Outline" %}
```csharp
var shape = new Parallelogram(20, 10, 2, 1);
TextWriterRaw.WriteRaw(shape.Render());
```

<figure><img src="../../../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Full" %}
```csharp
var shape = new Parallelogram(20, 10, 2, 1, true);
TextWriterRaw.WriteRaw(shape.Render());
```

<figure><img src="../../../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

## Rectangle

This writer allows you to write a rectangle to the console directly. You can specify whether to print the whole shape or just the edges.

{% tabs %}
{% tab title="Outline" %}
```csharp
var shape = new Rectangle(20, 10, 2, 1);
TextWriterRaw.WriteRaw(shape.Render());
```

<figure><img src="../../../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Full" %}
```csharp
var shape = new Rectangle(20, 10, 2, 1, true);
TextWriterRaw.WriteRaw(shape.Render());
```

<figure><img src="../../../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

## Square

This shape basically renders a rectangle, but with just the height specified. In the console, the width is multiplied by two due to the space widths taking up only one cell. It basically renders a square.

{% tabs %}
{% tab title="Outline" %}
```csharp
var shape = new Square(20, 2, 1);
TextWriterRaw.WriteRaw(shape.Render());
```

<figure><img src="../../../../.gitbook/assets/image (111).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Full" %}
```csharp
var shape = new Square(20, 2, 1, true);
TextWriterRaw.WriteRaw(shape.Render());
```

<figure><img src="../../../../.gitbook/assets/image (112).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

## Trapezoid

This renders a trapezoid using a specified height, a top edge width, and a bottom edge width. You can also make it either render just the outline or as a full shape.

{% tabs %}
{% tab title="Outline" %}
```csharp
var shape = new Trapezoid(10, 30, 20, 2, 1);
TextWriterRaw.WriteRaw(shape.Render());
```

<figure><img src="../../../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Full" %}
```csharp
var shape = new Trapezoid(10, 30, 20, 2, 1, true);
TextWriterRaw.WriteRaw(shape.Render());
```

<figure><img src="../../../../.gitbook/assets/image (137).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

## Triangle

This renders either an equilateral triangle or an isosceles triangle to the console.

{% tabs %}
{% tab title="Outline" %}
```csharp
var shape = new Triangle(30, 20, 2, 1);
TextWriterRaw.WriteRaw(shape.Render());
```

<figure><img src="../../../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Final" %}
```csharp
var shape = new Triangle(30, 20, 2, 1, true);
TextWriterRaw.WriteRaw(shape.Render());
```

<figure><img src="../../../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

## Line

This renders either a rough line or a smooth line, and it can either be half-width or full-width.

{% tabs %}
{% tab title="Rough line" %}
```csharp
var line = new Line()
{
    StartPos = new(2, 2),
    EndPos = new(10, 5)
};
TextWriterRaw.WriteRaw(line.Render());
```

<figure><img src="../../../../.gitbook/assets/image (148).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Smooth line" %}
```csharp
var line = new Line()
{
    StartPos = new(2, 2),
    EndPos = new(10, 5),
    AntiAlias = true,
};
TextWriterRaw.WriteRaw(line.Render());
```

<figure><img src="../../../../.gitbook/assets/image (147).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}
