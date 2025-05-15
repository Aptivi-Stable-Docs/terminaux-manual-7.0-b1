---
description: Other writers are here
icon: fill-drip
---

# Miscellaneous

## Eraser

This renderable allows you to erase either the entire screen or a part of the screen.

```csharp
var misc = new Eraser()
{
    Left = 2,
    Top = 2,
    InteriorWidth = 40,
    InteriorHeight = 10,
};
TextWriterRaw.WriteRaw(misc.Render());
```

For example, this is used to erase edges from a canvas without modifying the canvas instance itself:

```csharp
var canvas = new Canvas()
{
    Left = 2,
    Top = 2,
    Color = ConsoleColors.Green,
    InteriorWidth = 20,
    InteriorHeight = 20,
    Transparent = true,
    Pixels =
    [
        // Draw the top part of the "T" letter
        new(2, 2) { CellColor = ConsoleColors.Yellow },
        new(3, 2) { CellColor = ConsoleColors.Yellow },
        new(4, 2) { CellColor = ConsoleColors.Yellow },
        new(5, 2) { CellColor = ConsoleColors.Yellow },
        new(6, 2) { CellColor = ConsoleColors.Yellow },
        new(7, 2) { CellColor = ConsoleColors.Yellow },
        new(8, 2) { CellColor = ConsoleColors.Yellow },
        new(9, 2) { CellColor = ConsoleColors.Yellow },
        new(10, 2) { CellColor = ConsoleColors.Yellow },
        new(11, 2) { CellColor = ConsoleColors.Yellow },
        new(12, 2) { CellColor = ConsoleColors.Yellow },
        new(13, 2) { CellColor = ConsoleColors.Yellow },
        new(14, 2) { CellColor = ConsoleColors.Yellow },
        new(15, 2) { CellColor = ConsoleColors.Yellow },
        new(16, 2) { CellColor = ConsoleColors.Yellow },
        new(17, 2) { CellColor = ConsoleColors.Yellow },
        new(18, 2) { CellColor = ConsoleColors.Yellow },
        new(2, 3) { CellColor = ConsoleColors.Yellow },
        new(3, 3) { CellColor = ConsoleColors.Yellow },
        new(4, 3) { CellColor = ConsoleColors.Yellow },
        new(5, 3) { CellColor = ConsoleColors.Yellow },
        new(6, 3) { CellColor = ConsoleColors.Yellow },
        new(7, 3) { CellColor = ConsoleColors.Yellow },
        new(8, 3) { CellColor = ConsoleColors.Yellow },
        new(9, 3) { CellColor = ConsoleColors.Yellow },
        new(10, 3) { CellColor = ConsoleColors.Yellow },
        new(11, 3) { CellColor = ConsoleColors.Yellow },
        new(12, 3) { CellColor = ConsoleColors.Yellow },
        new(13, 3) { CellColor = ConsoleColors.Yellow },
        new(14, 3) { CellColor = ConsoleColors.Yellow },
        new(15, 3) { CellColor = ConsoleColors.Yellow },
        new(16, 3) { CellColor = ConsoleColors.Yellow },
        new(17, 3) { CellColor = ConsoleColors.Yellow },
        new(18, 3) { CellColor = ConsoleColors.Yellow },
        
        // Draw the line of the "T" letter
        new(9, 3) { CellColor = ConsoleColors.Yellow },
        new(9, 4) { CellColor = ConsoleColors.Yellow },
        new(9, 5) { CellColor = ConsoleColors.Yellow },
        new(9, 6) { CellColor = ConsoleColors.Yellow },
        new(9, 7) { CellColor = ConsoleColors.Yellow },
        new(9, 8) { CellColor = ConsoleColors.Yellow },
        new(9, 9) { CellColor = ConsoleColors.Yellow },
        new(9, 10) { CellColor = ConsoleColors.Yellow },
        new(9, 11) { CellColor = ConsoleColors.Yellow },
        new(9, 12) { CellColor = ConsoleColors.Yellow },
        new(9, 13) { CellColor = ConsoleColors.Yellow },
        new(9, 14) { CellColor = ConsoleColors.Yellow },
        new(9, 15) { CellColor = ConsoleColors.Yellow },
        new(9, 16) { CellColor = ConsoleColors.Yellow },
        new(9, 17) { CellColor = ConsoleColors.Yellow },
        new(9, 18) { CellColor = ConsoleColors.Yellow },
        new(9, 19) { CellColor = ConsoleColors.Yellow },
        new(10, 3) { CellColor = ConsoleColors.Yellow },
        new(10, 4) { CellColor = ConsoleColors.Yellow },
        new(10, 5) { CellColor = ConsoleColors.Yellow },
        new(10, 6) { CellColor = ConsoleColors.Yellow },
        new(10, 7) { CellColor = ConsoleColors.Yellow },
        new(10, 8) { CellColor = ConsoleColors.Yellow },
        new(10, 9) { CellColor = ConsoleColors.Yellow },
        new(10, 10) { CellColor = ConsoleColors.Yellow },
        new(10, 11) { CellColor = ConsoleColors.Yellow },
        new(10, 12) { CellColor = ConsoleColors.Yellow },
        new(10, 13) { CellColor = ConsoleColors.Yellow },
        new(10, 14) { CellColor = ConsoleColors.Yellow },
        new(10, 15) { CellColor = ConsoleColors.Yellow },
        new(10, 16) { CellColor = ConsoleColors.Yellow },
        new(10, 17) { CellColor = ConsoleColors.Yellow },
        new(10, 18) { CellColor = ConsoleColors.Yellow },
        new(10, 19) { CellColor = ConsoleColors.Yellow },
        new(11, 3) { CellColor = ConsoleColors.Yellow },
        new(11, 4) { CellColor = ConsoleColors.Yellow },
        new(11, 5) { CellColor = ConsoleColors.Yellow },
        new(11, 6) { CellColor = ConsoleColors.Yellow },
        new(11, 7) { CellColor = ConsoleColors.Yellow },
        new(11, 8) { CellColor = ConsoleColors.Yellow },
        new(11, 9) { CellColor = ConsoleColors.Yellow },
        new(11, 10) { CellColor = ConsoleColors.Yellow },
        new(11, 11) { CellColor = ConsoleColors.Yellow },
        new(11, 12) { CellColor = ConsoleColors.Yellow },
        new(11, 13) { CellColor = ConsoleColors.Yellow },
        new(11, 14) { CellColor = ConsoleColors.Yellow },
        new(11, 15) { CellColor = ConsoleColors.Yellow },
        new(11, 16) { CellColor = ConsoleColors.Yellow },
        new(11, 17) { CellColor = ConsoleColors.Yellow },
        new(11, 18) { CellColor = ConsoleColors.Yellow },
        new(11, 19) { CellColor = ConsoleColors.Yellow },
    ]
};
var eraser1 = new Eraser()
{
    Left = 2,
    Top = 2,
    InteriorWidth = 40,
    InteriorHeight = 1,
};
var eraser2 = new Eraser()
{
    Left = 2,
    Top = 3,
    InteriorWidth = 2,
    InteriorHeight = 19,
};
var eraser3 = new Eraser()
{
    Left = 2,
    Top = 21,
    InteriorWidth = 40,
    InteriorHeight = 1,
};
var eraser4 = new Eraser()
{
    Left = 38,
    Top = 3,
    InteriorWidth = 4,
    InteriorHeight = 19,
};
TextWriterRaw.WriteRaw(canvas.Render());
TextWriterRaw.WriteRaw(eraser1.Render());
TextWriterRaw.WriteRaw(eraser2.Render());
TextWriterRaw.WriteRaw(eraser3.Render());
TextWriterRaw.WriteRaw(eraser4.Render());
```

<figure><img src="../../../../.gitbook/assets/image (136).png" alt=""><figcaption></figcaption></figure>

## Keybindings

This renderable allows you to write a list of keybindings similar to that of old text-based applications to the terminal.

{% tabs %}
{% tab title="No overflow" %}
```csharp
var misc = new Keybindings()
{
    Width = ConsoleWrapper.WindowWidth,
    KeybindingList =
    [
        new("Binding 1", ConsoleKey.Enter),
        new("Binding 2", ConsoleKey.Escape),
        new("Binding 3", ConsoleKey.Tab),
    ]
};
TextWriterRaw.WriteRaw(RenderableTools.RenderRenderable(misc, new(0, ConsoleWrapper.WindowHeight - 1)));
```

<figure><img src="../../../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Overflow" %}
```csharp
var misc = new Keybindings()
{
    Width = ConsoleWrapper.WindowWidth,
    KeybindingList =
    [
        new("Binding 1", ConsoleKey.Enter),
        new("Binding 2", ConsoleKey.Escape),
        new("Binding 3", ConsoleKey.Tab),
        new("Binding 4", ConsoleKey.Spacebar),
        new("Binding 5", ConsoleKey.Home),
        new("Binding 6", ConsoleKey.End),
        new("Binding 7", ConsoleKey.DownArrow),
        new("Binding 8", ConsoleKey.UpArrow),
        new("Binding 9", ConsoleKey.Insert),
    ]
};
TextWriterRaw.WriteRaw(RenderableTools.RenderRenderable(misc, new(0, ConsoleWrapper.WindowHeight - 1)));
```

<figure><img src="../../../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Overflow + custom help key" %}
```csharp
var misc = new Keybindings()
{
    Width = ConsoleWrapper.WindowWidth,
    KeybindingList =
    [
        new("Binding 1", ConsoleKey.Enter),
        new("Binding 2", ConsoleKey.Escape),
        new("Binding 3", ConsoleKey.Tab),
        new("Binding 4", ConsoleKey.Spacebar),
        new("Binding 5", ConsoleKey.Home),
        new("Binding 6", ConsoleKey.End),
        new("Binding 7", ConsoleKey.DownArrow),
        new("Binding 8", ConsoleKey.UpArrow),
        new("Binding 9", ConsoleKey.Insert),
    ],
    HelpKeyInfo = new('H', ConsoleKey.H, false, false, false)
};
TextWriterRaw.WriteRaw(RenderableTools.RenderRenderable(misc, new(0, ConsoleWrapper.WindowHeight - 1)));
```

<figure><img src="../../../../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

## KeyShortcut

This renderable allows you to write a keybinding shortcut descriptor, which the `Keybindings` renderable internally uses, similar to that of old text-based applications to the terminal.

```csharp
var misc = new KeyShortcut()
{
    Shortcut = new("Binding 1", ConsoleKey.Enter),
    Width = ConsoleWrapper.WindowWidth,
};
TextWriterRaw.WriteRaw(misc.Render());
```

<figure><img src="../../../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

## Emoji

You can use this renderer to render an emoji within a rendered container.

```csharp
var rng = new Random();
var misc = new Emoji(Textify.Data.Unicode.EmojiEnum.SmilingFaceWithSmilingEyes);
TextWriterWhereColor.WriteWhere(misc.Render(), rng.Next(ConsoleWrapper.WindowWidth), rng.Next(ConsoleWrapper.WindowHeight));
```

<figure><img src="../../../../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

## Kaomoji

You can use this renderer to render a Kaomoji within a rendered container.

```csharp
var rng = new Random();
var misc = new Kaomoji(KaomojiCategory.Positive, KaomojiSubcategory.Joy, 3);
TextWriterWhereColor.WriteWhere(misc.Render(), rng.Next(ConsoleWrapper.WindowWidth), rng.Next(ConsoleWrapper.WindowHeight));
```

<figure><img src="../../../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

## NerdFonts

This renderable allows you to render a Nerd Fonts glyph to the console.

```csharp
var rng = new Random();
var misc = new NerdFonts(NerdFontsTypes.Codicons, "nf-md-microsoft_visual_studio_code");
var pos = new Coordinate(rng.Next(ConsoleWrapper.WindowWidth), rng.Next(ConsoleWrapper.WindowHeight));
ContainerTools.WriteRenderable(misc, pos);
```

<figure><img src="../../../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>
