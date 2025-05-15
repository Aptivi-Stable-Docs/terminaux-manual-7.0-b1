---
description: Your screen in front of you.
icon: display
---

# Console Screen

Terminaux offers the console screen feature, which allows you to define a screen for your interactive console application. This guarantees you a dynamic terminal sequence generation that you can print to the console. Usage of the VT sequences can be found here:

{% content-ref url="vt-sequences.md" %}
[vt-sequences.md](vt-sequences.md)
{% endcontent-ref %}

## `Screen` Instance

You can get started by making a new instance of the `Screen` class and using it to add a new `ScreenPart` instance with its name to make a layer for your rendering sequences. This facilitates buffering the screens to the console.

The screen part instance allows you to add text and sequences in different ways:

* `AddText()`: Adds a simple and static text to the buffer
* `AddTextLine()`: Adds a simple and static text to the buffer with the extra new line
* `AddDynamicText()`: This is the key of the Screen feature. It allows you to define a function delegate that generates text dynamically.
* `Clear()`: Clears the whole buffer.
* `GetBuffer()`: Gets the resulting buffer.
* `RequireRefresh()`: Tells the screen system to require a refresh.
* `Visible`: Controls the visibility of the entire part

{% hint style="info" %}
`AddDynamicText()` is needed if you want to display anything that changes, including a box that changes when the console is resized.
{% endhint %}

## Screen Management

The screen management tools allow you to manipulate with the screen rendering, such as getting the current screen instance, rendering the current screen once, etc.

* `Render()` renders the current screen.
* `Render(Screen)` renders the specified screen.

{% hint style="info" %}
Starting from Terminaux 3.0, the screen feature automatically clears your screen when needed. In case this is not feasible, a configuration entry (global and local) will allow you to control this behavior.
{% endhint %}

However, for `Render()` to work, you need to add your screen instance to the list of tracked screens in the screen manager. This can be done by calling the `SetCurrent()` function on your screen instance.

When this is done, the screensaver manager and the console resize listener will refresh and redraw your screen, taking new console window dimensions to account. This reaction makes your interactive console applications that use screens responsive to the resize events.

{% hint style="warning" %}
Don't forget to remove your screen from the list of tracked screens once you're done using it. You can call `UnsetCurrent()` to make this happen.

If your application contains a main loop wrapped in a `try` and `catch` block, you must create a `finally` block (if not done) and call `UnsetCurrent()` on your screen instance. It may be necessary to move your screen instance declaration in your code outside the `try` and `catch` block.
{% endhint %}

### An example

The kernel interactive testing system allows you to try the demonstration of this feature out to show you the concept of what happens when you try to resize the console when the kernel tracks your screen instance.

The screen instance in question shows you two rulers:

* A horizontal ruler that shows you the width of the console window
* A vertical ruler that shows you the height of the console window

{% @github-files/github-code-block url="https://github.com/Aptivi/Terminaux/blob/main/Terminaux.Console/Fixtures/Cases/TestScreen.cs" %}

### More details

The screen feature contains the following classes for different purposes:

* `Screen`: A class that hosts all the screen parts and their buffers
* `ScreenPart`: A class that hosts all the buffer queues to formulate the final buffer for the screen manager to write to the console
* `ScreenTools`: A group of API functions that manipulate with the screen

#### Screen

The screen class hosts an array of screen parts that you can add, edit, or remove using the following functions:

* `AddBufferedPart()`
* `EditBufferedPart()`
* `RemoveBufferedPart()`

You are required to provide a name or a GUID for the specific screen part. This is to easily identify different screen parts, because if you're just looking for final buffer results, you might not be able to tell which part was for which.

You can use either the buffered part index number or the part name when using any of the following querying functions (in addition to the last two functions):

* `GetBufferedPart()`
* `CheckBufferedPart()`

You can also clear the entire buffered parts queue using the `RemoveBufferedParts()` function.

{% hint style="info" %}
By default, when the screen feature detects a resize, it'll re-render the current screen. It will, by default, reset the resize state, causing some programs to behave incorrectly. If you want Terminaux not to reset the resize state when the screen is resized, use the `ResetResize` property to set it to `false`.
{% endhint %}

In addition to that, you can make the screen cyclic by specifying the amount of milliseconds that describes the frequency of the cyclic screen. This is achieved using the `CycleFrequency` property. However, before the cyclic screen gets rendered in a loop, you must first set it as a default cyclic screen using the `SetCurrentCyclic()` function and render it using the `StartCyclicScreen()` function instead of the usual `Render()` function. When you're done rendering this screen, for example, exiting from a specific screen, use the `StopCyclicScreen()` function. Afterwards, you can use the `UnsetCurrentCyclic()` function to unset the current cyclic screen.

{% hint style="info" %}
You can't override the current cyclic screen until the thread that renders the chosen cyclic screen stops. You can check to see if this thread is running using the `CyclicScreenRunning()` function.
{% endhint %}

#### Screen Part

The screen part hosts a list of dynamic buffers to generate a working text sequence for the console plain writer to write it to the terminal to show you its contents. You can also call the screen parts as "layers" to more easily understand the motive behind these "layers."

In order to uniquely identify each screen part without any ambiguity, you can use the `Id` property that is populated each time you make a new screen part.

You can order them using the `Order` property when creating them. However, TermRead renders all the screen parts from the least important (the smallest `Order` values) to the most important (the largest `Order` values). This is useful for layering if you don't feel comfortable adding dynamic texts that represent layers.

```csharp
var orderedPart = new ScreenPart() { Order = 1 };
var importantPart = new ScreenPart() { Order = 100 };
```

You can use the following functions to add simple or dynamic text to the buffer queue:

* `AddText()`: Adds a simple text without the newline.
* `AddTextLine()`: Adds a simple text with the newline.
* `AddDynamicText()`: This is the key of all the resizable console TUIs. You need to provide a lambda or a function that hosts the entire rendering sequence.

In addition to these functions, you can use some of the console manipulation tools to add a string containing a necessary VT sequence to perform an operation. The following functions can be used:

* `LeftPosition()`
* `TopPosition()`
* `Position()`
* `ForegroundColor()`
* `BackgroundColor()`
* `ResetColor()`

If you want to clear the queue list without printing the buffers to the console, you can clear the list of dynamic buffers using the `Clear()` function. You can also control its visibility using the Visible property.

#### Screen Tools

The screen feature contains a set of tools that allow you to manipulate with a screen and its associated parts.

Setting a current screen requires you to provide `SetCurrent()` with a console screen instance once you're done making your own screen and filling it with necessary printing strings, such as an interactive TUI or a simple two rulers resizable application as provided in the example at the top of the page. Once the current screen is set, `CurrentScreen` returns your screen instance.

{% hint style="info" %}
`CurrentScreen` returns `null` upon calling it with no screen set. Therefore, it's advisable to check for this case when trying to access it if you don't set more than one screen as a default.
{% endhint %}

Once you set the current screen to render, you've made that screen the default screen. As a result, if your console has enabled Terminaux's console resize listener, once it detects that your console has resized itself, the screen will be re-drawn to accommodate with the new console size. To turn on this listener, follow the instructions highlighted in the below page:

{% content-ref url="console-resize-listener.md" %}
[console-resize-listener.md](console-resize-listener.md)
{% endcontent-ref %}

You can render your screen using:

* `Render()`: Renders your current screen. Throws if you didn't set your current screen before calling this version of the function.
* `Render(screen)`: Renders your screen instance to the console.

To unset the screen, you'll have to call `UnsetCurrent()` with the screen instance that you've set it as the default before. This removes the screen from the list of tracked screens.

{% hint style="info" %}
If you've called the above function with two or more screens, `CurrentScreen` doesn't return `null`, but returns the last screen found in the list.
{% endhint %}
