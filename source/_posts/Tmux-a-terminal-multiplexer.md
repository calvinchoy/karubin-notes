---
title: 'Tmux, a terminal multiplexer'
tags:
  - command-line
  - terminal
  - tooling
  - ssh
  - shell
categories:
  - - command-line
  - - shell
date: 2018-11-10 10:07:55
---


Tmux is a terminal multiplexer for Unix-like operating systems. It allows multiple terminal sessions to be accessed simultaneously in a single window. It is useful for running more than one command-line program at the same time. It can also be used to detach processes from their controlling terminals, allowing SSH sessions to remain active without being visible ([wikipedia](https://en.wikipedia.org/wiki/Tmux)).

<!-- more -->

* Use tmux to create persistent sessions and organize it windows and panes.
* Tmux sessions have windows, and windows have panes.
* Tmux base shortcut always start with `Ctrl-b` following a key.
* Tmux can be configured by editing `~/.tmux.conf`
* Manage and automate Tmux sessions using [Tmuxinator](https://github.com/tmuxinator/tmuxinator)

## Tmux sessions
Create new tmux session with name
`tmux new -s <session-name>`

List availabe tmux sessions:
`tmux ls or Ctrl-b + s`

Attach to existing tmux session
`tmux a -t <session-name>`

Detach current sessiont
`tmux -d or Ctrl-b, d`

Rename session
`Ctrl-b + $`

Kill a session by name
`tmux kill-session -t <name>`

## Tmux Windows
Will only provide shortcuts (google if you want the named commands). Use these commands when you are already inside a tmux session default window.

Create new window
`Ctrl-b + c`

Rename current window
`Ctrl-b + ,`

List windows
`Ctrl-b + w`

Next window
`Ctrl-b + n`

Previous window
`Ctrl-b + p`

Jump to window by number
`Ctrl-b + 0-9`

## Tmux panes
Use these commands when you are in a window and want to split and navigate panes.

Split horizontal
`Ctrl-b + %`

Split vertical
`Ctrl-b + "`

Move to pane
`Ctrl-b + UDLR`

Kill current pane
`Ctrl-b + x`

## Resources
* [Tmux crash course by thoughbot](https://robots.thoughtbot.com/a-tmux-crash-course)
* [Tmux repo](https://github.com/tmux/tmux/wiki)
* [Tmuxinator repo](https://github.com/tmuxinator/tmuxinator)
* [Tmux wikipedia](https://en.wikipedia.org/wiki/Tmux)
