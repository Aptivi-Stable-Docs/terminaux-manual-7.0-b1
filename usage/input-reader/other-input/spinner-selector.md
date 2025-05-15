---
description: Spin, spin, spin!
icon: arrows-spin
---

# Spinner Selector

<figure><img src="../../../.gitbook/assets/image (59).png" alt=""><figcaption></figcaption></figure>

Terminaux provides a selector that allows you to choose a spinner in an interactive way with live previews, powered by the [textual UI](../../console-tools/textual-ui/) feature. This feature can be found in the `SpinnerSelector` class found in the `Terminaux.Inputs.Styles` namespace, and you can run it with the following functions:

* `PromptForSpinner()`
* `PromptForSpinner(string spinner)`

The first overload automatically falls back to the `Dots` built-in spinner, while the second overload allows you to specify the name of a built-in spinner. You can get a list of built-in spinner names defined in the `BuiltinSpinners` class.

{% hint style="warning" %}
You can't use custom spinners, as they are not considered to be built-in.
{% endhint %}

Once the user end submitted their selection, the two functions will return a `Spinner` instance obtained from the built-in spinner instance list, which can be rendered immediately using a function described [here](../../console-tools/console-writers/cyclic-writers/).

## Controls

The below keybindings can be used to control the selector:

<table><thead><tr><th width="285">Keybinding</th><th>Action</th></tr></thead><tbody><tr><td><code>Left arrow</code> (wheel up)</td><td>Previous spinner</td></tr><tr><td><code>Right arrow</code> (wheel down)</td><td>Next spinner</td></tr><tr><td><code>Enter</code></td><td>Submits your selection</td></tr><tr><td><code>Escape</code></td><td>Cancels your selection and returns the initial spinner</td></tr><tr><td><code>H</code></td><td>Help page</td></tr><tr><td><code>S</code></td><td>Select a spinner from the list</td></tr><tr><td><code>Shift + S</code></td><td>Select a spinner by writing its name</td></tr></tbody></table>
