---
description: Explaining the inner workings of all the kernel shells
icon: square-terminal
---

# Shell Structure

Shells can be built by implementing two different interfaces and base classes. Why two? Because the shell handler relies on:

* `BaseShell` and `IShell`: To hold shell type and initialization code
* `BaseShellInfo<ShellType>` and `IShellInfo`: To hold shell commands and the base shell

## Shell Handler

The shell handler, `ShellManager`, uses the available shell list, which holds the `BaseShellInfo` abstract class, to manipulate with that shell. That class can be get, depending on the needed type, with the `ShellManager.GetShellInfo()` function in the ︎`Nitrocid.Shell` namespace.

The shell handler also contains two properties: `CurrentShellType` and `LastShellType`. The former property holds the current shell type, which can be used with the shell management functions. The latter property holds the last shell type, which is usually the shell that you exited. However, there are three cases:

* If there are no shells in the shell stack, it returns the primary `Shell`
* If there is only one shell in the stack, it returns the current shell as the last one
* If there are two or more shells in the stack, it returns the last shell type

Additionally, when `GetLine()` is called, it sets Terminaux's reader history to point to the shell's history list. After it's done getting the input, it reverts back to the `General` history buffer. They are loaded on boot and saved on shutdown or reboot.

## Base Shell

The `BaseShell` abstract class, which your shell must override, contains the shell type name (`ShellType`), the flag to bail from the shell (`Bail`), and the shell initialization code with the shell arguments (`InitializeShell()`).

```csharp
public class YourShell : BaseShell, IShell
```

The shell initialization code usually waits for the `Bail` value to become `true` (the shell requested bailing, usually done by exiting the shell using the `exit` universal command), as in the below example code.

```csharp
public override void InitializeShell(params object[] ShellArgs)
{
    while (!Bail)
    {
        // Shell code
    }
}
```

While it's waiting for this to happen, the shell does what it's programmed to do, but in two conditions:

* All shells **must** call the `ShellManager.GetLine()` function, which usually is adaptive to your shell type. This is the below example code inside the shell initialization code to illustrate this:

```csharp
while (!Bail)
{
    ShellManager.GetLine();
}
```

* All shells **must** also handle both the `ThreadInterruptedException`, which must set `Bail` to `true`, and the general exceptions, which must call `continue` after dumping the exception to the debugger or to the console. For example, the below example code, inside the `InitializeShell()` function:

```csharp
while (!Bail)
{
    try
    {
        ShellManager.GetLine();
    }
    catch (ThreadInterruptedException)
    {
        Bail = true;
    }
    catch (Exception ex)
    {
        TextWriterRaw.WritePlain("There was an error in the shell." + CharManager.NewLine + "Error {0}: {1}", ex.GetType().FullName ?? "<null>", ex.Message);
        continue;
    }
}
```

The shell registration is required once you're done implementing the shell and all its required values, which will show you how to implement them in the next three pages. The function responsible for this action is `ShellTypeManager.RegisterShell()` in the `Terminaux.Shell.Shells` namespace.

{% hint style="danger" %}
Be sure to unregister your shell using the `UnregisterShell()` function, or the shell registry function will not update your `BaseShellInfo` class in the available shell lists!
{% endhint %}

### Shell Information

Every `BaseShell` class you create must accompany it with a separate class that implements the `BaseShellInfo` and `IShellInfo` classes, specifying your shell class name when inheriting the generic version of the `BaseShellInfo` class, as in below:

```csharp
internal class YourShellInfo : BaseShellInfo<YourShell>, IShellInfo
```

This is where your commands get together by overriding the `Commands` variable with the new dictionary containing all your commands, like below:

```csharp
public override List<CommandInfo> Commands => new()
{
    new CommandInfo("adduser", /* Localizable */ "Adds users",
        new[] {
            new CommandArgumentInfo(new[]
            {
                new CommandArgumentPart(true, "username"),
                new CommandArgumentPart(false, "password"),
                new CommandArgumentPart(false, "confirm"),
            }, Array.Empty<SwitchInfo>())
        }, new AddUserCommand(), CommandFlags.Strict),
    (...)
};
```

{% hint style="info" %}
You can omit the array definition of `CommandArgumentInfo` instances to create parameterless commands more easily.
{% endhint %}

In addition, you can override the `ShellPresets` class with a new dictionary containing all the presets for your shell, like below:

```csharp
public override Dictionary<string, PromptPresetBase> ShellPresets => new()
{
    { "Default", new DefaultPreset() }
};
```

The `ShellType` variable found within the `BaseShellInfo` class is a wrapper for the `ShellBase.ShellType` variable for easier access. It's not overridable and is defined like this:

```csharp
public string ShellType => ShellBase.ShellType;
```

By default, all the shells provide you a multi-line prompt, but if you want your input to be in one line wrapped mode, you can override the below property:

```csharp
public override bool OneLineWrap => false;
```

If your shell meets the following conditions:

* You need to handle written text in a way, and
* You need to use your commands with a slash character,

Then, you need to override the two properties in order for your special non-slash handler to execute:

```csharp
public override bool SlashCommand => true;
public override CommandInfo NonSlashCommandInfo => new CommandInfo(...);
```

{% hint style="info" %}
If you need to know how to define a command information class, consult [here](command-information.md).
{% endhint %}

## Base Command

The base command is required to be implemented, since it contains overridable command execution code. Your command must implement the command base class below:

```csharp
class YourCommand : BaseCommand, ICommand
```

The only function that you need to override is `Execute()`, which you can override like below:

```csharp
public override void Execute(CommandParameters parameters, ref string variableValue)
```

To support dumb consoles that don't support positioning or complex console functions, you can override `ExecuteDumb()`:

```csharp
public override void ExecuteDumb(CommandParameters parameters, ref string variableValue)
```

Additionally, you can override the extra help function, `HelpHelper()`, like this:

```csharp
public override void HelpHelper()
```

{% hint style="info" %}
If you want to support redirection or wrapping, you must either take dumb console support into account on the `Execute()` function by not calling any of the below console wrappers, or you must override the `ExecuteDumb()` function shown above to be compatible with the dumb consoles.

The following wrappers should not be called (explicitly and implicitly) on that function:

* `CursorLeft` (set)
* `CursorTop` (set)
* `ForegroundColor`
* `BackgroundColor`
* `CursorVisible`
* `OutputEncoding`
* `InputEncoding`
* `KeyAvailable`
* `Beep()`
* `Clear()`
* `OpenStandardError()`
* `OpenStandardInput()`
* `OpenStandardOutput()`
* `ReadKey()`
* `ResetColor()`
* `SetCursorPosition()`
* `SetOut()`
{% endhint %}

### Registering your command

In order for your command to be usable, your mods are now required to register the commands manually using a function that helps doing this. That function is defined in the `CommandManager` class.

{% code title="CommandManager.cs" lineNumbers="true" %}
```csharp
public static void RegisterCustomCommand(ShellType ShellType, CommandInfo commandBase)
public static void RegisterCustomCommand(string ShellType, CommandInfo commandBase)
public static void RegisterCustomCommands(ShellType ShellType, CommandInfo[] commandBases)
public static void RegisterCustomCommands(string ShellType, CommandInfo[] commandBases)
```
{% endcode %}

Similarly, if your mod is going to stop, you must unregister all your mod commands, including those that it created in the middle of the kernel uptime. You can use the following functions:

{% code title="CommandManager.cs" lineNumbers="true" %}
```csharp
public static void UnregisterCustomCommand(ShellType ShellType, string commandName)
public static void UnregisterCustomCommand(string ShellType, string commandName)
public static void UnregisterCustomCommands(ShellType ShellType, string[] commandNames)
public static void UnregisterCustomCommands(string ShellType, string[] commandNames)
```
{% endcode %}

If you've registered your commands correctly, the `help` command list should list your mod command that you've registered using one of the `RegisterCustomCommand` functions.

## More?

For guidance on how to define your command, click the below button:

{% content-ref url="command-information.md" %}
[command-information.md](command-information.md)
{% endcontent-ref %}

For guidance on how to define and manage your command's switches, click the below button:

{% content-ref url="command-switches.md" %}
[command-switches.md](command-switches.md)
{% endcontent-ref %}

For information about the help system and how it works, consult the below page:

{% content-ref url="help-system.md" %}
[help-system.md](help-system.md)
{% endcontent-ref %}

For command parsing, click the below button:

{% content-ref url="command-parsing.md" %}
[command-parsing.md](command-parsing.md)
{% endcontent-ref %}

For shell presets, click the below button:

{% content-ref url="shell-presets.md" %}
[shell-presets.md](shell-presets.md)
{% endcontent-ref %}

For command aliasing, click the below button:

{% content-ref url="command-aliasing.md" %}
[command-aliasing.md](command-aliasing.md)
{% endcontent-ref %}
