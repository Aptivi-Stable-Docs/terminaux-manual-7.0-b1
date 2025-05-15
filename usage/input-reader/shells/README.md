---
description: What is a shell?
icon: square-terminal
---

# Shells

<figure><img src="../../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

Operating systems contain their shells that listen to user input and execute any command – either built-in or custom – to perform operations that the users plan or need to do. Shells usually contain the prompt indicator to tell the user where is the current working directory, the user name, the host name, or anything that is set up to show.

In Linux systems, the shell is initiated with the help of both the log-in handler and the system initialization program, usually found in `/sbin/init`. Linux shells are numerous, like `zsh`, `dash`, and `bash`. In Windows, it has only two shells, which is PowerShell and Command Prompt (simulates the MS-DOS command prompt).

Each shell contain their own built-in commands and their usage and purpose that are hard-coded to the shell, and they're usually not distributed in a binary form. External commands are just programs or scripts that you would execute, but found in your system drive or any of the drives.

## Mirage Easy SHell (MESH)

This program is part of the core kernel that is programmed to be a standalone yet extensible shell. It provides you an ability to be able to implement your commands.

For more information about its inner workings and how you can build your own commands and shells, consult the below page.

{% content-ref url="shell-structure/" %}
[shell-structure](shell-structure/)
{% endcontent-ref %}
