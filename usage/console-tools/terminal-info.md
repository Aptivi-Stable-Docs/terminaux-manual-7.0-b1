---
description: What's your terminal type and its capabilities?
icon: square-terminal
---

# Terminal Info

Terminal information database is a list of terminal capabilities that control how console applications determine capabilities in the terminal type that the emulator uses, such as the color depth capability and the method of writing sequences that change the background and the foreground color. Termcap was implemented in 1978, and Terminfo was implemented in 1981-1982. Applications that use `ncurses` (for non-C# applications) or Terminaux (for C# applications) can use the database to get the capabilities.

## `TermInfoDesc` class

The TermInfo feature of Terminaux can be found in the base console tools namespace, `Terminaux.Base.TermInfo`.  `TermInfoDesc`'s functions contain the following:

* `TryLoad()`: Tries to load a terminal information description given the terminal type name.
* `Load()`: Loads a terminal information description given the terminal type name, and if the name is not given, it uses the current terminal type that your terminal emulator uses. If `TryLoad()` fails and you've specified a name, it throws an exception. Otherwise, it gives you a fallback `TermInfoDesc` instance.
* `LoadSafe()`: Loads a terminal information description given the terminal type name, and if the name is not given, it uses the current terminal type that your terminal emulator uses. If `TryLoad()` fails or `$TERM` is not specified, it gives you a fallback `TermInfoDesc` instance.
* `GetBuiltins()`: Gets a list of built-in terminal type names that Terminaux can find in the built-in capabilities list.

{% hint style="info" %}
This feature used to be exclusive to Linux users mostly, but we've added the built-in terminal information database so that Windows applications are now free to analyze such data, although `conhost` doesn't emulate any terminal, and is assumed to be compatible with `xterm`.
{% endhint %}

Built-in terminal capabilities can be accessed as properties in the `TermInfoDesc` instance that the loading functions return when parsing the terminal information files. For extra properties that Terminaux doesn't cover, this class provides you with the following functions:

* `GetBoolean()`: Gets a boolean value that holds either true or false. Returns null, however, if Terminaux is unable to get the value.
* `GetNum()`: Gets a number value that holds a numeric integer. Returns null, however, if Terminaux is unable to get the value.
* `GetString()`: Gets a textual value. Returns null, however, if Terminaux is unable to get the value.

`TermInfoDesc` also allows you to get an instance of `TermInfoDesc` corresponding to the current terminal type as specified in the `$TERM` environment variable for non-Windows systems. Windows systems always use the `xterm-256color` terminal for maximum compatibility. You can get this instance using one of the following properties:

* `Current`: Returns a `TermInfoDesc` instance corresponding to your terminal type.
* `Fallback`: Returns a `TermInfoDesc` instance corresponding to `xterm-256color`.

### TermInfo string parameters

Terminaux supports all the [printf(3)](https://manpages.debian.org/bullseye/manpages-dev/printf.3.en.html)-like string parameters that are defined in the [Parameterized Strings](https://manpages.debian.org/bullseye/ncurses-bin/terminfo.5.en.html#Parameterized_Strings) section from the `terminfo(5)` manual page found in the NCurses library. The following string parameters are supported according to the types:

| Parameter                               | Type                   | Description                                      |
| --------------------------------------- | ---------------------- | ------------------------------------------------ |
| `%%`                                    | Format                 | Writes a literal `%`                             |
| `%[[:]flags][width[.precision]][doxXs]` | Format                 | Formats a parameter in a way similar to `printf` |
| `%c`                                    | Format                 | Print a parameter as an unsigned character       |
| `%s`                                    | Format                 | Print a parameter as a string                    |
| `%'c'`                                  | Constants              | Single character constant                        |
| `%{nn}`                                 | Constants              | Integral constant                                |
| `%p[1-9]`                               | Manipulation           | Pushes the `n`th parameter                       |
| `%P[a-z]`                               | Manipulation           | Set dynamic variable to pop                      |
| `%g[a-z]`                               | Manipulation           | Get dynamic variable to push                     |
| `%P[A-Z]`                               | Manipulation           | Set static variable to pop                       |
| `%g[A-Z]`                               | Manipulation           | Get static variable to push                      |
| `%l`                                    | Manipulation           | Formats as string length of the pop'd variable   |
| `%i`                                    | Manipulation           | Adds 1 to the first two variables                |
| `%+`                                    | Binary (arithmetic)    | Adds two variables                               |
| `%-`                                    | Binary (arithmetic)    | Subtracts two variables                          |
| `%*`                                    | Binary (arithmetic)    | Multiplies two variables                         |
| `%/`                                    | Binary (arithmetic)    | Divides two variables                            |
| `%m`                                    | Binary (arithmetic)    | Returns mod of two variables                     |
| `%&`                                    | Binary (bit ops)       | Bitwise AND                                      |
| `%\|`                                   | Binary (bit ops)       | Bitwise OR                                       |
| `%^`                                    | Binary (bit ops)       | Bitwise exclusive OR                             |
| `%=`                                    | Binary (logical ops)   | Two variables equal                              |
| `%<`                                    | Binary (logical ops)   | Two variables less than                          |
| `%>`                                    | Binary (logical ops)   | Two variables greater than                       |
| `%A`                                    | Conditional operations | Logical AND                                      |
| `%O`                                    | Conditional operations | Logical OR                                       |
| `%!`                                    | Unary operations       | Logical complement                               |
| `%~`                                    | Unary operations       | Bit complement                                   |
| `%? expr %t thenpart %e elsepart %;`    | Conditional            | If-then-else conditional                         |

### Parameter Extraction

You can extract parameters from a capability string by using the `ExtractParameters()` function found in the `ParameterExtractor` class, passing it the capability that you want to parse. This returns an array of `ParameterInfo` instances that contain the following properties:

* Representation: The parameter that has been extracted from the capability string.
* Index: Zero-based index of the first character of the representation relative to the capability string.

For example, we have this string: `<ESCAPE>=%p1%' '%+%c%p2%' '%+%c`, with `<ESCAPE>` being a designator for `\u001b` that corresponds to the ESCAPE character essential for all terminal [VT sequences](textual-ui/vt-sequences.md) according to Unicode and ASCII encoding. When we ran this string through the parameter extractor, we got this result:

```
<ESCAPE> is not a parameter at index 0
=        is not a parameter at index 1

%p1  starts at index 2
  Representation: %p1
  Index:          2
%' ' starts at index 5
  Representation: %' '
  Index:          5
%+   starts at index 9
  Representation: %+
  Index:          9
%c   starts at index 11
  Representation: %c
  Index:          11
%p2  starts at index 13
  Representation: %p2
  Index:          13
%' ' starts at index 16
  Representation: %' '
  Index:          16
%+   starts at index 20
  Representation: %+
  Index:          20
%c   starts at index 22
  Representation: %c
  Index:          22
```

{% hint style="info" %}
For now, it's up to you how to process such strings to manipulate with the parameters. However, in a future Terminaux release, we'll release features that will assist you.
{% endhint %}
