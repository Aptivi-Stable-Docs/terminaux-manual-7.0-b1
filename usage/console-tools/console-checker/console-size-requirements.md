---
description: Size requirements for the console can be customized
icon: badge-check
---

# Console Size Requirements

The console size requirement checking has been recently added to the latest version of Terminaux. This assists your application in determining your minimum console size requirements, with the default being the standard [80x24](https://softwareengineering.stackexchange.com/a/148765) console size for historical reasons.

For console applications which require a specific console size, such as Nitrocid KS which requires the above console size, you can call the `CheckConsoleSize()` function. You can also make it check for sizes other than 80x24, such as 120x30, by passing the width and the height to the same function.

```csharp
public static bool CheckConsoleSize(int minimumWidth = 80, int minimumHeight = 24)
```

This function is found in the `ConsoleChecker` public class so that you can access this function easily.

If you call this function, it first checks to see if there are edge cases regarding running such console application on terminal multiplexers.

* If you're running your console application on TMUX, it queries the TMUX settings to get how many status lines are there, and subtracts the required height by the number of status lines.
* If you're running your console application on GNU Screen, it subtracts the minimum height by one, since it doesn't use more than one line to print its status if enabled.
* If you're running your console application without a terminal multiplexer, it doesn't subtract the minimum height and stays as-is.

Once the terminal multiplexer check is done, it queries the current window width and the window height and compares them to the required width and height. If the requirement is not satisfied, the function returns false. Otherwise, it returns true as the requirements have been satisfied.

The `CheckConsoleSizePrompt()` function checks to see if the console size requirements have been satisfied. If the requirements aren't satisfied, the application tells you to resize your console window to have a better experience and to press `ENTER` when resized to the required size.
