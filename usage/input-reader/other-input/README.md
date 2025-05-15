---
description: Other input...
icon: pen
---

# Other Input

Terminaux not only provides the normal input reader with its custom bindings and its customizability, but you can also use its other input functions, such as informational boxes.

Terminaux currently provides the following input styles:

* Choice (one line, two lines, and modern)
* Info box (buttons, normal (modal and non-modal), input, progress, slider (with minimum, current, and maximum values), selection, and multiple choices)
* Selection (single choice and multiple choices)
* Editor (Text and hex editors and viewers)

{% hint style="info" %}
Modal infoboxes are informational boxes that are displayed on the terminal, waiting for user input. However, non-modal infoboxes are boxes that are just displayed for informational purposes, such as reporting a progress non-deterministically. Selection-based inputs can be searched using regular expressions compatible with the .NET syntax.
{% endhint %}

In addition to the above styles, you can also consult the following additional and specialized styles:

{% content-ref url="figlet-font-selector.md" %}
[figlet-font-selector.md](figlet-font-selector.md)
{% endcontent-ref %}

{% content-ref url="color-wheel.md" %}
[color-wheel.md](color-wheel.md)
{% endcontent-ref %}

{% content-ref url="editors-and-viewers.md" %}
[editors-and-viewers.md](editors-and-viewers.md)
{% endcontent-ref %}

To learn more about choice-based inputs, visit this page:

{% content-ref url="choice-based-inputs.md" %}
[choice-based-inputs.md](choice-based-inputs.md)
{% endcontent-ref %}

For keybindings, you can make use of the keybindings writer to convey the available keybindings to the end user by utilizing the `KeybindingsWriter` class, assuming that you've made an array of the `Keybinding` class.

{% hint style="info" %}
You can also customize the "help" keybinding, but be aware that it only supports keyboard binding.
{% endhint %}
