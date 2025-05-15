---
description: Make your command aliases!
icon: arrows-cross
---

# Command Aliasing

The MESH shell provides you with facility to make aliasing long commands easier than before. The alias management class, `AliasManager`, allows you to manage the shell aliases, like adding aliases, editing them, removing them, and so on.

Currently, the below functions are available for you to use:

* `AddAlias()`: Adds an alias to the list of aliases.
* `RemoveAlias()`: Removes an alias from the list of aliases.
* `DoesAliasExist()`: Checks to see if a particular alias exists.
* `GetAliasesListFromType()`: Gets a list of aliases from a shell type, excluding the built-in ones.
* `GetEntireAliasListFromType()`: Gets a list of aliases from a shell type, including the built-in ones.
* `GetAlias()`: Gets information about a specific alias.
