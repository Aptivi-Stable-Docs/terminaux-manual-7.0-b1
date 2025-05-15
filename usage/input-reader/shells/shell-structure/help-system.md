---
description: Inner workings of the help system
icon: question
---

# Help System

The help system is what every shell uses, invoked by the unified `help` command available for every type of shell. The function responsible for showing help entries or command usage and some extra help is `HelpSystem.ShowHelp()` in the `Terminaux.Shell.Commands` namespace. Explore with us the mechanics of the help system below.

## General help

When the user requests the `help` command in any shell, the above function gets called, querying the current shell type (`Shell.CurrentShellType`) as discussed previously.

The function gets all the commands, including the unified ones, from the command type, but also takes care of the aliased commands. The help system then prints the list of commands to the console.

## Command help

If the user specified a command when calling the `help` command, the help system extracts the help definition and all the command usages.

It extracts from these values found in the `CommandInfo` class:

* `HelpDefinition`: The brief summary of what the command does
* `CommandArgumentInfo`: The command argument info that supplies the below information:
  * `.Arguments`: Defines the command arguments
  * `.Switches`: Defines the command switches
  * `.RenderedUsage`: Defines the rendered usage to be printed for a command

The rendered usage has the following characteristics:

* For required switches, they're surrounded with the `<` and the `>` marks. Switches that are not required are surrounded with the `[` and the `]` marks instead.
* Switches that require values don't have the `[` and the `]` marks surrounding the `=value` part, indicating that the switch needs a value.
* For required arguments, they're surrounded with the `<` and the `>` marks. Arguments that are not required are surrounded with the `[` and the `]` marks instead.
* For numeric arguments, a marker is shown indicating that it only accepts numbers.
* For switches that conflict, they're put in a group, such as `[-switch1|-switch2]`.
