---
description: Nerd Fonts support coming to Terminaux!
icon: glasses
---

# Nerd Fonts

Terminaux also provides Nerd Fonts management for the text that you print to the console. This is to make applications look more understandable thanks to a large collection of Nerd Fonts glyphs that contain several different types of Nerd Fonts icons. Nerd Fonts in Terminaux is categorized into different types according to the glyph sets provided by the [NF wiki](https://github.com/ryanoasis/nerd-fonts/wiki/Glyph-Sets-and-Code-Points):

* [Custom](https://nerdfonts.com/cheat-sheet?q=nf-custom-)
* [Devicons](https://nerdfonts.com/cheat-sheet?q=nf-dev-)
* [Font Awesome](https://nerdfonts.com/cheat-sheet?q=nf-fa-)
* [Font Awesome Extension](https://nerdfonts.com/cheat-sheet?q=nf-fae-)
* [Material Design](https://nerdfonts.com/cheat-sheet?q=nf-md-)
* [Weather](https://nerdfonts.com/cheat-sheet?q=nf-weather-)
* [Octicons](https://nerdfonts.com/cheat-sheet?q=nf-oct-)
* [PowerLine Symbols](https://nerdfonts.com/cheat-sheet?q=nf-pl-)
* [PowerLine Extra Symbols](https://nerdfonts.com/cheat-sheet?q=nf-ple-)
* [IEC Power Symbols](https://nerdfonts.com/cheat-sheet?q=nf-iec-)
* [Font Logos](https://nerdfonts.com/cheat-sheet?q=nf-linux-)
* [Pomicons](https://nerdfonts.com/cheat-sheet?q=nf-pom-)
* [Codicons](https://nerdfonts.com/cheat-sheet?q=nf-code-)

In addition to these categories, there exists a category, called [`All`](https://nerdfonts.com/cheat-sheet?q=nf-), to represent basically the entire Nerd Fonts glyph list. You can use the cheat sheet to get the glyph names for your icon and either match them with the generated category class or with the symbol name that several functions, such as getting the Nerd Font character by category, take. These functions are found in the `Terminaux.Writer.CyclicWriters.Renderer.Tools` namespace as `NerdFontsTools`.

This class provides the following tools:

* `GetNerdFontChar()`
* `GetNerdFontCharNames()`

{% hint style="info" %}
If you want to use the Nerd Fonts feature on your console application, make sure that you use a compatible font that supports Nerd Fonts glyphs, such as a recent version of [Cascadia Code](https://github.com/microsoft/cascadia-code). Additionally, you can download a font off the [NF repository](https://github.com/ryanoasis/nerd-fonts).
{% endhint %}
