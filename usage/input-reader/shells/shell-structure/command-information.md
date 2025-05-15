---
description: Define this command for me!
icon: info
---

# Command Information

Each command you define in your shell must provide a new instance of the `CommandInfo` class holding details about the specified command. The new instance of the class can be made using one of the constructors defined below:

```csharp
public CommandInfo(string Command, string HelpDefinition, CommandArgumentInfo[] CommandArgumentInfo, BaseCommand CommandBase)
public CommandInfo(string Command, string HelpDefinition, BaseCommand CommandBase)
```

where:

* `Command`: The command
* `HelpDefinition`: The brief summary of what the command does
* `CommandArgumentInfo`: Array of argument information about your command (can be omitted)
* `CommandBase`: An instance of the `BaseCommand` containing command execution information

To implement `CommandArgumentInfo`, call the constructor either with no parameters, which implies that there is no argument required to run this command, or with the following options listed below.

```csharp
public CommandArgumentInfo()
public CommandArgumentInfo(bool AcceptsSet)
public CommandArgumentInfo(bool AcceptsSet, bool infiniteBounds)
public CommandArgumentInfo(CommandArgumentPart[] Arguments)
public CommandArgumentInfo(CommandArgumentPart[] Arguments, bool AcceptsSet)
public CommandArgumentInfo(CommandArgumentPart[] Arguments, bool AcceptsSet, bool infiniteBounds)
public CommandArgumentInfo(SwitchInfo[] Switches)
public CommandArgumentInfo(SwitchInfo[] Switches, bool AcceptsSet)
public CommandArgumentInfo(SwitchInfo[] Switches, bool AcceptsSet, bool infiniteBounds)
public CommandArgumentInfo(CommandArgumentPart[] Arguments, SwitchInfo[] Switches)
public CommandArgumentInfo(CommandArgumentPart[] Arguments, SwitchInfo[] Switches, bool AcceptsSet)
public CommandArgumentInfo(CommandArgumentPart[] Arguments, SwitchInfo[] Switches, bool AcceptsSet, bool infiniteBounds)
```

where:

* `Arguments`: Defines the command arguments
* `Switches`: Defines the command switches
* `AcceptsSet`: Whether to accept the `-set` switch
* `infiniteBounds`: Whether to accept infinite number of arguments or not

For `CommandArgumentPart` instances, consult the below constructor to create an array of `CommandArgumentPart` instances when defining your commands:

```csharp
public CommandArgumentPart(bool argumentRequired, string argumentExpression, Func<string[], string[]> autoCompleter = null, bool isNumeric = false, string[] exactWording = null, string argumentDesc = "")
```

where:

* `argumentRequired`: Is this argument part required?
* `argumentExpression`: Command argument expression
* `autoCompleter`: Auto completion function delegate
  * The first `string[]` denotes the list of last passed arguments
  * The second `string[]` (output) denotes the suggestions returned
* `isNumeric`: Whether this argument part accepts numeric values only
* `exactWording`: If not empty, the user must write one of the words declared in this variable for this argument to be satisfied
* `argumentDesc`: Argument description that shows up in the help entry

{% hint style="info" %}
When it comes to auto-completion, if you press `TAB` on any of the argument positions, the shell will select the following completers as appropriate:

* If the auto completer is specified, then, regardless of whether the expression represents the selection (expressions containing the slash `/` character) or not, the auto completer specified in the constructor will be called.
* If the auto completer is not specified, then it will go through the following completers:
  * The shell goes through the list of known completion expressions according to the argument expression, which are the following:
    * `cmd`, `command`: List of all available commands
    * `shell`: List of all available shells
  * If the expression is not listed in any of the known expressions list, it'll check for the selection indicator characters (the slash `/` key).
    * For example, the `true/false` expression will generate an autocompleter that completes the two words: `true` and `false`.
  * In case there is none, the shell will use the default auto completer, which returns nothing.
{% endhint %}

{% hint style="success" %}
Usually, there is no need for you to cut the string to the required position; the shell does it to every single autocomplete result that is given.
{% endhint %}

### Command argument part with options

In case you want to expressively specify the options without having to use default values for all parameters to set a certain parameter, you can use the `CommandArgumentPartOptions` overload:

```csharp
public CommandArgumentPart(bool argumentRequired, string argumentExpression, CommandArgumentPartOptions options)
```
