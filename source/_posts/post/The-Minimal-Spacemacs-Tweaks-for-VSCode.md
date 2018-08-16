---
title: Spacemacs/Space-Vim Config for VSCode
date: 2017-12-02 00:35:26
categories: post
tags: [spacemacs, vscode, space, intellij idea, pycharm, webstorm]
---

# The space way

## Leader key

Using <kbd>space</kbd> key as the leader is a very popular way of editing, navigation and commanding. There is never an easy way to get used to new shortcuts, but trust me, you would definitely like it once you use it.

## Sticky key

Think about how you invoke commands in VSCode before. When you want to call the `command-palette`, you need to put your left hand's two fingers on <kbd>Ctrl + Shift</kbd> key or <kbd>Command + Shift</kbd> key and press <kbd>p</kbd>. And note that it's a key chord combination when you actually press these keys.

This looks so stupid when you compare it with just <kbd>Space Space</kbd> in Vim's normal or visual mode. And by saying <kbd>Space Space</kbd>, it's a sticky key bindings which means you just type <kbd>space</kbd> key twice in sequence. And you can just set your hands as the default typing position shown in this picture.

<!--more-->

![](https://ws2.sinaimg.cn/large/006tNc79gy1fm3jb9l72jj30r80i6ae1.jpg)

## Prefix key

Well, now you probably get the point of using <kbd>space</kbd> key. But there is more of it.

Since sticky keys are just key sequences, you can cluster a lot of similar commands to a prefix like <kbd>space f</kbd>(file related commands). For example, <kbd>space f f</kbd> go to the explorer, <kbd>space f s</kbd>save file and <kbd>space f S</kbd>save all. In this case, you won't mess up with these keys because they have the same prefix <kbd>space f</kbd>.

# The hybrid editing mode

## Insert mode

Spacemacs has a hybrid mode that takes the normal and visual modes' key bindings from Vim while still using the general Emacs key bindings in insert mode. To be honest, it's super smart way of editing.

The Unix key bindings (<kbd>C-a</kbd>->home, <kbd>C-e</kbd>->end, <kbd>C-b</kbd>->back, <kbd>C-f</kbd>->forward, <kbd>C-n</kbd>->next line, <kbd>C-p</kbd>->last line) work in almost every Mac application. You probably never find out they work out of box in your Mac or Linux, but many of your guys don't know about it.

So, why the hell people want to use Unix key bindings in their machines?

There are many reasons:

1.  Your Mac does not has the <kbd>home</kbd>, <kbd>end</kbd> key like a full keyboard.
2.  It's a much faster way for navigation once you get used to it
3.  Be more consistent about the key bindings. They work in terminal, intellij IDEA, even Wechat. So why not use it everywhere.

## Normal & visual mode

As for the normal and visual mode, They are pretty much the same. But they can do much more now in space way.

> Note: The leader key is <kbd>space</kbd>

| Key                        | Description                        |
| -------------------------- | ---------------------------------- |
| <kbd>leader space</kbd>    | show commands                      |
| <kbd>leader b b</kbd>      | quick open (see your opened files) |
| <kbd>leader f f</kbd>      | go the explorer                    |
| <kbd>leader f s</kbd>      | save file                          |
| <kbd>leader f S</kbd>      | save all                           |
| <kbd>leader =</kbd>        | beautify file                      |
| <kbd>leader w [lhjk]</kbd> | navigate window                    |
| <kbd>leader w v</kbd>      | split vertically                   |
| <kbd>C-g</kbd> (Optional)  | ESC                                |

# To use it

1.  Add the following configuration in your VSCode's `User Setting` (You can find out how to get to the `User Setting` [over here](https://code.visualstudio.com/docs/getstarted/settings)).

```json
{
  // Vim setting
  "vim.useSystemClipboard": true,
  "vim.easymotion": false,
  "vim.easymotionMarkerFontFamily":
    "Operator Mono Lig, Ubuntu Mono, Menlo, Monaco, 'Courier New', monospace",
  "vim.easymotionMarkerFontSize": "14",
  "vim.handleKeys": {
    "<C-n>": false,
    "<C-p>": false,
    "<C-a>": false,
    "<C-e>": false
  },
  "vim.leader": "<space>",
  "vim.insertModeKeyBindings": [
    {
      "before": ["<C-f>"],
      "after": ["<right>"]
    },
    {
      "before": ["<C-b>"],
      "after": ["<left>"]
    },
    {
      "before": ["<C-e>"],
      "commands": [
        {
          "command": "cursorEnd",
          "when": "editorTextFocus"
        }
      ]
    },
    {
      "before": ["<C-a>"],
      "commands": [
        {
          "command": "cursorHome",
          "when": "editorTextFocus"
        }
      ]
    },
    {
      "before": ["<C-d>"],
      "commands": [
        {
          "command": "deleteRight",
          "when": "editorTextFocus && !editorReadonly"
        }
      ]
    }
  ],
  "vim.normalModeKeyBindingsNonRecursive": [
    {
      "before": ["g", "r"],
      "commands": [
        {
          "command": "editor.action.referenceSearch.trigger",
          "when":
            "editorHasReferenceProvider && editorTextFocus && !inReferenceSearchEditor && !isInEmbeddedEditor"
        }
      ]
    },
    {
      "before": ["<C-a>"],
      "commands": [
        {
          "command": "cursorHome",
          "when": "editorTextFocus"
        }
      ]
    },
    {
      "before": ["<C-e>"],
      "commands": [
        {
          "command": "cursorEnd",
          "when": "editorTextFocus"
        }
      ]
    },
    {
      "before": ["<C-k>"],
      "after": ["D"]
    },
    {
      "before": ["<leader>", "<space>"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.showCommands",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "'"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.terminal.toggleTerminal",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "1"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.focusFirstEditorGroup",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "2"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.focusSecondEditorGroup",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "3"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.focusThirdEditorGroup",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "b", "b"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.quickOpen",
          "args": []
        }
      ]
    },
    {
      "before": ["<CR>"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.quickOpen",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "b", "d"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.closeActiveEditor",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "b", "n"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.nextEditor",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "b", "p"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.previousEditor",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "e", "l"],
      "after": [],
      "commands": [
        {
          "command": "workbench.actions.view.problems",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "f", "e"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.openGlobalSettings",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "f", "f"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.files.openFile",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "f", "r"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.openRecent",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "f", "s"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.files.save",
          "args": []
        }
      ]
    },
    // save file
    {
      "before": ["<leader>", "f", "S"],
      "commands": [
        {
          "command": "workbench.action.files.saveAll"
        }
      ]
    },
    {
      "before": ["<leader>", "f", "t"],
      "after": [],
      "commands": [
        {
          "command": "workbench.view.explorer",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "f", "y"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.files.copyPathOfActiveFile",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "g", "s"],
      "after": [],
      "commands": [
        {
          "command": "workbench.view.scm",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "j", "="],
      "after": [],
      "commands": [
        {
          "command": "editor.action.formatDocument",
          "args": []
        }
      ]
    },
    // beautify files
    {
      "before": ["<leader>", "="],
      "commands": [
        {
          "command": "editor.action.formatDocument"
        }
      ]
    },
    {
      "before": ["<leader>", "p", "f"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.quickOpen",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "p", "l"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.files.openFolder",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "p", "p"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.openRecent",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "q", "f"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.closeWindow",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "q", "r"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.reloadWindow",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "q", "q"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.closeWindow",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "s", "e"],
      "after": [],
      "commands": [
        {
          "command": "editor.action.rename",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "s", "j"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.gotoSymbol",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "s", "p"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.findInFiles",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "s", "P"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.findInFilesWithSelectedText",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "T", "F"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.toggleFullScreen",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "T", "m"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.toggleMenuBar",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "T", "s"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.selectTheme",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "T", "t"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.toggleActivityBarVisibility",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "v"],
      "after": [],
      "commands": [
        {
          "command": "editor.action.smartSelect.grow",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "V"],
      "after": [],
      "commands": [
        {
          "command": "editor.action.smartSelect.shrink",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "w", "w"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.focusNextGroup",
          "args": []
        }
      ]
    },
    // navigation
    {
      "before": ["leader", "w", "l"],
      "commands": [
        {
          "command": "extension.vim_navigateRight",
          "when": "vim.active && vim.use<C-w> && !editorTextFocus"
        }
      ]
    },
    {
      "before": ["leader", "w", "h"],
      "commands": [
        {
          "command": "extension.vim_navigateLeft",
          "when": "vim.active && vim.use<C-w> && !editorTextFocus"
        }
      ]
    },
    {
      "before": ["leader", "w", "j"],
      "commands": [
        {
          "command": "extension.vim_navigateDown",
          "when": "vim.active && vim.use<C-w> && !editorTextFocus"
        }
      ]
    },
    {
      "before": ["leader", "w", "k"],
      "commands": [
        {
          "command": "extension.vim_navigateUp",
          "when": "vim.active && vim.use<C-w> && !editorTextFocus"
        }
      ]
    },
    {
      "before": ["leader", "w", "v"],
      "commands": [
        {
          "command": "workbench.action.splitEditor",
          "key": "cmd+\\"
        }
      ]
    },
    {
      "before": ["<leader>", "w", "W"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.focusPreviousGroup",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "w", "m"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.maximizeEditor",
          "args": []
        }
      ]
    }
  ],
  "vim.visualModeKeyBindingsNonRecursive": [
    {
      "before": ["g", "r"],
      "commands": [
        {
          "command": "editor.action.referenceSearch.trigger",
          "when":
            "editorHasReferenceProvider && editorTextFocus && !inReferenceSearchEditor && !isInEmbeddedEditor"
        }
      ]
    },
    {
      "before": ["<backspace>"],
      "commands": [
        {
          "command": "deleteLeft",
          "when": "editorTextFocus && !editorReadonly"
        }
      ]
    },
    {
      "before": ["<C-a>"],
      "commands": [
        {
          "command": "cursorHome",
          "when": "editorTextFocus"
        }
      ]
    },
    {
      "before": ["<C-e>"],
      "commands": [
        {
          "command": "cursorEnd",
          "when": "editorTextFocus"
        }
      ]
    },
    {
      "before": ["<C-k>"],
      "after": ["D"]
    },
    {
      "before": ["<leader>", "<space>"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.showCommands",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "'"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.terminal.toggleTerminal",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "1"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.focusFirstEditorGroup",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "2"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.focusSecondEditorGroup",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "3"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.focusThirdEditorGroup",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "b", "b"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.quickOpen",
          "args": []
        }
      ]
    },
    {
      "before": ["<CR>"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.quickOpen",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "b", "d"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.closeActiveEditor",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "b", "n"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.nextEditor",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "b", "p"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.previousEditor",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "e", "l"],
      "after": [],
      "commands": [
        {
          "command": "workbench.actions.view.problems",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "f", "e"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.openGlobalSettings",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "f", "f"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.files.openFile",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "f", "r"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.openRecent",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "f", "s"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.files.save",
          "args": []
        }
      ]
    },
    // save file
    {
      "before": ["<leader>", "f", "S"],
      "commands": [
        {
          "command": "workbench.action.files.saveAll"
        }
      ]
    },
    {
      "before": ["<leader>", "f", "t"],
      "after": [],
      "commands": [
        {
          "command": "workbench.view.explorer",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "f", "y"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.files.copyPathOfActiveFile",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "g", "s"],
      "after": [],
      "commands": [
        {
          "command": "workbench.view.scm",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "j", "="],
      "after": [],
      "commands": [
        {
          "command": "editor.action.formatDocument",
          "args": []
        }
      ]
    },
    // beautify files
    {
      "before": ["<leader>", "="],
      "commands": [
        {
          "command": "editor.action.formatDocument"
        }
      ]
    },
    {
      "before": ["<leader>", "p", "f"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.quickOpen",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "p", "l"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.files.openFolder",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "p", "p"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.openRecent",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "q", "f"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.closeWindow",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "q", "r"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.reloadWindow",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "q", "q"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.closeWindow",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "s", "e"],
      "after": [],
      "commands": [
        {
          "command": "editor.action.rename",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "s", "j"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.gotoSymbol",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "s", "p"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.findInFiles",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "s", "P"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.findInFilesWithSelectedText",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "T", "F"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.toggleFullScreen",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "T", "m"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.toggleMenuBar",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "T", "s"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.selectTheme",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "T", "t"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.toggleActivityBarVisibility",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "v"],
      "after": [],
      "commands": [
        {
          "command": "editor.action.smartSelect.grow",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "V"],
      "after": [],
      "commands": [
        {
          "command": "editor.action.smartSelect.shrink",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "w", "w"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.focusNextGroup",
          "args": []
        }
      ]
    },
    // navigation
    {
      "before": ["leader", "w", "l"],
      "commands": [
        {
          "command": "extension.vim_navigateRight",
          "when": "vim.active && vim.use<C-w> && !editorTextFocus"
        }
      ]
    },
    {
      "before": ["leader", "w", "h"],
      "commands": [
        {
          "command": "extension.vim_navigateLeft",
          "when": "vim.active && vim.use<C-w> && !editorTextFocus"
        }
      ]
    },
    {
      "before": ["leader", "w", "j"],
      "commands": [
        {
          "command": "extension.vim_navigateDown",
          "when": "vim.active && vim.use<C-w> && !editorTextFocus"
        }
      ]
    },
    {
      "before": ["leader", "w", "k"],
      "commands": [
        {
          "command": "extension.vim_navigateUp",
          "when": "vim.active && vim.use<C-w> && !editorTextFocus"
        }
      ]
    },
    {
      "before": ["leader", "w", "v"],
      "commands": [
        {
          "command": "workbench.action.splitEditor",
          "key": "cmd+\\"
        }
      ]
    },
    {
      "before": ["<leader>", "w", "W"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.focusPreviousGroup",
          "args": []
        }
      ]
    },
    {
      "before": ["<leader>", "w", "m"],
      "after": [],
      "commands": [
        {
          "command": "workbench.action.maximizeEditor",
          "args": []
        }
      ]
    }
  ]
}
```

2.  Add the following to your VSCode's `keybindings.json`.

> Note: You can find your keybindings.json here.
> ![img](https://ws4.sinaimg.cn/large/006tKfTcgy1fm2fa491z3j30y40d275w.jpg)

```json
[
  // unbind "C-k .", needed to bind C-k as kill line
  {
    "command": "-extension.clipToHtml",
    "key": "ctrl+k .",
    "when": "editorTextFocus"
  },
  // (Optional) bind <C-g> as <ESC>
  {
    "key": "ctrl-g",
    "command": "extension.vim_escape",
    "when": "editorTextFocus && vim.active && !inDebugRepl"
  },
  {
    "command": "-workbench.action.gotoLine",
    "key": "ctrl+g"
  },
  {
    "command": "workbench.action.closeQuickOpen",
    "key": "ctrl-g",
    "when": "inQuickOpen"
  },
  {
    "command": "workbench.action.exitZenMode",
    "key": "ctrl-g ctrl-g",
    "when": "inZenMode"
  }
]
```
