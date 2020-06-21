---
layout: post
title:  "Multi-cursor and selection - 에디터 다중선택 편집"
date:   2020-06-21 09:40:00
categories: Python Dev
---

*(create: '20.6.21, update: '20.6.21)*

## VS Code Multi-cursor and selection

- Key Bindings for Visual Studio Code : <https://code.visualstudio.com/docs/getstarted/keybindings>

- MaxOS (source: [Visual Studio Code Keyboard shortcuts for macOS, PDF](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-macos.pdf))

  | Keybinding      | Command                                     | 설명                                                |
  | :-------------- | :------------------------------------------ | :-------------------------------------------------- |
  | ⌥ + click       | Insert cursor                               | 다중선택 할 지점에서 "Ctrl + 클릭, 클릭, 클릭, ..." |
  | ⌥⌘↑             | Insert cursor above                         |                                                     |
  | ⌥⌘↓             | Insert cursor below                         |                                                     |
  | ⌘U              | Undo last cursor operation                  |                                                     |
  | ⇧⌥I             | Insert cursor at end of each line selected  |                                                     |
  | ⌘L              | Select current line                         |                                                     |
  | ⇧⌘L             | Select all occurrences of current selection |                                                     |
  | ⌘F2             | Select all occurrences of current word      |                                                     |
  | ⌃⇧⌘→ / ←        | Expand / shrink selection                   |                                                     |
  | ⇧⌥ + drag mouse | Column (box) selection                      |                                                     |
  | ⇧⌥⌘↑ / ↓        | Column (box) selection up/down              |                                                     |
  | ⇧⌥⌘← / →        | Column (box) selection left/right           |                                                     |
  | ⇧⌥⌘PgUp         | Column (box) selection page up              |                                                     |
  | ⇧⌥⌘PgDn         | Column (box) selection page down            |                                                     |
  | → / ← / ↑ / ↓   | Multi-cursor moving left/right/up/down      |                                                     |

- Windows (source: [Visual Studio Code Keyboard shortcuts for Windows, PDF](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-windows.pdf))

- Linux (source: [Visual Studio Code Keyboard shortcuts for Linux, PDF](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-linux.pdf))

## Jupyter Notebook Multi-cursor and selection
