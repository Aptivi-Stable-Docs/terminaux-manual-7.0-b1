---
description: Mouse on your console!
icon: computer-mouse
---

# Pointer Events

## Pointer Events

Terminaux not only provides keyboard-based input, but it also provides mouse-based input. This adds flexibility to your already-flexible interactive console user interfaces by making them behave as if they are graphical user interface applications, but in the form of text.

{% hint style="success" %}
Terminaux is the **#1** console manipulation library that proudly features console mouse pointer support; something that competitors like `Spectre.Console` don't provide!
{% endhint %}

Do you want to enable it in your application? If so, you'll need to set the `MouseEnabled` property value to `true` that is found in the `Input` class. Once started, the application that waits for mouse events respond to every single mouse-based event based on the following conditions:

* If the user has moved their mouse and the movement events are acknowledged according to the `EnableMovementEvents` property, a `PointerEventContext` is made with `ButtonPress` being `Moved`.
* If the user has clicked anywhere on the console, a `PointerEventContext` is made with `ButtonPress` being `Clicked`. Also, the `Button` property indicates what mouse button was being pressed at the time. As soon as the user has let go of the same button, another context is made with `ButtonPress` being `Released`.
* If the user has clicked anywhere and moved the pointer without releasing any button, a `PointerEventContext` is made with `ButtonPress` being `Moved` and with `Dragging` being `True`. This enables applications to indicate that the user was dragging the mouse while clicking a button at the same time.
* If the user has used scrolling wheels in their mouse, a `PointerEventContext` is made with `ButtonPress` being `Scrolled` and `Button` indicating whether the user has scrolled up or down.

All pointer events include whether any of CTRL, ALT, and SHIFT keys were pressed at the time of the event or not. This is indicated in the `Modifiers` property. Such events also indicate the position of the mouse where the event occurred, which is a very important aspect to handling mouse click events in console applications. You can access this information using the `Coordinates` property that gives you two variables: `x` and `y`. The coordinates start from zero.

You can also access the button click tier information when the `PointerButtonPress` value is `Released`. Button click tier 1 means a single click, 2 means a double click, and so on. You can access this information using the `ClickTier` property.

{% hint style="info" %}
Here are some notes to consider before implementing pointer support to your Terminaux console application:

* Each platform handles console mouse pointer events differently. While Linux, macOS, and Android use [VT sequences](https://www.xfree86.org/current/ctlseqs.html#Mouse%20Tracking), Windows uses its own API to fetch console events as seen in the [`MOUSE_EVENT_RECORD`](https://learn.microsoft.com/en-us/windows/console/mouse-event-record-str) structure. We're trying to polish the relationship across Terminaux releases to make applications that use mouse event handling behave more consistently.
* On Android, you'll have to connect your external wireless mouse to your phone or your tablet in order to be able to click anywhere. Movement handling is not supported there.
* On Linux, macOS, and Android, there may be residual input when using the terminal reader in conjunction with the pointer listener. This is something to be considered as part of the polishing plan.
{% endhint %}

{% hint style="info" %}
All of the input methods that use the whole screen, such as selection and [your interactive TUI](https://github.com/Aptivi-Stable-Docs/terminaux-manual-6.x/blob/main/usage/console-tools/textual-ui/interactive-tui.md) apps, support mouse.
{% endhint %}

### Helper functions

Terminaux's mouse feature provides you with a wide assortment of helper functions and properties to enable your Terminaux application to listen to the mouse events. The following functions and properties are available:

* `Input.Listening`
* `Input.KeyboardInputAvailable`
* `Input.MouseInputAvailable`
* `Input.InputAvailable`
* `Input.PointerActive`
* `Input.InvertScrollYAxis`: Inverts the Y axis for vertical scrolling
* `Input.SwapLeftRightButtons`: Swaps the left/right mouse buttons
* `Input.DoubleClickTimeout`
* `Input.EnableMovementEvents`
* `Input.ReadPointer()`
* `Input.ReadPointerOrKey()`

At first, this may sound complicated, but it's rather easy to use. Inspired by the same concept of listening to console keyboard events using `ReadKey()` and `KeyAvailable`, you can use almost the same trick for mouse pointer events, albeit you'll always want to be able to handle both mouse and keyboard events.

The easiest way to listen to both the mouse and the keyboard events is this:

```csharp
// ...your code, usually screen rendering
SpinWait.SpinUntil(() => Input.InputAvailable);
if (Input.MouseInputAvailable)
{
    // Mouse input received.
    var mouse = TermReader.ReadPointer();
    switch (mouse.Button)
    {
        // Insert case statements here...
    }
}
else if (ConsoleWrapper.KeyAvailable && !Input.PointerActive)
{
    // Keyboard input received.
    var key = TermReader.ReadKey();
    switch (key.Key)
    {
        // Insert case statements here...
    }
}
```

The topmost `if` statement is the mouse event, and the bottommost `if` statement is the keyboard event. However, you may want to filter some events based on the button press state. For example, if you want to listen to left-clicks but don't want to listen to anything except when released, you can use this conditional:

<pre class="language-csharp"><code class="lang-csharp">switch (mouse.Button)
{
    case PointerButton.Left:
<strong>        if (mouse.ButtonPress != PointerButtonPress.Released)
</strong><strong>            break;
</strong>        // ...
        break;
    // ...
}
</code></pre>

{% hint style="warning" %}
You must not directly stop the listener right after a mouse click has been detected without listening to the `Released` event, or Windows's listener might still think that a mouse button has been pressed when it's not.
{% endhint %}

### Pointer tools

In addition to that, Terminaux provides the pointer tools that allow you to perform various operations to make building your console TUI applications easier. You can find the pointer tools in the `PointerTools` class, which are listed below:

* `PointerWithinPoint()`: This function returns `true` if the mouse pointer (click, movement, etc.) is found within a single point. For example, it returns `true` if your mouse pointer at `(22, 4)` matches the provided point position `(22, 4)`.
* `PointerWithinRange()`: This function returns `true` if the mouse pointer is found within a block range of the two points that form an invisible rectangle. For example, if you've specified `(22, 4)` and `(33, 6)` as two point ranges, and your mouse pointer has clicked on position `(25, 5)`, this function returns `true`.
