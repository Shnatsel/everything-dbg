# everything-dbg
Install all debug symbols for a Debian package in one command.

## Why?

Let's say you want to debug or profile `xfce4-terminal`. To get debugging symbols for it on Debian (and its derivatives like Ubuntu or elementary OS) you'd run:

`$ sudo apt install xfce4-terminal-dbg`

However, debugger still shows a lot of unknown function calls! What do?

Turns out you have only installed debugging symbols for xfce4-terminal itself, but not for any of its libraries (gtk+, libvte, etc) which shoulder most of the actual work. There was no easy way to install debugging symbols for all the dependencies... until now.

## Introducing everything-dbg

`$ everything-dbg xfce4-terminal` will print names of -dbg packages for all dependencies of the specified package. Simply pass it to `apt install` to install them.

Features:

1. Fetches debugging symbols for dependencies of dependencies and so on all the way down to libc6-dbg.
1. Supports [-dbgsym packages](https://wiki.debian.org/AutomaticDebugPackages): uses -dbgsym package if it's available, otherwise uses -dbg
1. Checks that every -dbg package is actually installable, prints warnings and skips the ones that cannot be installed (Ubuntu has a bunch of -dbg packages which cannot be installed due to dependency issues)
1. Clean output on stdout, all messages go to stderr, so it can be easily combined with other tools.

## Installation

```
sudo apt install apt-rdepends
git clone https://github.com/Shnatsel/everything-dbg.git
```
