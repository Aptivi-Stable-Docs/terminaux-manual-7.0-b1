---
description: Describe something using images!
icon: crystal-ball
---

# Icons

As of Terminaux 4.2.0, it provides a method to render icons. They represent symbols that describe something, such as computer peripherals and books, to describe a thing or two using just the icons. The `IconsManager` class provides you with icon management tools that allow you to render the icons and get their names.

{% hint style="warning" %}
They're not suitable for icons inside the text, because it uses pictures. If you still want to use them, use the text-based emojis instead.
{% endhint %}

In order to be able to use the icons in your interactive applications, you can get the value from the `RenderIcon()` function, specifying the icon name, the width and the height of your icon, and the position of where do you want your icon to be rendered. This value can then be printed using the conventional `TextWriterRaw.WriteRaw()` function.

You can choose one of the two following properties:

* Quality: Normal quality (72x72), high quality (618x618), or scalable quality (SVG)
* Color: Colored or Black

The icon selector allows you to interactively select an icon while showing it to you at the same time to review your icon choice. This can be accessed in the `IconsSelector` class.
