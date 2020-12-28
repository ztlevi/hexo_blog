---
title: Spacemacs/Space-Vim Config for Jetbrain IDEs
date: 2018-6-11 15:00:00
categories: post
tags:
  - spacemacs
  - space-vim
  - jetbrain
  - intellij idea
  - pycharm
  - webstorm
---

# Another Spacemacs configuration for Jetbrain IDEs

Recently, I'm working on a React Native project. I have tried using Emacs to do the coding, but I
cannot really pick up the whole new stuff without a fancy auto-completion or finding definitions
since the syntax of React is so different and special. That's why I pick up Webstorm as a
workaround. And there, I find a way to build my Jetbrain IDEs just like Spacemacs.

Like I said in my previous post, space way is good for Vim users and only Vim can do this because it
has other modes other than just insert mode. In this case, key bindings will never be a problem. We
are using the sticky key sequences and prefix key for memorization.

Welcome to the heaven!!!

<img src="https://tctechcrunch2011.files.wordpress.com/2015/08/safe_image.gif" alt="" style="width:500px;margin:auto;display:block;"/>

<!--more-->

> If you're too lazy to read the whole stuff, grab my
> [.ideavimrc](https://github.com/ztlevi/Dotfiles/blob/master/ideavimrc) on Github

# The space way

## Leader key

Using <kbd>space</kbd> key as the leader is a very popular way of editing, navigation, and
commanding. There is never an easy way to get used to new shortcuts, but trust me, you would
definitely like it once you use it.

## Sticky key

Think about how you invoke commands in VSCode before. When you want to call the `command-palette`,
you need to put your left hand's two fingers on <kbd>Ctrl + Shift</kbd> key or <kbd>Command +
Shift</kbd> key and press <kbd>p</kbd>. And note that it's a key chord combination when you actually
press these keys.

This looks so stupid when you compare it with just <kbd>Space Space</kbd> in Vim's normal or visual
mode. And by saying <kbd>Space Space</kbd>, it's a sticky key binding which means you just type
<kbd>space</kbd> key twice in sequence. And you can just set your hands as the default typing
position shown in this picture.

<img src="https://ws2.sinaimg.cn/large/006tNc79gy1fm3jb9l72jj30r80i6ae1.jpg" alt="" style="width:500px;margin:auto;display:block;"/>

## Prefix key

Well, now you probably get the point of using <kbd>space</kbd> key. But there is more of it.

Since sticky keys are just key sequences, you can cluster a lot of similar commands to a prefix like
<kbd>space f</kbd> (file related commands). For example, <kbd>space> f f</kbd> go to the explorer,
<kbd>space> f s</kbd> save file and <kbd>space> f S</kbd> save all. In this case, you won't mess up
with these keys because they have the same prefix <kbd>space> f</kbd>.

# Keybindings

For the normal and visual mode, They are pretty much the same. But they can do much more now in
space way.

The <kbd>space w m</kbd> and other window pop up combination is just beautiful.

The most used ones are in bold text.

<kbd><space> f t</kbd> is very helpful when you want to navigate to the file you're currently
viewing in the project view.

> Note: The leader key is <kbd>space</kbd>

| Key                                       | Description                                                                    |
| ----------------------------------------- | ------------------------------------------------------------------------------ |
| <kbd>C-i</kbd>                            | Forward                                                                        |
| <kbd>C-o</kbd>                            | Go back                                                                        |
| <kbd>g d</kbd>                            | **Go to declaration**                                                          |
| <kbd>g h</kbd>                            | Go to Documentation                                                            |
| <kbd>g r</kbd>                            | **Find Usages**                                                                |
| <kbd>g s</kbd>                            | Go to Symbol                                                                   |
| <kbd>leader '</kbd>                       | Active terminal window                                                         |
| <kbd>leader R</kbd>                       | reload `~/.ideavimrc`                                                          |
| <kbd>leader a a</kbd>                     | Select All                                                                     |
| <kbd>leader a l</kbd>                     | Prompt action list                                                             |
| <kbd>leader b b</kbd> (<kbd>\<CR\></kbd>) | **Recent files** (You can still use <kbd>command+e</kbd> or <kbd>ctrl+e</kbd>) |
| <kbd>leader b i</kbd>                     | **Active structure tool window**                                               |
| <kbd>leader b u</kbd>                     | Reopen Closed Tab                                                              |
| <kbd>leader c c</kbd>                     | Go to Class                                                                    |
| <kbd>leader d D</kbd>                     | Debug Class                                                                    |
| <kbd>leader d d</kbd>                     | **Debug**                                                                      |
| <kbd>leader e e</kbd>                     | show error description                                                         |
| <kbd>leader f T</kbd>                     | **Select current file in project view**                                        |
| <kbd>leader f b</kbd>                     | **Show Bookmarks**                                                             |
| <kbd>leader f d</kbd>                     | Smart search launcher (You have to install Dash or Zeal first)                 |
| <kbd>leader f f</kbd>                     | **Search Everywhere**                                                          |
| <kbd>leader f s</kbd>                     | save all files (I still use <kbd>command+s</kbd> or <kbd>ctrl+s</kbd>)         |
| <kbd>leader f t</kbd>                     | **Active file tree window**                                                    |
| <kbd>leader i m</kbd>                     | Implement Methods                                                              |
| <kbd>leader g S<kbd>/                     | Active version control window                                                  |
| <kbd>leader g s</kbd>                     | **Vsc quick list pop up**                                                      |
| <kbd>leader j i</kbd>                     | Fire structure pop up (similar to structure tool)                              |
| <kbd>leader j j</kbd>                     | Ace Action                                                                     |
| <kbd>leader j l</kbd>                     | Ace Line Action                                                                |
| <kbd>leader m =</kbd>                     | **beautify file**                                                              |
| <kbd>leader r R</kbd>                     | Run Class                                                                      |
| <kbd>leader r p</kbd>                     | **Replace in project**                                                         |
| <kbd>leader r r</kbd>                     | **Run**                                                                        |
| <kbd>leader s s</kbd>                     | **Stop**                                                                       |
| <kbd>leader s p</kbd>                     | **Search in project**                                                          |
| <kbd>leader space</kbd>                   | **Go to Action**                                                               |
| <kbd>leader t b</kbd>                     | Toggle Bookmark                                                                |
| <kbd>leader t t</kbd>                     | **Toggle Line Breakpoint**                                                     |
| <kbd>leader w [lhjk]</kbd>                | **navigate window**                                                            |
| <kbd>leader w c</kbd>                     | close window                                                                   |
| <kbd>leader w m</kbd>                     | **hide all windows except the editor tabs** (You can invoke again to revert)   |
| <kbd>leader w s</kbd>                     | split window horizontally                                                      |
| <kbd>leader w v</kbd>                     | **split window vertically**                                                    |
| <kbd>leader w z</kbd>                     | Toggle Zen mode                                                                |
| <kbd>z C</kbd>                            | collapse all region                                                            |
| <kbd>z O</kbd>                            | expand all region                                                              |
| <kbd>z c</kbd>                            | **collapse region**                                                            |
| <kbd>z o</kbd>                            | **expand region**                                                              |

# Install

1.  Install ideaVim and create a `.ideavimrc` file in home directory, just like `~/.ideavimrc`.

> In case you want to sync your settings across multiple machines, you should checkout the **Setting
> Repository** >
> [here](https://www.jetbrains.com/help/idea/sharing-your-ide-settings.html#settings-repository).

2.  If you want to use the Emacs key in Vim's insert mode, which is the hybrid mode in Spacemacs,
    copy the following script to `~/.ideavimrc`.

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

Note: You have to disable the <kbd>C-a</kbd>, <kbd>C-e</kbd> in Jetbrain IDE to have the visual mode
working correctly.

You can click the from here to find the action by key.

![](https://ws1.sinaimg.cn/large/006tKfTcgy1fm6eh3f8mgj31hg0fk42l.jpg)

3.  To bind the actions under <kbd>space</kbd>, put the following script in the `~/.ideavimrc`.

The ugly `<Backspace><Backspace><Backspace><Backspace><Backspace>` is because when we enter the
command mode from visual mode, we have `:'<,'>`. The extra chars need to be deleted before we invoke
the actions.

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
nmap <leader>wz :action ToggleDistractionFreeMode<CR>

vmap <leader>wh <c-w>h
vmap <leader>wl <c-w>l
vmap <leader>wk <c-w>k
vmap <leader>wj <c-w>j
vmap <leader>wv <c-w>v
vmap <leader>ws <c-w>s
vmap <leader>wc <c-w>c
vmap <leader>wm :<Backspace><Backspace><Backspace><Backspace><Backspace>action HideAllWindows<CR>
vmap <leader>wz :<Backspace><Backspace><Backspace><Backspace><Backspace>action ToggleDistractionFreeMode<CR>

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

nmap <CR>            :action RecentFiles<CR>
nmap <c-i>           :action Forward<CR>
nmap <c-o>           :action Back<CR>
nmap <leader>'       :action ActivateTerminalToolWindow<CR>
nmap <leader><Space> :action GotoAction<CR>
nmap <leader><tab>   :action RecentFiles<CR>
nmap <leader>aa      :action $SelectAll<CR>
nmap <leader>al      :actionlist<CR>
nmap <leader>bb      :action RecentFiles<CR>
nmap <leader>bi      :action ActivateStructureToolWindow<CR>
nmap <leader>bu      :action ReopenClosedTab<CR>
nmap <leader>cc      :action GotoClass<CR>
nmap <leader>dD      :action DebugClass<CR>
nmap <leader>dd      :action Debug<CR>
nmap <leader>ee      :action ShowErrorDescription<CR>
nmap <leader>fT      :action SelectInProjectView<CR>
nmap <leader>fb      :action ShowBookmarks<CR>
nmap <leader>fd      :action SmartSearchAction<CR>
nmap <leader>ff      :action SearchEverywhere<CR>
nmap <leader>fs      :action SaveAll<CR>
nmap <leader>ft      :action ActivateProjectToolWindow<CR>
nmap <leader>im      :action ImplementMethods<CR>
nmap <leader>ji      :action FileStructurePopup<CR>
nmap <leader>jj      :action AceAction<CR>
nmap <leader>jl      :action AceLineAction<CR>
nmap <leader>m=      :action ReformatCode<CR>
nmap <leader>rR      :action RunClass<CR>
nmap <leader>rr      :action Run<CR>
nmap <leader>ss      :action Stop<CR>
nmap <leader>tb      :action ToggleBookmark<CR>
nmap <leader>tt      :action ToggleLineBreakpoint<CR>
nmap gd              :action GotoDeclaration<CR>
nmap gh              :action QuickJavaDoc<CR>
nmap gr              :action FindUsages<CR>
nmap gs              :action GotoSymbol<CR>

vmap <CR>            :<Backspace><Backspace><Backspace><Backspace><Backspace>action RecentFiles<CR>
vmap <c-i>           :<Backspace><Backspace><Backspace><Backspace><Backspace>action Forward<CR>
vmap <c-o>           :<Backspace><Backspace><Backspace><Backspace><Backspace>action Back<CR>
vmap <leader>'       :<Backspace><Backspace><Backspace><Backspace><Backspace>action ActivateTerminalToolWindow<CR>
vmap <leader><Space> :<Backspace><Backspace><Backspace><Backspace><Backspace>action GotoAction<CR>
vmap <leader><tab>   :<Backspace><Backspace><Backspace><Backspace><Backspace>action RecentFiles<CR>
vmap <leader>aa      :<Backspace><Backspace><Backspace><Backspace><Backspace>action $SelectAll<CR>
vmap <leader>al      :<Backspace><Backspace><Backspace><Backspace><Backspace>actionlist<CR>
vmap <leader>bb      :<Backspace><Backspace><Backspace><Backspace><Backspace>action RecentFiles<CR>
vmap <leader>bi      :<Backspace><Backspace><Backspace><Backspace><Backspace>action ActivateStructureToolWindow<CR>
vmap <leader>bu      :<Backspace><Backspace><Backspace><Backspace><Backspace>action ReopenClosedTab<CR>
vmap <leader>cc      :<Backspace><Backspace><Backspace><Backspace><Backspace>action GotoClass<CR>
vmap <leader>dD      :<Backspace><Backspace><Backspace><Backspace><Backspace>action DebugClass<CR>
vmap <leader>dd      :<Backspace><Backspace><Backspace><Backspace><Backspace>action Debug<CR>
vmap <leader>ee      :<Backspace><Backspace><Backspace><Backspace><Backspace>action ShowErrorDescription<CR>
vmap <leader>fT      :<Backspace><Backspace><Backspace><Backspace><Backspace>action SelectInProjectView<CR>
vmap <leader>fb      :<Backspace><Backspace><Backspace><Backspace><Backspace>action ShowBookmarks<CR>
vmap <leader>fd      :<Backspace><Backspace><Backspace><Backspace><Backspace>action SmartSearchAction<CR>
vmap <leader>ff      :<Backspace><Backspace><Backspace><Backspace><Backspace>action SearchEverywhere<CR>
vmap <leader>fs      :<Backspace><Backspace><Backspace><Backspace><Backspace>action SaveAll<CR>
vmap <leader>ft      :<Backspace><Backspace><Backspace><Backspace><Backspace>:action ActivateProjectToolWindow<CR>
vmap <leader>im      :<Backspace><Backspace><Backspace><Backspace><Backspace>action ImplementMethods<CR>
vmap <leader>ji      :<Backspace><Backspace><Backspace><Backspace><Backspace>action FileStructurePopup<CR>
vmap <leader>m=      :<Backspace><Backspace><Backspace><Backspace><Backspace>action ReformatCode<CR>
vmap <leader>rR      :<Backspace><Backspace><Backspace><Backspace><Backspace>action RunClass<CR>
vmap <leader>rr      :<Backspace><Backspace><Backspace><Backspace><Backspace>action Run<CR>
vmap <leader>ss      :<Backspace><Backspace><Backspace><Backspace><Backspace>action Stop<CR>
vmap <leader>tb      :<Backspace><Backspace><Backspace><Backspace><Backspace>action ToggleBookmark<CR>
vmap <leader>tt      :<Backspace><Backspace><Backspace><Backspace><Backspace>action ToggleLineBreakpoint<CR>
vmap gd              :<Backspace><Backspace><Backspace><Backspace><Backspace>action GotoDeclaration<CR>
vmap gr              :<Backspace><Backspace><Backspace><Backspace><Backspace>action FindUsages<CR>

" tab is used in karabiner as <C-i>, <C-d> as delete
nmap <tab>           :action Forward<CR>
nmap <delete>        <C-d>
vmap <tab>           :<Backspace><Backspace><Backspace><Backspace><Backspace>action Forward<CR>
vmap <delete>        <C-d>

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

4.  The multi-cursor action does not work correctly as well as the extend region and shrink region.
    They mess up some visual selection in Vim and the original selection. That's the reason. But so
    far I cannot do anything. So I just put the script here in case they work later on.

```
" select occurrence, they do not work when editing
nmap mn :action SelectNextOccurrence<CR>
nmap mp :action UnselectPreviousOccurrence<CR>
nmap ma :action SelectAllOccurrences<CR>
vmap mn :<Backspace><Backspace><Backspace><Backspace><Backspace>action SelectNextOccurrence<CR>
vmap mp :<Backspace><Backspace><Backspace><Backspace><Backspace>action UnselectPreviousOccurrence<CR>
vmap ma :<Backspace><Backspace><Backspace><Backspace><Backspace>action SelectAllOccurrences<CR>
```

5.  There are other options you might want to add.

```
set gdefault
set smartcase


" use system clipboard
set clipboard=unnamedplus,unnamed

set surround

" Allow backspace and cursor keys to cross line boundaries
set whichwrap+=<,>,h,l

" black hole register
vmap <backspace> "_d
vmap <del> "_d
```
