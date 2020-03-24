---
title: Environment variable source files in Linux
date: 2020-03-23
description: Meanings of /etc/environment, /etc/profile, /etc/bash.bashrc and files in $HOME
tags: linux, variables, environment, bash, scripting
sources: https://unix.stackexchange.com/questions/26676/how-to-check-if-a-shell-is-login-interactive-batch
---

Shells are invoked as interactive and/or as login-shell, for example bash in some test cases:
| Test case           | Interactive | Login |
| ------------------- |-------------| ----- |
| `bash`              | No          | No    |
| `bash -i`           | Yes         | No    |
| `bash -l`           | No          | Yes   |
| `bash -i -l`        | Yes         | Yes   |
| SSH login [^1]      | Yes         | Yes   |
| Local TTY [^2]      | Yes         | No    |
| Terminal in Session | Yes         | No    |

[^1]: sshd 
[^2]: Even if you just logged in on terminal!

Interactive shells:
* `/etc/profile` better use `/etc/profile.d/*`
* `.bashrc` is only read by a shell that's both interactive and non-login

~/.ssh/environment (PermitUserEnvironment)
~/.ssh/rc (PermitUserRC) 
/etc/ssh/sshrc

/etc/profile
       The systemwide initialization file, executed for login shells
~/.bash_profile
       The personal initialization file, executed for login shells
~/.bashrc
       The individual per-interactive-shell startup file


Test-Script:
```bash
[[ $- == *i* ]] && echo 'Interactive' || echo 'Not interactive'
shopt -q login_shell && echo 'Login shell' || echo 'Not login shell'
```

If you login via SSH, it's an interactive login shell.

![Shell demo](test-shell.jpg)
