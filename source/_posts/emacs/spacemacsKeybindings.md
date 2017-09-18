---
title: Spacemacs keybindings
categories: emacs
tags: emacs
date: 2017-05-25 19:58:42
---
<!-- markdown-toc start - Don't edit this section. Run M-x markdown-toc-generate-toc again -->
**Table of Contents**

- [Common Stuffs](#common-stuffs)
- [Debug](#debug)
- [Search](#search)
- [Replace](#replace)
- [Toggle](#toggle)
- [Bookmark Related Opeation](#bookmark-related-opeation)
- [File Related Operation](#file-related-operation)
- [Buffer Related Operation](#buffer-related-operation)
- [Layout Related Operation](#layout-related-operation)
- [Window Related Operation](#window-related-operation)
- [Project Related Operation](#project-related-operation)
- [Ranger Related Operation](#ranger-related-operation)
- [Org mode](#org-mode)
- [JS2 Mode](#js2-mode)

<!-- markdown-toc end -->
<!--more-->
This is my Spacemacs personal config on Github: <https://github.com/ztlevi/spacemacs-config>

Common Stuffs
=============

In key bindings, M stands for Alt key (option key for mac), s for Command key, C for Control key, SPC for Space key.

| Key Bindings  | Description                                                                    |
|---------------|--------------------------------------------------------------------------------|
| C-g           | Quit                                                                           |
| **C-o**       | Evil jump backward                                                             |
| **C-i**       | Evil jump forward                                                              |
| **C-o**       | Open Action panel when mini dired enabled                                      |
| C-h k/v/f/d   | Key/ variable/ function/ Documentation                                         |
| C-h C-k/v/f   | Find key/ variable/ function                                                   |
| C-h e         | Show Emacs's errors                                                            |
| SPC SPC (M-x) | eval-buffer, customize-group                                                   |
| SPC e n       | Js2-next-error                                                                 |
| **s-/**       | Comment                                                                        |
| **SPC j i**   | Imenu (show all the functions)                                                 |
| **SPC v**     | Expand Region                                                                  |
| SPC x o       | Open link                                                                      |
| **C-q**       | Insert Quote                                                                   |
| SPC s e       | iedit: need to select in vim-visual mode, and then press the key to edit them. |
| SPC ?         | List key bindings                                                              |
| \*SPC '\*     | Pop up shell                                                                   |

Debug
=====

Kill emacs when not responding: `pkill -SIGUSR2 -i emacs`, and use `toggle-debug-on-quit` to enable C-g.

The following command profile the CPU.

    Profiler-start
    Profiler-report

| Key Bindings  | Description                                                            |
|---------------|------------------------------------------------------------------------|
| C-x C-e       | eval-last-sexp                                                         |
| M-.           | pop last command execute                                               |
| Diminish Undo | Show mode detail in the mode line, e.g. company-mode                   |
| SPC o (       | Switches to the buffer ‘\*ielm\*’, or creates it if it does not exist. |
| \*, d m\*     | macrostep-transient-state, expand and collapse funcs and macros        |

Search
======

| Key Bindings               | Description                                                                                                 |
|----------------------------|-------------------------------------------------------------------------------------------------------------|
| **SPC o d** (M-s o)        | **Occur dwim** (see the occurrences in codes and <br>go through them by toggling them), use e to enter edit |
| e                          | Go to edit mode (Under Occur mode)                                                                          |
| C-c C-c                    | Exit edit mode (Under Occur mode)                                                                           |
| **C-s**                    | Swiper                                                                                                      |
| **SPC r i / C-c C-r** (F6) | Ivy-resume, e.g. resume the swiper view                                                                     |
| **SPC r h**                | Helm-resume, e.g. resume counsel-git view                                                                   |
| SPC s                      | Grep(g), ag(a), ack(k), pt(t) &lt;br&gt;Project a/g p, Directory t/k f.                                     |
| **C-c C-e**                | Show results in another buffer, and then edit(e.g. replace).                                                |
| **C-c C-c**                | On the result buffer, commit changes.                                                                       |

Replace
=======

1.  Just use vim, `:%s/xxx/yyy/g(c)`
2.  Mark a key word, then use C-r (evil-quick-replace). It will automatically generate the vim command.
3.  Use Occur-dwim (SPC o d), then use iedit (SPC s e).

| Key Bindings | Description          |
|--------------|----------------------|
| M-%          | query-replace        |
| C-M-%        | query-replace-regexp |

Toggle
======

| Key Bindings | Description                 |
|--------------|-----------------------------|
| Spc t n      | Toggle line number          |
| Spc t r      | Toggle relative line number |
| **SPC t g**  | toggle golden ration        |
| **SPC t -**  | Center point                |
| SPC t f      | Toggle fci-mode             |

Bookmark Related Opeation
=========================

| Key Bindings | Description                                  |
|--------------|----------------------------------------------|
| Spc h b      | Open bookmarks in helm window                |
| C-d          | delete the selected bookmark                 |
| C-e          | edit the selected bookmark                   |
| C-f          | toggle filename location                     |
| C-o          | open the selected bookmark in another window |
| C-x C-d      | Run browse project directory                 |

File Related Operation
======================

| SPC f       | File related operation                       |
|-------------|----------------------------------------------|
| SPC p f     | Open file with projectile or counsel-git     |
| SPC f f     | Helm-find-file                               |
| C-M-j       | Ivy immediate done                           |
| SPC f L     | Find the file across the Whole Mac System    |
| SPC f l     | find file literally                          |
| SPC f h     | Open file in hex mode(C-c C-c to exit)       |
| **SPC f o** | Open in default external application         |
| **SPC f E** | sudo edit                                    |
| **SPC f j** | Jump to dried, remapped to ranger            |
| SPC f r     | Open recent file                             |
| SPC f R     | Rename current file                          |
| SPC f v     | Add local variable                           |
| SPC f a d   | find the current visited directory with fasd |
| SPC f C d/u | convert file encoding between unix and dos   |
| SPC f e d   | find the .spacemacs file                     |
| SPC f e i   | file the .emacs init file                    |
| SPC f b     | Show bookmarks                               |
| SPC f s/S   | Save buffers                                 |
| SPC f c     | Copy file                                    |
| SPC f t     | Open neo tree                                |

Buffer Related Operation
========================

| SPC b       | Buffer related operation   |
|-------------|----------------------------|
| **SPC TAB** | Switch back and forth      |
| SPC b .     | buffer micro state (hydra) |
| SPC b b     | Switch buffers             |
| SPC b d     | Kill buffer                |
| SPC b f     | Reveal in finder           |
| SPC b B/i   | iBuffer                    |
| SPC b h     | Spacemacs home buffer      |
| SPC b k     | Kill matching buffers      |
| SPC b N     | New empty buffer           |
| SPC b C-d   | Kill other buffers         |
| **SPC b R** | Safe revert buffer         |
| SPC b s     | Scratch buffer             |
| SPC b Y     | Yank the whole buffer      |
| SPC b P     | Paste the whole buffer     |
| SPC b w     | Write in dried buffer      |
| SPC b n/p   | Next/Previous buffer       |

Layout Related Operation
========================

| SPC l     | Layout related operation     |
|-----------|------------------------------|
| SPC o l l | load layout (ztlevi)         |
| SPC o l s | save layout (ztlevi)         |
| SPC l o   | Custom layout                |
| SPC l L/s | Load or Save layout          |
| SPC l l   | Switch between layouts       |
| SPC l R   | Rename current layout        |
| SPC l TAB | Quick switch between layouts |
| SPC l ?   | Toggle layout help           |

Window Related Operation
========================

| SPC w             | Window Related Operation            |
|-------------------|-------------------------------------|
| **SPC w .**       | Window micro state (cheat sheet)    |
| SPC w -/s         | Split window below and focus        |
| SPC w //v         | Split window right and focus        |
| SPC w m           | Toggle-maximize-buffer              |
| SPC w 2/3         | Use predefined window layout        |
| SPC w b           | Switch to mini buffer               |
| SPC w d           | Delete the current window           |
| SPC w h/j/k/l     | Move to window                      |
| **SPC w m**       | Maximize window                     |
| SPC w H/J/K/L     | Move window to position             |
| **SPC w u/U**     | Window undo/redo                    |
| SPC w o           | Switch to other frame               |
| SPC w F           | make a new frame                    |
| M/(SPC w) 1/2/3/4 | Go to window with the window number |
| SPC w =           | Balance windows                     |
| SPC w w           | Go to other window one by one       |
| SPC w W           | Ace windows                         |

Project Related Operation
=========================

| SPC p   | Project related operation               |
|---------|-----------------------------------------|
| SPC p f | Project files                           |
| SPC p b | Buffer files                            |
| SPC p p | Switch to a project                     |
| SPC p l | Switch to a project and create a layout |
| s-p     | Find files in project                   |

Ranger Related Operation
========================

| SPC a      | Ranger Related Operation                             |
|------------|------------------------------------------------------|
| C-c C-e    | Wdired-change-to-wdired-mode: write in ranger        |
| C-c C-c    | Commit changes                                       |
| C-c Esc    | Abort changes                                        |
| SPC a r    | launch ranger                                        |
| SPC a d    | deer (minimal ranger window in current directory)    |
| C-p        | (ranger) toggle ranger in dired buffer               |
| j          | (ranger) navigate down                               |
| k          | (ranger) navigate up                                 |
| h          | (ranger) go up directory                             |
| l          | (ranger) find file / enter directory                 |
| RET        | (ranger) find file / enter directory                 |
| dd/ **da** | (ranger) cut, da to add cut file                     |
| yy/ **ya** | (ranger) copy, ya to add copy file                   |
| pp         | (ranger) paste                                       |
| R          | (ranger) rename                                      |
| D          | (ranger) delete                                      |
| **;+**     | (ranger) create directory                            |
| f          | (ranger) search for file names, also can create file |
| i          | (ranger) show preview of current file                |
| zi         | (ranger) toggle showing literal / full-text previews |
| zh         | (ranger) toggle showing dotfiles                     |
| o          | (ranger) sort options                                |
| H          | (ranger) search through history                      |
| q          | (ranger) quit                                        |
| r          | (ranger) revert buffer                               |
| z-         | (ranger) reduce number of parents                    |
| z+         | (ranger) increment number of parents                 |
| v          | (ranger) toggle all marks                            |
| V          | (ranger) visually select lines                       |
| S          | (ranger) enter shell                                 |
| C-SPC      | (ranger) mark current file                           |
| ;C         | (ranger) copy directory / copy and move directory    |

Org mode
========

| Key Bindings      | Description |
|-------------------|-------------|
| SPC a o o (C-c a) | Org agenda  |
| SPC m s (C-c C-s) | Schedule    |
| SPC m d (C-c C-d) | Deadline    |
| C-c C-e           | Org Export  |

JS2 Mode
========

| Key Bindings                                | Description                                                                               |
|---------------------------------------------|-------------------------------------------------------------------------------------------|
| **js2-refactor commands**                   | A lot more key bindings could be found [here](https://github.com/magnars/js2-refactor.el) |
| , r &lt;                                    | js2r-forward-braf                                                                         |
| , r &gt;                                    | js2r-forward-slurp                                                                        |
| **The following 3 commands using xref-js2** |                                                                                           |
| M-.                                         | Jump to definition                                                                        |
| M-,                                         | Pop back to where M-. was last invoked.                                                   |
| M-?                                         | Jump to references                                                                        |
