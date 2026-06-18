---
Weight: "3"
---
# Introduction

**Vim** (Vi IMproved) is a highly configurable, keyboard-driven text editor built directly into the Linux terminal. 

Sources to learn:
[vim-hero](https://www.vim-hero.com/)
[vim-adventures](https://vim-adventures.com/)
[vim-genius](http://vimgenius.com/)


There are two main modes for Vim:
- Normal mode
- Insert mode

## Normal mode

Also known as command mode is how `vi` starts by default. In this mode, keyboard keys are associated with commands for navigation and text manipulation tasks.

[[vim_normal_mode_cheatsheet.pdf]]

## Insert mode

The insert mode is straightforward: text appears on the screen as it is typed on the keyboard.

To enter Insert mode the user must execute an insertion command in the normal mode `i`.
To exit from Insert mode the user must execute an exit command which is `esc`.

## Colon Commands

The normal mode also supports another set of `vi` commands: the `colon commands`. They are executed after pressing the colon key `:` in normal mode.

[[vim_colon_commands_cheatsheet.pdf]]

## Alternative Editors

A simpler alternative is GNU nano, a small text editor that offers all basic text editing features.

![[nano-editor.png]]

---