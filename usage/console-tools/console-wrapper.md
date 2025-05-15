---
description: How do I wrap the console?
icon: plug
---

# Console Wrapper

Terminaux provides you with a powerful console wrapper that allows you to customize how the console behaves in your .NET console applications that make use of this wrapper and/or built-in Terminaux features. This wrapper is easy to use, amidst the recent structural improvements to the console wrapper functionality compared to Terminaux 1.x.

One big advantage of using this console wrapper is that you're able to get the console cursor visibility, but only if you're using Terminaux's cursor visibility wrapper. This works on Windows, macOS, Android, and Linux.

To use this console wrapper, just replace all the calls to `Console` with our replacement `ConsoleWrapper` to take advantage of Terminaux's console wrapping feature. However, you can use this wrapper only for the following actions:

* `CursorLeft` (get and set)
* `CursorTop` (get and set)
* `WindowWidth` (get and set)
* `WindowHeight` (get and set)
* `BufferWidth` (get and set)
* `BufferHeight` (get and set)
* `CursorVisible` (get and set)
* `KeyAvailable` (get)
* `TreatCtrlCAsInput` (get and set)
* `Clear()` (with and without background)
* `GetCursorPosition()`
* `SetCursorPosition()`
* `SetWindowDimensions()`
* `SetBufferDimensions()`
* `Beep()`
* `ReadKey()`
* `Write()`
* `WriteLine()`
* `Error.Write()`
* `Error.WriteLine()`

{% hint style="info" %}
**Note that properties and functions that work only for Windows, such as `MoveBufferArea`, and have no good alternative alternatives for macOS and Linux are not going to be wrapped.**
{% endhint %}

## Setting the Wrappers

You can customize the console wrappers so that applications that call the Terminaux console wrapper can make use of your own custom wrapper function by setting the action properties found in `ConsoleWrapperTools`. You can make changes to the following wrappers (all prefixed by the `Action` word in all the properties):

* `IsDumb`
* `CursorLeft`
* `SetCursorLeft`
* `CursorTop`
* `SetCursorTop`
* `WindowWidth`
* `SetWindowWidth`
* `WindowHeight`
* `SetWindowHeight`
* `BufferWidth`
* `SetBufferWidth`
* `BufferHeight`
* `SetBufferHeight`
* `CursorVisible`
* `GetCursorVisible`
* `TreatCtrlCAsInput`
* `KeyAvailable`
* `Clear()` (without background)
* `ClearLoadBack()` (with background)
* `GetCursorPosition()`
* `SetCursorPosition()`
* `SetWindowDimensions()`
* `SetBufferDimensions()`
* `Beep()`
* `BeepSeq()`
* `ReadKey()`
* `WriteChar()`
* `WriteString()`
* `WriteParameterized()`
* `WriteLine()`
* `WriteLineStirng()`
* `WriteLineParameterized()`
* `WriteError()`
* `WriteErrorLine()`

{% hint style="info" %}
In order for your console wrapper to be usable, all your custom wrapper functions must be fast, as interactive TUIs rely on performance.
{% endhint %}
