---
description: How do you use it?
icon: lightbulb-on
---

# Preface

To use this library, you first need to know exactly why do you need to install Terminaux into your console application. If your application is intended to be an interactive one, or if your application shows graphics (text, info box, ...), then Terminaux is the right library for you.

Terminaux provides several terminal actions, like reading an input (was on TermRead), getting color information (was on ColorSeq), and using VT sequences and filtering them (was on VT.NET).

### Reading an input

To get started reading input, follow the below page to get started:

{% content-ref url="input-reader/" %}
[input-reader](input-reader/)
{% endcontent-ref %}

### Other console tools

For other console tools that Terminaux provides, you can access the below page:

{% content-ref url="console-tools/" %}
[console-tools](console-tools/)
{% endcontent-ref %}

## Trying Terminaux out

Each version of Terminaux contains their own release page that allows you to download a demo zip file from GitHub. This allows you access to the interactive demo, which allows you to try almost all Terminaux features out, including the interactive TUI, the terminal reader, and so on.

This demo can be used as a test to verify that your console works as expected and that it supports all the features that Terminaux requires.

{% hint style="info" %}
Any call to any function that require VT sequences and advanced console features, such as fancy writers and mouse pointer events, will cause Terminaux to check your console.
{% endhint %}
