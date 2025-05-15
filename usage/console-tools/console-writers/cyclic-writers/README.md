---
description: Such writers render repeatedly with or without some movement
icon: arrow-rotate-right
---

# Cyclic Writers

Cyclic writers are dynamic writers that can be rendered individually by making a new class instance of a renderable class that implements the base cyclic writer class, `CyclicWriter`, and one of the typed cyclic writer classes that you can implement in your renderable class. Such writers can either be animated or static, and can be rendered either by calling their individual `Render()` function one by one or by putting renderable classes to a container and calling that container's `WriteContainer()` function from the `ContainerTools` class.

In cyclic writers, the implementation usually implements the base cyclic writer class and one of the following classes:

* `GraphicalCyclicWriter`: This cyclic writer utilizes positioning and supports widths and heights for graphical terminal applications.
* `SimpleCyclicWriter`: This cyclic writer simply writes the rendered output to the console and is suitable for simple and scrolling terminal applications.

{% hint style="info" %}
Most of the renderables also support colors, in which you can set with `UseColors` and their appropriate properties.
{% endhint %}

For margins, in all cyclic writers that derive from the `GraphicalCyclicWriter` class, you can use the following properties:

* `Padding`: Object padding to create blank space around the selected areas in cells.
* `Margin`: Object margin to reduce the width and the height based on the margin values.

All graphical cyclic writers use the `SetMargin` property to set the appropriate position and size in accordance to the two above property values.

The following built-in cyclic writers are available:

* Shapes
  * `Circle`
  * `Arc`
  * `Ellipsis`
  * `Parallelogram`
  * `Rectangle`
  * `Square`
  * `Trapezoid`
  * `Triangle`
  * `Line`
* Charts
  * `BreakdownChart`
  * `BarChart`
  * `StickChart`
  * `StemLeafChart`
  * `LineChart`
  * `LinesChart`
  * `PieChart`
  * `WinsLosses`
* Text
  * `AlignedFigletText`
  * `AlignedText`
  * `AnimatedText`
  * `BoundedText`
  * `FigletText`
  * `PowerLine`
  * `TextMarquee`
  * `Decoration`
  * `SyntaxText`
  * `TextPath`
* Artistic
  * `Border`
  * `Box`
  * `BoxFrame`
  * `Canvas`
  * `AnimatedCanvas`
* Misc
  * `ProgressBar`
  * `ProgressBarNoText`
  * `SimpleProgress`
  * `Slider`
  * `Spinner`
    * Built-in spinners are available in the `BuiltinSpinners` class.
  * `Table` and `Calendars`
  * `Eraser`
  * `Keybindings`
  * `KeyShortcut`
  * `ListEntry`
  * `Listing`
  * `Emoji`
  * `Kaomoji`
  * `NerdFonts`
  * `Selection`

You can define a container by creating a new instance of the `Container` class and adding some of the renderables that can be identified by their name. You can also set their positions using the `SetRenderablePosition()` function, and you can set their sizes using the `SetRenderableSize()` function. If you don't want to use a container, you can use the `RenderRenderable()` function or the `WriteRenderable()` function from the `RendererTools` class to render a specific renderable in a specific position and to write the result to the console, respectively.

{% hint style="info" %}
Some of the renderables may override the position variable for a renderable and may use the values from the renderables' properties.
{% endhint %}

In addition to that, you can manipulate with a renderable using the following functions:

* `IsRegistered()`: Checks to see if a renderable with this ID is registered or not.
* `RemoveRenderable()`: Removes a renderable with this ID.
* `GetRenderable()`: Gets a renderable instance from this ID.
* `GetRenderablePosition()`: Gets a renderable instance position from this ID.
* `GetRenderableSize()`: Gets a renderable instance size from this ID.
* `GetRenderableNames()`: Gets an array of renderable IDs.

In order to explore cyclic writers, please use the left sidebar.
