---
description: We need to filter and build the VT sequences.
icon: wave-sine
---

# VT Sequences

In your own terminal emulator, VT sequences are the power of any terminal emulator found in literally every PC.

This feature provides several filtering and manipulation tools which allow you to perform these operations on strings that contain escape sequences under the `Terminaux.Sequences` namespace. Currently, these tools are provided:

| Function                            | Description                                                                                        |
| ----------------------------------- | -------------------------------------------------------------------------------------------------- |
| `FilterVTSequences()`               | Filters all of the VT sequences that are of either a single type or of multiple types              |
| `MatchVTSequences()`                | Matches all of the VT sequences that are of either a single type or of multiple types              |
| `IsMatchVTSequences()`              | Does the string contain all of the VT sequences or a VT sequence of one or more types?             |
| `IsMatchVTSequencesSpecific()`      | Does the string contain all of the VT sequences or a VT sequence of any specific type?             |
| `SplitVTSequences()`                | Splits all of the VT sequences that are either of a single type or of multiple types               |
| `DetermineTypeFromText()`           | Determines the VT sequence type from the given text                                                |
| `GetSequenceFilterRegexFromType()`  | Gets the sequence filter regular expression from the provided VT sequence type                     |
| `GetSequenceFilterRegexFromTypes()` | Gets the sequence filter regular expression list from the provided VT sequence types (one or more) |

## Usage

Place the `using Terminaux.Sequences;` clause at the top of the file that you want to call these functions in. You need to put the class name `VtSequenceTools` before the function name mentioned above so that it looks like this:

<pre class="language-csharp"><code class="lang-csharp">char BellChar = Convert.ToChar(0x7);
char EscapeChar = Convert.ToChar(0x1b);
char StringTerminator = Convert.ToChar(0x9c);
string vtSequence1 = $"{EscapeChar}[38;5;43m";
<strong>string filtered = VtSequenceTools.FilterVTSequences($"Hello!{vtSequence1}");
</strong><strong>Console.WriteLine(filtered);
</strong></code></pre>

### Sequence builder

Terminaux offers a `Builder` namespace that contains building blocks for building a VT sequence for your console applications.

It starts with `VtSequenceBasicChars` which allows you to get a variety of starting-point characters for your VT sequence in case you want to manually build the sequence yourself. Here are the available characters:

* `BEL (\x07 - CTRL+G - BellChar)`
* `BS (\x08 - CTRL+H - BackspaceChar)`
* `CR (\x0D - CTRL+M - CarriageReturnChar)`
* `ENQ (\x05 - CTRL+E - ReturnTerminalStatusChar)`
* `FF (\x0C - CTRL+L - FormFeedChar)`
* `LF (\x0A - CTRL+J - LineFeedChar)`
* `SI (\x0F - CTRL+O - StandardCharacterSetChar)`
* `SO (\x0E - CTRL+N - AlternateCharacterSetChar)`
* `SP (" " - SPACE - SpaceChar)`
* `TAB (\x09 - CTRL+I - HorizontalTabChar)`
* `VT (\x0B - CTRL+K - VerticalTabChar)`
* `ESC (\x1B - VerticalTabChar)`
* `ST (\x9C - VerticalTabChar)`

Each type of VT sequence contain their own class files that stores both the regex match information about specific actions and sequence generation functions based on the given action and argument. Here are a list of supported sequence types:

* APC sequences
  * Application program command
* C1 sequences
  * 8-bit control characters
* CSI sequences
  * Controls beginning with control sequence introducer
* DCS sequences
  * Device control
* ESC sequences
  * Controls beginning with ESC
* OSC sequences
  * Operating system command sequences
* PM sequences
  * Privacy message

To learn more about these sequences, visit the below page:

{% embed url="https://invisible-island.net/xterm/ctlseqs/ctlseqs.html" %}

The builder also provides a powerful tool which allows you to build almost any VT sequence using only the arguments and the specific type of VT sequence (Character attributes for example). This tool is found inside the `VtSequenceBuilderTools` class under the `Terminaux.Sequences.Builder` namespace.

Currently, it provides these tools:

* `BuildVtSequence(VtSequenceSpecificTypes specificType, params object[] arguments)`
  * Allows you to build your VT sequence
  * Returns a string consisting of a VT sequence of the requested type with the requested arguments
* `DetermineTypeFromSequence(string sequence)`
  * Allows you to determine the type from a specific VT sequence
  * Returns a tuple of `(VtSequenceType, VtSequenceSpecificTypes)` which holds both the broad VT sequence type (CSI for example) and the specific type (Character attribute for example).

## Techniques

There are currently four types of operations.

### Filters

Found in `VtSequenceTools.FilterVTSequences()`, when this function is called, Terminaux selects the appropriate regular expression for the sequence type and replaces the found sequences with blanks. You can optionally replace it with something, like a text, a syntax, or even another VT sequence.

### Matches

Found in `VtSequenceTools.MatchVTSequences()`, when this function is called, Terminaux selects the appropriate regular expression for the sequence type and gets all the matched regular expressions. You can then wrap the values in the `for` or the `foreach` loop to get match information for each matched sequence.

### Queries

Found in `VtSequenceTools.IsMatchVTSequences()`, when this function is called, Terminaux selects the appropriate regular expression for the sequence type and checks the text to see if any part of the text is a VT sequence.

Additionally, it contains `IsMatchVTSequencesSpecific()`, which helps to check the text for any specific VT sequence type.

### Splits

Found in `VtSequenceTools.SplitVTSequences()`, when this function is called, Terminaux selects the appropriate regular expression for the sequence type and splits the text with the matched VT sequences as delimiters.

## Regex of VT expressions

Each type of VT sequences listed below by the `VtSequenceRegexes` class are supported by Terminaux for the above operations.

* CSI sequences (`CSISequences`)
  * `(\x9B|\x1B\[)[0-?]*[ -\/]*[@-~]`
* OSC sequences (`OSCSequences`)
  * `(\x9D|\x1B\]).+(\x07|\x9c)`
* ESC sequences (`ESCSequences`)
  * ``\x1b [F-Nf-n]|\x1b#[3-8]|\x1b%[@Gg]|\x1b[()*+][A-Za-z0-9=`<>]|\x1b[()*+]""[>4?]|\x1b[()*+]%[0-6=]|\x1b[()*+]&[4-5]|\x1b[-.\/][ABFHLM]|\x1b[6-9Fcl-o=>\|\}~]``
* APC sequences (`APCSequences`)
  * `(\x9f|\x1b_).+\x9c`
* DCS sequences (`DCSSequences`)
  * `(\x90|\x1bP).+\x9c`
* PM sequences (`PMSequences`)
  * `(\x9e|\x1b\^).+\x9c`
* C1 sequences (`C1Sequences`)
  * `\x1b[DEHMNOVWXYZ78]`
* All VT sequences (`AllVTSequences`)

## Usage in console writers

All console writers internally use the VT sequence filtering tools, like `GetFilteredPositions()` that uses `FilterVTSequences()`, to be able to determine the exact text position. This is to work around Linux Mono installs that report wrong position when VT sequences are appended.

{% hint style="info" %}
This workaround was not necessary as of the modern .NET implementation, but the workaround is still in place, because Terminaux targets .NET Standard, which means that it can be used for .NET Framework console projects, and, thus, Mono on Linux.
{% endhint %}

It works by seeking through every visible letter from the text in the form of "advancing" so that `GetFilteredPositions()` can make sure that the filtered positions are actually correct and sought "to the last letter" rather than "past the last letter" that Mono and the normal `Console.Write()` and `Console.WriteLine()` were suffering.
