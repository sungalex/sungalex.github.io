---
layout: post
title:  "Multi-cursor and selection - 다중선택 편집"
date:   2020-06-21 09:40:00
categories: Python Dev
---

*(create: '20.6.21, update: '20.6.21)*

## VS Code Multi-cursor and selection

- Key Bindings for Visual Studio Code : <https://code.visualstudio.com/docs/getstarted/keybindings>

- MaxOS (source: [Visual Studio Code Keyboard shortcuts for MacOS, PDF](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-macos.pdf))

  | Keybinding      | Command                                     | Description                                         |
  | :-------------- | :------------------------------------------ | :-------------------------------------------------- |
  | ⌥ + click       | Insert cursor                               | 다중선택 할 지점에서 "Ctrl + 클릭, 클릭, 클릭, ..." |
  | ⌥⌘↑             | Insert cursor above                         | 커서의 위 방향으로 다중 선택                        |
  | ⌥⌘↓             | Insert cursor below                         | 커서의 아래 방향으로 다중 선택                      |
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

- reference: [Jupyter notebook에서 Multi-Cursor / Multiple Selection 적용하기](https://rrbb014.tistory.com/26)
  - [Sublime-style multiple cursors in Jupyter](https://www.perfectlyrandom.org/2016/03/19/sublime-text-style-multiple-cursors-in-jupyter-notebook/)
  - <https://github.com/jupyter/notebook/issues/278>

- source: <https://github.com/sungalex/aiqa/blob/master/Sublime-style_multiple_cursors_in_Jupyter.ipynb>

- Keyboard Shortcuts 환경설정

  - 아래의 환경설정을 하지 않아도 `Cmd + 멀티 클릭`과 `Cmd + 방향키`는 동작하지만, 다른 에디터에서 사용하던 단축키를 사용하기 위해서는 아래와 같은 환경설정이 필요합니다. 

  1. Jypyter Notebook을 실행시켜서 Jupyter 설정 폴더 찾기

      ~~~ipython
      from jupyter_core.paths import jupyter_config_dir
      
      jupyter_dir = jupyter_config_dir()
      print(jupyter_dir)        # Jupyter 설정 디렉토리 경로 (ex. `/Users/alex/.jupyter`)
      ~~~

  2. Jupyter 설정 폴더로 이동하여, custom 디렉토리에 custom.js 파일 생성 (폴더 및 파일 생성 -> 있는 경우 파일 오픈)

      ~~~bash
      $ cd /Users/alex/.jupyter     # Jupyter 설정 디렉토리
      $ mkdir custom                # custom 디렉토리가 있는 경우 생략
      $ cd custom
      $ vi custom.js                # custom.js 생성 또는 오픈
      ~~~

  3. custom.js 파일에 아래의 구문 삽입

      ~~~bash
      require(["codemirror/keymap/sublime", "notebook/js/cell", "base/js/namespace"],
          function(sublime_keymap, cell, IPython) {
              cell.Cell.options_default.cm_config.keyMap = 'sublime';
              var cells = IPython.notebook.get_cells();
              for(var c=0; c < cells.length ; c++){
                  cells[c].code_mirror.setOption('keyMap', 'sublime');
              }
          } 
      );
      ~~~

- Multi-cursor Keyboard Shortcuts ([Sublime Text Unofficial Documentation: Keyboard Shortcuts - OSX](https://sublime-text-unofficial-documentation.readthedocs.io/en/sublime-text-2/reference/keyboard_shortcuts_osx.html))

  ![sublime keyboard shortcuts](/img/sublime-keyboard-shortcuts-editing.png)

- Windows : [Sublime Text 3 - Useful Shortcuts (Windows)](https://gist.github.com/mrliptontea/4c793ebdf72ed145bcbf)
