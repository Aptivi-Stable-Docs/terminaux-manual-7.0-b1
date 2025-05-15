---
description: Something is wrong here.
icon: stethoscope
---

# Console Logging

The `ConsoleLogger` class in the `Terminaux.Base` namespace allows you to control console logging that Terminaux utilizes. This is to aid in debugging display-related issues, color-related issues, and more problems related to the general operation of Terminaux.

You can enable or disable logging for the lifetime of the application by setting the `EnableLogging` property to either `true` or `false`, depending on whether you need to turn logging on or off. Once done, you should be able to see information about what Terminaux is doing.

{% hint style="info" %}
Currently, only a single message gets printed to the Terminaux log files, but we'll make sure that the logs contain diagnostic information in the next release.
{% endhint %}

You can find the log files under:

* Windows: `%LOCALAPPDATA%/Aptivi/Logs`
* Unix: `~/.config/Aptivi/Logs`

Search for your application name, and scroll through the logs to find some interesting information about what Terminaux is doing prior to the time that you think that a bug occurred.
