---
description: We need to write to the console
icon: pen
---

# Console Writers

Terminaux provides a vast amount of console writers for different purposes, like the progress bar writer, writing console output in color, etc. Also, you can use their `Render()` functions found in basically every static writer (not those that are dynamic, such as wrapped writers).

{% hint style="info" %}
The `Render()` functions are made primarily for plain writing operations. You can use them with `TextWriterRaw` writers.
{% endhint %}

## Markups

Terminaux provides you with a simple BBCode-inspired markup syntax intended to style your own text without resorting to complicated string concatenations. It allows you to seamlessly apply formatting to different parts of text designed to be printed to the console. You can use the markup to convert your markup text to a raw text using the following methods:

* Creating a `Mark` instance with your text and calling `ParseMarkup()`.
* Calling `ParseMarkup()` from `MarkupTools`.

This is all found in the `Terminaux.Writer.CyclicWriters.Renderer.Markup` namespace. This maintains compatibility with [Spectre.Console markup syntax](https://spectreconsole.net/markup) to some degree. You can use the following syntaxes:

* Text formatting that you can use with this syntax: `[format]Hello![/]`
  * `bold`
  * `conceal`
  * `dim`
  * `invert`
  * `italic`
  * `rapidblink`
  * `slowblink`
  * `standout`
  * `strikethrough`
  * `underline`
* [Color specifiers](../../color-sequences/) that Terminaux can parse, such as `Red`, `#FF0000`, or `255;0;0`.
