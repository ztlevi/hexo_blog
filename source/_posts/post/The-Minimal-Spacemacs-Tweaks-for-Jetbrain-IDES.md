---
title: The Minimal Spacemacs Tweaks for Jetbrain IDEs
date: 2017-12-05 01:45:50
categories: post
tags: [spacemacs, jetbrain, space, intellij idea, pycharm, webstorm]
---

# Another Spacemacs configuration for Jetbrain IDEs

Recently, I'm working on a React Native project. I have tried using Emacs to do the coding, but I cannot really pick up the whole new stuff without a fancy auto-completion or finding definitions since the syntax of React is so different and special. That's why I pick up Webstorm as a workaround. And there, I find a way to build my Jetbrain IDEs just like Spacemacs.

Like I said in my previous post, space way is good for Vim users and only Vim can do this because it has other modes other than just insert mode. In this case, key bindings will never be a problem. We are using the sticky key sequences and prefix key for memorization.

Welcome to the heaven!!!

<img src="https://tctechcrunch2011.files.wordpress.com/2015/08/safe_image.gif" alt="" style="width:500px;margin:auto;display:block;"/>

<!--more-->

> I am just quoting myself here
# The space way
## Leader key
Using `<space>` key as the leader is a very popular way of editing, navigation, and commanding. There is never an easy way to get used to new shortcuts, but trust me, you would definitely like it once you use it.

## Sticky key
Think about how you invoke commands in VSCode before. When you want to call the `command-palette`, you need to put your left hand's two fingers on `Ctrl + Shift` key or `Command + Shift` key and press `p`. And note that it's a key chord combination when you actually press these keys.

This looks so stupid when you compare it with just `Space Space` in Vim's normal or visual mode. And by saying `Space Space`, it's a sticky key binding which means you just type `<space>` key twice in sequence. And you can just set your hands as the default typing position shown in this picture.


<img src="https://ws2.sinaimg.cn/large/006tNc79gy1fm3jb9l72jj30r80i6ae1.jpg" alt="" style="width:500px;margin:auto;display:block;"/>

## Prefix key

Well, now you probably get the point of using `<space>` key. But there is more of it.

Since sticky keys are just key sequences, you can cluster a lot of similar commands to a prefix like `<space> f` (file related commands). For example, `<space> f f` go to the explorer, `<space> f s` save file and `<space> f S` save all. In this case, you won't mess up with these keys because they have the same prefix `<space> f`.

# Keybindings

For the normal and visual mode, They are pretty much the same. But they can do much more now in space way.

The `<space> w m` and other window pop up combination is just beautiful.

The most used ones are in bold text.

> Note: The leader key is `<space>`

| Key                 | Description                                                                  |
| ------------------- | ----------------------------------                                           |
| `<leader>` space    | **Go to Action**                                                             |
| `<leader>` b b      | **Recent files** (You can still use `command+e` or `ctrl+e`)                 |
| `<leader>` b i      | **Active structure tool window**                                             |
| `<leader>` b p      | Fire structure pop up (similar to structure tool)                            |
| `<leader>` b u      | Reopen Closed Tab                                                            |
| `<leader>` f f      | Go to file                                                                   |
| `<leader>` f t      | **Active file tree window**                                                  |
| `<leader>` f d      | Dash Launcher (You have to install Dash first)                               |
| `<leader>` f s      | save all files (I still use `command+s` or `ctrl+s`)                         |
| `<leader>` d d      | **Debug**                                                                    |
| `<leader>` d D      | Debug Class                                                                  |
| `<leader>` t t      | **Toggle Line Breakpoint**                                                                 |
| `<leader>` r r      | **Run**                                                                      |
| `<leader>` r R      | Run Class                                                                    |
| `<leader>` s p      | **Search in project**                                                        |
| `<leader>` r p      | **Replace in project**                                                       |
| `<leader>` R        | reload `~/.ideavimrc`                                                        |
| `<leader>` '        | Active terminal window                                                       |
| `<leader>` ee       | show error description                                                       |
| `<leader>` c c      | Go to Class                                                                  |
| `<leader>` a l      | show the action list                                                         |
| `<leader>` g s      | **Vsc quick list pop up**                                                    |
| `<leader>` g S      | Active version control window                                                |
| `<leader>` w [lhjk] | **navigate window**                                                          |
| `<leader>` w v      | **split window vertically**                                                  |
| `<leader>` w s      | split window horizontally                                                    |
| `<leader>` w c      | close window                                                                 |
| `<leader>` w m      | **hide all windows except the editor tabs** (You can invoke again to revert) |
| C-o                 | Go back                                                                      |
| C-i                 | Forward                                                                      |
| g d                 | **Go to declaration**                                                        |
| g h                 | Go to Documentation                                                          |
| g s                 | Go to Symbol                                                                 |
| , =                 | **beautify file**                                                            |
| z c                 | **collapse region**                                                          |
| z o                 | **expand region**                                                            |
| z C                 | collapse all region                                                          |
| z O                 | expand all region                                                            |

# Install
1. Install ideaVim and create a `.ideavimrc` file in home directory, just like `~/.ideavimrc`.

  > In case you want to sync your settings across multiple machines, you should checkout the **Setting Repository** [here](https://www.jetbrains.com/help/idea/sharing-your-ide-settings.html#settings-repository).

2. If you want to use the Emacs key in Vim's insert mode, which is the hybrid mode in Spacemacs, copy the following script to `~/.ideavimrc`.

  ```
  " ============================================================================
  " emacs keymaping for cursor movement{{{
  " You have to unbind C-g before it works
  " ============================================================================
  nmap <c-g> <Esc>
  vmap <c-g> <Esc>
  imap <c-g> <Esc>a
  nmap <c-a> ^
  nmap <c-e> $
  vmap <c-a> ^
  vmap <c-e> $
  imap <c-e> <Esc>A
  imap <c-a> <Esc>I
  imap <c-d> <del>
  inoremap <c-p> <up>
  inoremap <c-n> <down>
  " command line
  cnoremap <C-a> <Home>
  cnoremap <C-e> <End>
  "}}}
  ```

  Note: You have to disable the `C-a`, `C-e` in Jetbrain IDE to have the visual mode working correctly.

  You can click the from here to find the action by key.

  ![](https://ws1.sinaimg.cn/large/006tKfTcgy1fm6eh3f8mgj31hg0fk42l.jpg)

3. To bind the actions under `<space>`, put the following script in the `~/.ideavimrc`.

  The ugly `<Backspace><Backspace><Backspace><Backspace><Backspace>` is because when we enter the command mode from visual mode, we have `:'<,'>`. The extra chars need to be deleted before we invoke the actions.

  ```
  let mapleader = " "

  " ============================================================================
  " key bindings for quickly moving between windows
  " h left, l right, k up, j down
  " ============================================================================
  nmap <leader>wh <c-w>h
  nmap <leader>wl <c-w>l
  nmap <leader>wk <c-w>k
  nmap <leader>wj <c-w>j
  nmap <leader>wv <c-w>v
  nmap <leader>ws <c-w>s
  nmap <leader>wc <c-w>c
  nmap <leader>wm :action HideAllWindows<CR>

  vmap <leader>wh <c-w>h
  vmap <leader>wl <c-w>l
  vmap <leader>wk <c-w>k
  vmap <leader>wj <c-w>j
  vmap <leader>wv <c-w>v
  vmap <leader>ws <c-w>s
  vmap <leader>wc <c-w>c
  vmap <leader>wm :<Backspace><Backspace><Backspace><Backspace><Backspace>action HideAllWindows<CR>

  " ============================================================================
  " expand and collapse
  " ============================================================================
  nmap zO :action ExpandAllRegions<CR>
  nmap zo :action ExpandRegion<CR>
  nmap zc :action CollapseRegion<CR>
  nmap zC :action CollapseAllRegions<CR>

  " ============================================================================
  " IDE actions
  " ============================================================================

  nmap <leader><Space> :action GotoAction<CR>
  nmap <leader>cc      :action GotoClass<CR>
  nmap <leader>ff      :action GotoFile<CR>
  nmap <leader>ft      :action ActivateProjectToolWindow<CR>
  nmap <leader>fs      :action SaveAll<CR>
  nmap <leader>fd      :action DashLauncherAction<CR>
  nmap <leader>bb      :action RecentFiles<CR>
  nmap <leader>bi      :action ActivateStructureToolWindow<CR>
  nmap <leader>bp      :action FileStructurePopup<cr>
  nmap <leader>bu      :action ReopenClosedTab<CR>
  nmap <leader>dd      :action Debug<CR>
  nmap <leader>dD      :action DebugClass<CR>
  nmap <leader>tt      :action ToggleLineBreakpoint<CR>
  nmap <leader>rr      :action Run<CR>
  nmap <leader>rR      :action RunClass<CR>
  nmap <leader>im      :action ImplementMethods<CR>
  nmap <leader>ee      :action ShowErrorDescription<cr>
  nmap <leader>'       :action ActivateTerminalToolWindow<CR>
  nmap gd              :action GotoDeclaration<cr>
  nmap gh              :action QuickJavaDoc<CR>
  nmap gs              :action GotoSymbol<cr>
  nmap ,=              :action ReformatCode<CR>
  nmap <c-o>           :action Back<cr>
  nmap <c-i>           :action Forward<cr>

  vmap <leader><Space> :<Backspace><Backspace><Backspace><Backspace><Backspace>action GotoAction<CR>
  vmap <leader>cc      :<Backspace><Backspace><Backspace><Backspace><Backspace>action GotoClass<CR>
  vmap <leader>ff      :<Backspace><Backspace><Backspace><Backspace><Backspace>action GotoFile<CR>
  vmap <leader>ft      :<Backspace><Backspace><Backspace><Backspace><Backspace>action ActivateProjectToolWindow<CR>
  vmap <leader>fs      :<Backspace><Backspace><Backspace><Backspace><Backspace>actio SaveAll<CR>
  vmap <leader>fd      :<Backspace><Backspace><Backspace><Backspace><Backspace>action DashLauncherAction<CR>
  vmap <leader>bb      :<Backspace><Backspace><Backspace><Backspace><Backspace>action RecentFiles<CR>
  vmap <leader>bu      :<Backspace><Backspace><Backspace><Backspace><Backspace>action ReopenClosedTab<CR>
  vmap <leader>bi      :<Backspace><Backspace><Backspace><Backspace><Backspace>action ActivateStructureToolWindow<CR>
  vmap <leader>bp      :<Backspace><Backspace><Backspace><Backspace><Backspace>action FileStructurePopup<cr>
  vmap <leader>dd      :<Backspace><Backspace><Backspace><Backspace><Backspace>action Debug<CR>
  vmap <leader>dD      :<Backspace><Backspace><Backspace><Backspace><Backspace>action DebugClass<CR>
  vmap <leader>tt      :<Backspace><Backspace><Backspace><Backspace><Backspace>action ToggleLineBreakpoint<CR>
  vmap <leader>rr      :<Backspace><Backspace><Backspace><Backspace><Backspace>action Run<CR>
  vmap <leader>rR      :<Backspace><Backspace><Backspace><Backspace><Backspace>action RunClass<CR>
  vmap <leader>im      :<Backspace><Backspace><Backspace><Backspace><Backspace>action ImplementMethods<CR>
  vmap <leader>ee      :<Backspace><Backspace><Backspace><Backspace><Backspace>action ShowErrorDescription<cr>
  vmap <leader>'       :<Backspace><Backspace><Backspace><Backspace><Backspace>action ActivateTerminalToolWindow<CR>
  vmap ,=              :<Backspace><Backspace><Backspace><Backspace><Backspace>action ReformatCode<CR>
  vmap <c-o>           :<Backspace><Backspace><Backspace><Backspace><Backspace>action Back<cr>
  vmap <c-i>           :<Backspace><Backspace><Backspace><Backspace><Backspace>action Forward<cr>

  " Enter the command-line mode
  nmap <CR> :
  vmap <CR> :

  " Reload .ideavimrc
  nmap <leader>R :source ~/.ideavimrc<CR>
  vmap <leader>R :<Backspace><Backspace><Backspace><Backspace><Backspace>source ~/.ideavimrc<CR>

  " check the action list
  nmap <leader>al :actionlist<CR>
  vmap <leader>al :a<Backspace><Backspace><Backspace><Backspace><Backspace>ctionlist<CR>

  " git
  nmap <leader>gs :action Vcs.QuickListPopupAction<CR>
  vmap <leader>gs :<Backspace><Backspace><Backspace><Backspace><Backspace>action Vcs.QuickListPopupAction<CR>
  nmap <leader>gS :action ActivateVersionControlToolWindow<CR>
  vmap <leader>gS :<Backspace><Backspace><Backspace><Backspace><Backspace>action ActivateVersionControlToolWindow<CR>

  " search in project
  nmap <leader>sp :action FindInPath<CR>
  vmap <leader>sp :<Backspace><Backspace><Backspace><Backspace><Backspace>action FindInPath<CR>

  " replace in project
  nmap <leader>rp :action ReplaceInPath<CR>
  vmap <leader>rp :<Backspace><Backspace><Backspace><Backspace><Backspace>action FindInPath<CR>
  ```

4. The multi-cursor action does not work correctly as well as the extend region and shrink region. They mess up some visual selection in Vim and the original selection. That's the reason. But so far I cannot do anything. So I just put the script here in case they work later on.

  ```
  " select occurrence, they do not work when editing
  nmap mn :action SelectNextOccurrence<CR>
  nmap mp :action UnselectPreviousOccurrence<CR>
  nmap ma :action SelectAllOccurrences<CR>
  vmap mn :<Backspace><Backspace><Backspace><Backspace><Backspace>action SelectNextOccurrence<CR>
  vmap mp :<Backspace><Backspace><Backspace><Backspace><Backspace>action UnselectPreviousOccurrence<CR>
  vmap ma :<Backspace><Backspace><Backspace><Backspace><Backspace>action SelectAllOccurrences<CR>
  ```

5. There are other options you might want to add.

  ```
  set gdefault
  set smartcase

  " Integrate with system clipboard
  set clipboard=unnamedplus,unnamed

  set surround
  ```
