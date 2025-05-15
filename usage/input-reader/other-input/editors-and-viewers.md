---
description: Edit or view text or hex
icon: book-open
---

# Editors and Viewers

Terminaux provides a way to edit or view a hexadecimal representation of bytes or lines of text in an interactive way without any hassle. The following classes are available for you to use:

* `HexEditInteractive`
  * Represents an interactive hex editor
* `HexViewInteractive`
  * Represents an interactive hex viewer
* `TextEditInteractive`
  * Represents an interactive text editor
* `TextViewInteractive`
  * Represents an interactive text viewer

## Hex editor and viewer

<figure><img src="../../../.gitbook/assets/image (96).png" alt=""><figcaption></figcaption></figure>

The interactive hex editor allows you to edit either a file or a byte array byte by byte, while giving you basic editing abilities, such as replacing all occurrences of a byte value with another byte value, finding a byte value or a group of it, and so on. This is all done with the help of the [screen feature](../../console-tools/textual-ui/console-screen.md) in Terminaux to allow visual editing.

In the other hand, the interactive hex viewer only allows you to view a hexadecimal representation of each byte without any editing functionality. This allows quick viewing of bytes in hexadecimal.

{% hint style="info" %}
You can consult the list of keybindings through the `K` key.
{% endhint %}

## Text editor and viewer

<figure><img src="../../../.gitbook/assets/image (97).png" alt=""><figcaption></figcaption></figure>

The interactive text editor allows you to seamlessly and interactively edit multi-line text. Inspired by VIM, the popular extensible terminal text editor, this text editor features two modes:

* Normal mode: You can perform some basic operations, such as finding and replacing, inserting a new line, removing a line, deleting a character, and entering the Insertion mode.
* Insertion mode: You can write your own text wherever you want

In the other hand, the interactive text viewer only allows you to view what's written and to search for a portion of the text.

{% hint style="info" %}
You can consult the list of keybindings through the `K` key.
{% endhint %}
