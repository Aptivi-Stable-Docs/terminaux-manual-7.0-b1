---
description: How command parsing works
icon: badge-check
---

# Command Parsing

Once the `GetLine()` function gets your input, it attempts to split any command with the semicolon between them, like:

```
command1 arg1 arg2 ; command2 arg3 arg4
```

<figure><img src="../../../../.gitbook/assets/107-shell.png" alt=""><figcaption></figcaption></figure>

Any command that starts with either a space or a hashtag will be ignored as a comment, like: (Notice the extra space in the first comment)

```
 comment
#comment
```

<figure><img src="../../../../.gitbook/assets/108-shell.png" alt=""><figcaption></figcaption></figure>

The first word is a command, and all words following it in a single command text are the series of arguments. These words then get split to arguments (without the switch indicator `-switch`) and switches (arguments that come after the dash) using the `ProvidedArgumentsInfo` class, though it does much more than that.

This class contains these variables:

* `Command`: Target command
* `ArgumentsText`: Provided arguments and switches
* `ArgumentsList`: Array of arguments without the switches
* `SwitchesList`: Array of switches
* `RequiredArgumentsProvided`: Checks to see if the arguments are provided or not
* `RequiredSwitchesProvided`: Checks to see if the required switches are provided or not
* `RequiredSwitchArgumentsProvided`: Checks to see if the required switch arguments are provided or not

After the above class constructor is called, the shell attempts to execute an alias command, if found. Else, the built-in command is going to be executed.

Finally, the command executor thread is fired up with the `ExecuteCommandParameters` instance to hold command execution parameters for the same thread. The thread is then started.

## Command-line Arguments

The command-line arguments feature is backported from Nitrocid KS with more customization in place. This allows you to create a console application that handles arguments deeply, such as support for argument values.

To parse the arguments, you'll have to define a statically defined dictionary in a static class with a type of `Dictionary<string, ArgumentInfo>`, given that `ArgumentInfo` can be constructed with the following:

* `Argument`: The argument name that users will have to write down
* `HelpDefinition`: The description of the argument that will be shown in the help renderer
* `ArgArgumentInfo`: An array of argument info instances that will modify its behavior
* `ArgumentBase`: An argument executor instance that holds the actual code for the argument
* `Obsolete`: Whether this argument is obsolete or not

Afterwards, you can use the `ParseArguments()` function somewhere in the main application code. You can find the relevant classes in the `Terminaux.Shell.Arguments.Base` namespace.

{% hint style="info" %}
If you want to retain the behavior of Nitrocid KS 0.1.1 or earlier by considering every word as an argument, you can use the `ParseArgumentsLegacy()` function.

However, if you want to use the behavior of Nitrocid KS 0.1.2 or later by considering every word that matches one of the arguments as an argument, you can use the `ParseArguments()` function.
{% endhint %}

## Switch Management

You can know more about switch management by clicking on the below button:

{% content-ref url="command-switches.md" %}
[command-switches.md](command-switches.md)
{% endcontent-ref %}

### Special characters

<figure><img src="../../../../.gitbook/assets/105-shell.png" alt=""><figcaption></figcaption></figure>

If a command, such as `wrap`, is set to use the arguments string, you can escape special characters, as long as these characters are known. For example, if you want to pass a switch to a wrapped command, you can use the `wrap` command like this:

```
wrap help \-addon
```
