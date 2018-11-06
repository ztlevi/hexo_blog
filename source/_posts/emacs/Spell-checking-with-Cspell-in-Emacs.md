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
  ;; disable mode-enabled for flycheck due to performance issue
  (setq flycheck-check-syntax-automatically '(save idle-change)
        flycheck-idle-change-delay 3)

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

I disable the `mode-enabled` in `flycheck-check-syntax-automatically` due to the performance issue.
The problem is every time I enable `evil-normal-mode`, it will check the buffer as well. It should
only check when `flychek-mode` is enabled. And it feels lagging and I couldn't find a hack for this.

So the temporarily solution is disable `mode-enabled` and set `flycheck-idle-change-delay` to 3s. In
this case, spelling check should work without much lag.

Furthurmore, you can customize it with [cspell.json](https://github.com/Jason3S/cspell#cspelljson)
