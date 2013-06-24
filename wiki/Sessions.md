---
title: Sessions
permalink: wiki/Sessions/
layout: wiki
---

X2Go Remote access
------------------

This a remote desktop solution akin to FreeNX. It is really fast and
useful for working directly on the cluster machines when you don't have
access to a Linux machine of your own. You can reconnect and get your
desktop session back (e.g.: windows and apps from last session).

Please take in mind that a desktop session takes up significant
resources so use this feature wisely and log out your session when you
don't need it anymore.

Terminal sessions
-----------------

You can use the screen and tmux terminal multiplexing software to
persist your console sessions on the nodes.

We recommend the use of byobu (tmux wrapper) that is already installed
on the nodes.

### Keybindings

F2 - Create a new window

F3 - Move to previous window

F4 - Move to next window

F5 - Reload profile

F6 - Detach from this session

F7 - Enter copy/scrollback mode

F8 - Re-title a window

F9 - Configuration Menu

F12 - Lock this terminal

shift-F2 - Split the screen horizontally

ctrl-F2 - Split the screen vertically

shift-F3 - Shift the focus to the previous split region

shift-F4 - Shift the focus to the next split region

shift-F5 - Join all splits

ctrl-F6 - Remove this split

ctrl-F5 - Reconnect GPG and SSH sockets

shift-F6 - Detach, but do not logout

alt-pgup - Enter scrollback mode

alt-pgdn - Enter scrollback mode

Ctrl-a $ - show detailed status

Ctrl-a R - Reload profile

Ctrl-a ! - Toggle key bindings on and off

Ctrl-a k - Kill the current window

Ctrl-a \~ - Save the current window's scrollback buffer

From <http://manpages.ubuntu.com/manpages/oneiric/en/man1/byobu.1.html>