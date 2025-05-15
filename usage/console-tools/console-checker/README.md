---
description: Checking to see if you're working on the right console...
icon: badge-check
---

# Console Checker

Sometimes, your console application might need some of the additional features, such as VT color sequences, that might not be available to all of the terminal emulators installed on your system. In this case, Terminaux provides you with a wide assortment of console checkers to ease the process of checking the features.

## Checking

There are various checkers you'll be able to use with Terminaux:

* Dumb console checker
* General console checker
* 256 color support checker
* Size requirement checker

For checking the size requirement, you'll need to consult the below page to get started:

{% content-ref url="console-size-requirements.md" %}
[console-size-requirements.md](console-size-requirements.md)
{% endcontent-ref %}

In case of unit tests failing because your application contains calls to parts of Terminaux that require this check to run, you can add your test assembly to the check whitelist to bypass checking only for your assembly.

* `AddToCheckWhitelist()`: Adds your assembly to the check whitelist.
* `RemoveFromCheckWhitelist()`: Removes your assembly from the check whitelist.

{% hint style="info" %}
The easiest way to add your own test assembly to the whitelist is by calling the `Assembly.GetEntryAssembly()` function within your one-time unit test initialization code.

{% code lineNumbers="true" %}
```csharp
var asm = Assembly.GetEntryAssembly();
ConsoleChecker.AddToCheckWhitelist(asm);
```
{% endcode %}
{% endhint %}

### Dumb console

Dumb consoles, in general, don't understand the concept of colors, positioning, erasing, and features other than writing to the console. However, some of them may be provided with basic color support and various other features that are simple.

The dumb console checker checks to see if we can call the `CursorLeft` property inside the exception handler. Usually, this property throws an `IOException` if it can't query the terminal for the cursor left position, but this happens when the console doesn't understand the concept of positioning, which happens on dumb consoles.

If the cursor position is queried, the checker queries the terminal type to check to see if it's one of `dumb` or `unknown`. These two terminal types are assumed to be dumb.

If checks pass, the console is not considered as dumb. This means that Terminaux is able to use the color features and all the other features.

### General checker

The general console checker throws an exception if the checker found the terminal to be one of the "dumb" consoles. Then, it queries both the console blacklist and the greylist for both the emulator and the type.

If the blacklist checker raised some of the red flags by matching the console type or emulator, the general checker, `CheckConsole()`, throws an exception. If the greylist checker raised some of the red flags, the application shows a warning on the screen.

#### Registering console filters

The terminal type and emulator blacklist and greylist checkers contain adding and removing console regular expression patterns to/from the blacklist or the greylist. You can use them by calling any function in the `ConsoleFilter` class.

The console filter severities (`ConsoleFilterSeverity`) are available:

* `Blacklist`
* `Graylist`

The console filter types (`ConsoleFilterType`) are available:

* `Type`
* `Emulator`

Each of these checkers contain a function for adding the query (`AddToFilter`), removing the query (`RemoveFromFilter`), and checking the current console type or emulator (`IsConsoleFiltered`). These are the essential functions.

{% hint style="info" %}
The default terminal type blacklist contains `dumb` and `unknown` terminal types.
{% endhint %}

### 256-color support checker

This checker is a very simple checker, because it only queries the terminal type for a string containing `-256col`. Any terminal type that doesn't have this string is assumed to be not supporting 256-color feature, but that doesn't necessarily mean that the console doesn't support this feature, depending on your console application. Use `IsConsole256Colors()` to use this checker.

### ConHost checker

This checker is a very simple checker that checks to see if your Terminaux application is being run in a Windows console that uses ConHost as the console rendering backend. Note that it always returns false on non-Windows systems. Use `IsConHost()` to use this checker.
