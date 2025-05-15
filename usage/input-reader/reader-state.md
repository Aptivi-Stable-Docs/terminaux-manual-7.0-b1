---
description: The reader state.
icon: badge-check
---

# Reader State

When the input reader is invoked by your console application, it creates a state class that is applicable to the current input read. The reader state contains variables that are building blocks for your custom bindings. You can also manipulate with the text positioning using the `PositioningTools` class.

## Variable-based States

The terminal reader state class contains the below most important variables that are documented here, alongside the less important ones.

* `InputPromptLeftBegin` and `InputPromptTopBegin`: Specifies the zero-based X and Y position that indicates the first character of where the first line of the input prompt is being written.
* `InputPromptLeft` and `InputPromptTop`: Specifies the zero-based X and Y position that indicates the first character of the input text in the first line of the input. It includes the left margin and the length of the last input prompt line.
* `LeftMargin` and `RightMargin`: Specifies the left margin and the right margin.
* `CurrentCursorPosLeft` and `CurrentCursorPosTop`: Specifies the current console cursor position relative to the current text position.
* `MaximumInputPositionLeft`: Specifies the maximum zero-based X position of the input that indicates the boundary of the input according to the right margin.
* `LongestSentenceLengthFromLeft`: Specifies the longest sentence length from the leftmost position with respect to the right margin.
* `LongestSentenceLengthFromLeftForFirstLine`: Specifies the longest sentence length from the leftmost position, subtracted from `InputPromptLeft`, in order to get the length for the first line.
* `LongestSentenceLengthFromLeftForGeneralLine`: Specifies the longest sentence length from the leftmost position, subtracted from `LeftMargin`, in order to get the length for a general input line.
* `CurrentTextPos`: Specifies the current text position as a one-based number.
* `InputPromptLastLineLength`: Specifies the last line length from the input prompt text relative to the current console width.
* `InputPromptText`: Specifies the input prompt text.
* `InputPromptHeight`: Specifies the height of the input prompt as simulated by the wrapped line splitter relative to the current console width.
* `CurrentText`: Specifies the current input text being written.
* `PasswordMode`: Specifies whether the reader is in the password mode or not.
* `PressedKey`: Specifies the currently-pressed key.
* `KillBuffer`: Specifies the kill-buffer for use with clipboard-related keybindings, such as Yank and Kill.
* `Settings`: Specifies the reader settings being passed to the reader.
* `CanInsert`: Specifies whether the user can insert a character or not.
* `OperationWasInvalid`: Whether an invalid key was pressed, or an invalid operation was performed, or not.
* `Concealing`: Whether the input is being concealed right now.
* `RefreshRequired`: Whether the operation requires a refresh at the end of the binding execution or not.

You can access the reader settings from the state, whether it's a general settings that Terminaux makes use of or it's an overridden settings instance, using the `Settings` property.

{% hint style="info" %}
In order to set `OperationWasInvalid` to true, you must put a conditional return by referring to the `ConditionalTools` and negating the `ShouldNot` condition like this:

```csharp
// If we're at the start of the text, bail.
if (!ConditionalTools.ShouldNot(state.CurrentTextPos == 0, state))
    return;
```
{% endhint %}
