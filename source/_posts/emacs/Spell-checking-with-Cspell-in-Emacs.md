---
title: Spell checking with Cspell in Emacs
categories: emacs
tags: emacs
date: 2018-11-05 23:46:18
---

`cspell` is a command line tool and librray for spell checking code. It supports camel case checking
and is really popular in VSCode, roughly 1,350,000 downloads so far.

As for Emacs, there are many options there but none of them seems working perfectly for me. But I
have to say they are powerful tools.Besides [wucuo]() is kind of cool tool as well because it
supports camel case as well.

I found this `cspell` and it works great in VSCode and I decide to move this to Emacs. A tricky
thing is it a plain checker and doesn't help to provide correction candidates for you, but flyspell
does. So it better just add a `flycheck-checker` rather hack on `Flyspell`.

Here is the code:

```emacs-lisp
(with-eval-after-load 'flycheck
  (flycheck-define-checker cspell
    "Cspell checker supports camel case checking"
    :command ("cspell"
              "--config" (eval (substitute-in-file-name "$HOME/.cspell.json"))
              source-inplace)
    :error-patterns
    ((info line-start (file-name) ":" line ":" column " - "
           (message)
           line-end))
    :modes (c-mode c++-mode js2-mode rjsx-mode java-mode go-mode))
  (add-to-list 'flycheck-checkers 'cspell))
```

> **Note**: If you feel lagging, you can set `flycheck-idle-change-delay` to 3s or remove
> `idle-change` from `flycheck-check-syntax-automatically`.

Furthurmore, you can customize it with [cspell.json](https://github.com/Jason3S/cspell#cspelljson)
