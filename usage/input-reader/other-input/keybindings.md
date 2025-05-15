---
description: Press any key!
icon: keyboard
---

# Keybindings

Individual keybindings are defined using the `Keybinding` class found in the `Terminaux.Writers.MiscWriters.Tools` namespace. They define what key or key combination, whether it's a mouse or a keyboard event, corresponds to what action that is described using text. You can define them using one of the following constructors:

* Console key without any modifiers
  * `string bindingName, ConsoleKey bindingKeyName`
* Console key with modifiers
  * `string bindingName, ConsoleKey bindingKeyName, ConsoleModifiers bindingKeyModifiers`
* Mouse pointer button without button press state and modifier
  * `string bindingName, PointerButton bindingPointerButton`
* Mouse pointer button with button press state, but without modifier
  * `string bindingName, PointerButton bindingPointerButton, PointerButtonPress bindingPointerButtonPress`
* Mouse pointer button with button press state and modifier
  * `string bindingName, PointerButton bindingPointerButton, PointerButtonPress bindingPointerButtonPress, PointerModifiers bindingButtonModifiers`

These keybindings have no action, as it's mostly for informational purposes, but you can also use it to define keybindings with the appropriate actions. However, a user might want to know what are the available keybindings in your interactive applications. We've implemented the `KeybindingsWriter` that contains the following functions:

* One-line keybindings list
  * `WriteKeybindings()`
  * `RenderKeybindings()`
* Keybindings list in an infobox
  * `ShowKeybindingInfoboxPlain()`
  * `ShowKeybindingInfobox()`
  * `ShowKeybindingInfoboxColor()`
  * `ShowKeybindingInfoboxColorBack()`
  * `RenderKeybindingHelpText()`

The `Render` function variant returns a string that you can either write to the terminal or add as part of the screen buffer if you're planning to write a complex application.
