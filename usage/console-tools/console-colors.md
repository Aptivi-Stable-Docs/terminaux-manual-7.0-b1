---
description: Console color tools here!
icon: palette
---

# Console Colors

In addition to all of the Terminaux's features, we also provide you with a rich class for console color tools. Here are the supported properties and functions that you can use in your console applications:

* Setting the console color
* Setting the console color dryly
* ...and more

For more color functions and to get started making the color sequences, you can consult the below page:

{% content-ref url="../color-sequences/" %}
[color-sequences](../color-sequences/)
{% endcontent-ref %}

## Current colors

The console tools class provides you with two properties that allow you to get the current foreground and the background color.

{% code title="ColorTools.cs" lineNumbers="true" %}
```csharp
public static Color CurrentForegroundColor
public static Color CurrentBackgroundColor
```
{% endcode %}

## Color setting

The console tools class provides you with two functions that set the console foreground and background colors both dryly and permanently.

{% code title="ColorTools.cs" lineNumbers="true" %}
```csharp
public static void SetConsoleColor(Color ColorSequence, bool Background = false, bool ForceSet = false, bool canSetBackground = true)
public static void SetConsoleColorDry(Color ColorSequence, bool Background = false, bool ForceSet = false, bool canSetBackground = true)
```
{% endcode %}

The first function sets either the console's foreground color or the console's background color permanently. The changes will be done and you can verify this using either `CurrentForegroundColor` or `CurrentBackgroundColor`.

The second function, however, only runs dryly and doesn't set any of the abovementioned properties. This allows you to temporarily set the background or the foreground color.

{% hint style="info" %}
If you want to dryly set the console color, you must either use the plain writers, or use the `Color` instances to apply them to all the `Color`-related parameters.

Additionally, if you wish to dryly set the colors on plain writers, you can use the `RenderSetConsoleColor()` function, but you'll have to append one of the following:

* `RenderResetColors()`
* `RenderResetForeground()`
* `RenderResetBackground()`

If you want to go back to the current color set by Terminaux, use one of the following:

* `RenderRevertColors()`
* `RenderRevertForeground()`
* `RenderRevertBackground()`

if you don't want the color to leak. As for the background colors, consider these:

* Currently, `AllowBackground` is set to `false`, which means that background colors are disabled, unless forced. To enable background colors globally, you must enable it.
{% endhint %}

## Background loading

The console color tools class also provides you with background loading functions that allow you to quickly clear the console with the selected background color.

{% code title="ColorTools.cs" lineNumbers="true" %}
```csharp
public static void LoadBack()
public static void LoadBack(Color ColorSequence, bool Force = false)
public static void LoadBackDry()
public static void LoadBackDry(Color ColorSequence, bool Force = false)
```
{% endcode %}

The non-dry `LoadBack()` functions allow you to load the background color and permanently set the console background color to either the already-set current background color or to your specified background color. However, the dry version allows you to load the background color temporarily.

{% hint style="info" %}
If you want to dryly set the background color, you must either use the plain writers, or use the background `Color` instances to apply them to all the background color-related parameters.
{% endhint %}

## Sequence Initialization

If you have a Windows system, you can call a function that allows you to initialize the VT sequences. This function in the `ConsoleExtensions` class is called `InitializeSequences()`.

{% hint style="info" %}
If you have already set the VT sequence processing using a registry key found in `HKEY_CURRENT_USER\Console\VirtualTerminalLevel`, this function does nothing.
{% endhint %}

## Resetting the colors

You can also reset the colors either fully or selectively (foreground or background) by calling one of the following functions:

* `ResetColors()`: Resets both the foreground and the background colors.
* `ResetForeground()`: Resets the foreground color.
* `ResetBackground()`: Resets the background color.

## Reverting the colors

Reverting the colors to their currently set colors monitored by Terminaux can be done easily by calling one of the following functions:

* `RevertColors()`: Reverts both the foreground and the background colors.
* `RevertForeground()`: Reverts the foreground color.
* `RevertBackground()`: Reverts the background color.
