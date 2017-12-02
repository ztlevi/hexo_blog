---
title: The Minimal Spacemacs Tweeks for VSCode
date: 2017-12-02 00:35:26
categories: coding
tags: vscode, spacemacs
---

# The space way
Using `<space>` key as the leader is a very popular way of editing, navigation and commanding. There is never an easy way to get used to new shortcuts, but trust me, you would definitely like it once you use it.

# The hybrid editing mode
## Insert mode
Spacemacs has a hybrid mode that takes the normal and visual modes' key bindings from Vim while still using the general Emacs key bindings in insert mode. To be honest, it's super smart way of editing.

The Unix key bindings (`<C-a>`->home, `<C-e>`->end, `<C-b>`->back, `<C-f>`->forward, `<C-n>`->next line, `<C-p>`->last line) work in almost every Mac application. You probably never find out they work out of box in your Mac or Linux, but many of your guys don't know about it.

So, why the hell people want to use Unix key bindings in their machines?

There are many reasons:

1. Your Mac does not has the `<home>`, `<end>` key like a full keyboard.
2. It's a much faster way for navigation once you get used to it
3. Be more consistent about the key bindings. They work in terminal, intellij IDEA, even Wechat. So why not use it everywhere.

## Normal & visual mode
As for the normal and visual mode, They are pretty much the same. But they can do much more now in space way.

> Note: The leader key is `<space>`

| Key                 | Description                        |
|---------------------|------------------------------------|
| `<leader>` space    | show commands                      |
| `<leader>` b b      | quick open (see your opened files) |
| `<leader>` f f      | go the explorer                    |
| `<leader>` =        | beautify file                      |
| `<leader>` w [lhjk] | navigate window                    |
| `<leader>` w v      | split vertically                   |
| C-g (Optional)      | ESC                                |

# To use it
1. Add the following configuration in your VSCode's `User Setting` (You can find out how to get to the `User Setting` [over here](https://code.visualstudio.com/docs/getstarted/settings)).

```json
{
  "": [{
      "before": ["<C-f>"],
      "after": ["<right>"]
    },
    {
      "before": ["<C-b>"],
      "after": ["<left>"]
    },
    {
      "before": ["<C-n>"],
      "after": ["<down>"]
    },
    {
      "before": ["<C-p>"],
      "after": ["<up"]
    },
    {
      "before": ["<C-e>"],
      "commands": [{
        "command": "cursorEnd",
        "when": "editorTextFocus"
      }]
    },
    {
      "before": ["<C-a>"],
      "commands": [{
        "command": "cursorHome",
        "when": "editorTextFocus"
      }]
    },
    {
      "before": ["<C-d>"],
      "commands": [{
        "command": "deleteRight",
        "when": "editorTextFocus && !editorReadonly"
      }]
    }
  ],
  "vim.otherModesKeyBindingsNonRecursive": [
  // comment out if you don't want to use <C-a> <C-e> in normal or visual mode
    {
      "before": ["<C-a>"],
      "commands": [{
        "command": "cursorHome",
        "when": "editorTextFocus"
      }]
    },
    {
      "before": ["<C-e>"],
      "commands": [{
        "command": "cursorEnd",
        "when": "editorTextFocus"
      }]
    },
    {
      "before": ["<C-k>"],
      "after": ["D"]
    },
    // ivy buffer
    {
      "before": ["<leader>", "b", "b"],
      "commands": [{
        "command": "workbench.action.quickOpen"
      }]
    },
    // M-x
    {
      "before": ["<leader>", " "],
      "commands": [{
        "command": "workbench.action.showCommands"
      }]
    },
    // go to last tab
    {
      "before": ["<leader>", "<tab>"],
      "commands": [{
        "command": "workbench.action.navigateLast"
      }]
    },
    // go to explorer
    {
      "before": ["<leader>", "f", "f"],
      "commands": [{
        "command": "workbench.view.explorer"
      }]
    },
    // beautify files
    {
      "before": ["<leader>", "="],
      "commands": [{
        "command": "HookyQR.beautifyFile"
      }]
    },
    // navigation
    {
      "before": ["leader", "w", "l"],
      "commands": [{
        "command": "extension.vim_navigateRight",
        "when": "vim.active && vim.use<C-w> && !editorTextFocus"
      }]
    },
    {
      "before": ["leader", "w", "h"],
      "commands": [{
        "command": "extension.vim_navigateLeft",
        "when": "vim.active && vim.use<C-w> && !editorTextFocus"
      }]
    },
    {
      "before": ["leader", "w", "j"],
      "commands": [{
        "command": "extension.vim_navigateDown",
        "when": "vim.active && vim.use<C-w> && !editorTextFocus"
      }]
    },
    {
      "before": ["leader", "w", "k"],
      "commands": [{
        "command": "extension.vim_navigateUp",
        "when": "vim.active && vim.use<C-w> && !editorTextFocus"
      }]
    },
    {
      "before": ["leader", "w", "v"],
      "commands": [{
        "command": "workbench.action.splitEditor",
        "key": "cmd+\\"
      }]
    }
  ],
  "vim.leader": "<space>"
}
```

2. Add the following to your VSCode's `keybindings.json`.

> Note: You can find your keybindings.json here.
![img](https://ws4.sinaimg.cn/large/006tKfTcgy1fm2fa491z3j30y40d275w.jpg)

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
