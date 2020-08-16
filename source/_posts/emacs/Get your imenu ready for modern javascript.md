---
title: Get your imenu ready for modern Javascript
date: 2017-12-29
tags: [emacs, imenu]
categories: emacs
---

# Introduction

These days, I was working on a React Native project. In the meanwhile, I found it's kind of hard to catch up the modern
syntax of Javascript, so as for imenu (a built in project structure menu bar in Emacs).

Fortunately, there are so many people love Emacs and contribute to it. Thanks for Chen bin's great
[post](http://blog.binchen.org/posts/why-emacs-is-better-editor-part-two.html). I just put down more imenu generic
expressions for modern Javascript like React, Vue. This helps me navigate and go through projects.

<!--more-->

# Screenshot

A quick look a the result is here.

![](https://ws1.sinaimg.cn/large/006tKfTcgy1fmy5k692izj31co1bwwpm.jpg)

# Set up

> Note: To get functions like `componentDidMount`, and exclude `if, for, while`, plain regexp in Emacs seems not
> working. At least I couldn't find an easy solution like `[^if|for|while]`. But since `imenu-generic-expression` takes
> functions as parameters, I created another function to wrap one generic expression. Finally it works but as you can
> see, it's not beautiful.

```emacs-lisp
(defun my-js2-mode-hook ()
  (progn
    (setq imenu-create-index-function 'js2-imenu-make-index)))

(add-hook 'js2-mode-hook 'my-js2-mode-hook)

;; this imenu generic expression aims to exclude for, while, if when aims to match functions in
;; es6 js, e.g. ComponentDidMount(), render() function in React
;; https://emacs-china.org/t/topic/4538/7
(defun js-exception-imenu-generic-expression-regexp ()
  ;; (async)? xxx (e) { }
  (if (re-search-backward "^[ \t]*\\(async\\)?[ \t]*\\([A-Za-z_$][A-Za-z0-9_$]+\\)[ \t]*([a-zA-Z0-9, ]*) *\{ *$" nil t)
      (progn
        (if (member (match-string 2) '("for" "if" "while" "switch"))
            (js-exception-imenu-generic-expression-regexp)
          t))
    nil))

(defun js2-imenu-make-index ()
  (interactive)
  (save-excursion
    ;; (setq imenu-generic-expression '((nil "describe\\(\"\\(.+\\)\"" 1)))
    (imenu--generic-function '(("describe" "\\s-*describe\\s-*(\\s-*[\"']\\(.+\\)[\"']\\s-*,.*" 1)
                               ("it" "\\s-*it\\s-*(\\s-*[\"']\\(.+\\)[\"']\\s-*,.*" 1)
                               ("test" "\\s-*test\\s-*(\\s-*[\"']\\(.+\\)[\"']\\s-*,.*" 1)
                               ("before" "\\s-*before\\s-*(\\s-*[\"']\\(.+\\)[\"']\\s-*,.*" 1)
                               ("after" "\\s-*after\\s-*(\\s-*[\"']\\(.+\\)[\"']\\s-*,.*" 1)
                               ("Controller" "[. \t]controller([ \t]*['\"]\\([^'\"]+\\)" 1)
                               ("Controller" "[. \t]controllerAs:[ \t]*['\"]\\([^'\"]+\\)" 1)
                               ("Filter" "[. \t]filter([ \t]*['\"]\\([^'\"]+\\)" 1)
                               ("State" "[. \t]state([ \t]*['\"]\\([^'\"]+\\)" 1)
                               ("Factory" "[. \t]factory([ \t]*['\"]\\([^'\"]+\\)" 1)
                               ("Service" "[. \t]service([ \t]*['\"]\\([^'\"]+\\)" 1)
                               ("Module" "[. \t]module([ \t]*['\"]\\([a-zA-Z0-9_\.]+\\)" 1)
                               ("ngRoute" "[. \t]when(\\(['\"][a-zA-Z0-9_\/]+['\"]\\)" 1)
                               ("Directive" "[. \t]directive([ \t]*['\"]\\([^'\"]+\\)" 1)
                               ("Event" "[. \t]\$on([ \t]*['\"]\\([^'\"]+\\)" 1)
                               ("Config" "[. \t]config([ \t]*function *( *\\([^\)]+\\)" 1)
                               ("Config" "[. \t]config([ \t]*\\[ *['\"]\\([^'\"]+\\)" 1)
                               ("OnChange" "[ \t]*\$(['\"]\\([^'\"]*\\)['\"]).*\.change *( *" 1)
                               ("OnClick" "[ \t]*\$([ \t]*['\"]\\([^'\"]*\\)['\"]).*\.click *( *" 1)
                               ("Watch" "[. \t]\$watch( *['\"]\\([^'\"]+\\)" 1)

                               ("Class" "^[ \t]*[0-9a-zA-Z_$ ]*[ \t]*class[ \t]*\\([a-zA-Z_$.]*\\)" 1)
                               ("Class" "^[ \t]*\\(var\\|let\\|const\\)[ \t]*\\([0-9a-zA-Z_$.]+\\)[ \t]*=[ \t]*[a-zA-Z_$.]*.extend" 2)
                               ("Class" "^[ \t]*cc\.\\(.+\\)[ \t]*=[ \t]*cc\..+\.extend" 1)

                               ("Function" "\\(async\\)?[ \t]*function[ \t]+\\([a-zA-Z0-9_$.]+\\)[ \t]*(" 2) ;; (async)? function xxx (
                               ("Function" "^[ \t]*\\([a-zA-Z0-9_$.]+\\)[ \t]*:[ \t]*\\(async\\)?[ \t]*function[ \t]*(" 1) ;; xxx : (async)? function (
                               ("Function" "^[ \t]*\\(export\\)?[ \t]*\\(var\\|let\\|const\\)?[ \t]*\\([a-zA-Z0-9_$.]+\\)[ \t]*=[ \t]*\\(async\\)?[ \t]*function[ \t]*(" 3) ;; (export)? (var|let|const)? xxx = (async)? function (

                               ;; {{ es6 beginning
                               ("Function" js-exception-imenu-generic-expression-regexp 2) ;; (async)? xxx (e) { }
                               ("Function" "^[ \t]*\\([A-Za-z_$][A-Za-z0-9_$.]*\\)[ \t]*:[ \t]*\\(async\\)?[ \t]*(" 1) ;; xxx : (async)? (
                               ("Function" "^[ \t]*\\(export\\)?[ \t]*\\(var\\|let\\|const\\)?[ \t]*\\([A-Za-z_$][A-Za-z0-9_$.]*\\)[ \t]*=[ \t]*\\(async\\)?[ \t]*(" 3) ;; (export)? (var|let|const)? xxx = (async)? (
                               ("Function" "^[ \t]*\\(export\\)?[ \t]*\\(var\\|let\\|const\\)?[ \t]*\\([A-Za-z_$][A-Za-z0-9_$.]*\\)[ \t]*=[ \t]*\\(async\\)?[ \t]*[A-Za-z_$][A-Za-z0-9_$.]*[ \t]*=>" 3) ;; (export)? (var|let|const)? xxx = (async)? e =>
                               ;; }}

                               ("Task" "[. \t]task([ \t]*['\"]\\([^'\"]+\\)" 1)))))
```
