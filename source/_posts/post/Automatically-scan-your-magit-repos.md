---
title: Automatically scan your magit repos
date: 2019-02-24 12:04:43
categories:
tags: git
---

`projectile` is amazing. It helps people to quickly switch between projects. Unfortunatelly, it
cannot automatically scan the projects on your machine and load them when you first time fire
projectile.

Also, it doesn't really remove those invalid project entires for me. For example, there is a git
projcet under `~/Developer/dummy-git` and I move this projcet to `~/Developer/new-git`. Both entires
will exists every time I trigger `M-x counsel-projectile-switch-project` (or helm-projectile). It
makes me confused sometimes.

Here is the solution. For me, basically I every project I created is by git. So I utilzed the
`magit-list-repos-1` func in `magit`. For those of you use other source control tool or
`.projectile` in your project, you might need to find the corresponding func or write your own.

<!--more-->

```emacs-lisp
(defun append-to-list (list-var elements)
  "Append ELEMENTS to the end of LIST-VAR.

The return value is the new value of LIST-VAR."
  (unless (consp elements)
    (error "ELEMENTS must be a list"))
  (let ((list (symbol-value list-var)))
    (if list
        (setcdr (last list) elements)
      (set list-var elements)))
  (symbol-value list-var))

(with-eval-after-load 'magit
  ;; define magit root directory with depth 2
  (setq magit-repository-directories '(("~/Developer" . 2))))

(with-eval-after-load 'projectile
  ;; Add personal repo root to scan git projects
  (defvar +my/repo-root-list '("~" "~/Dropbox"))

 (defun update-projectile-known-projects ()
    (interactive)
    (require 'magit)
    (let (magit-repos
          magit-abs-repos
          (home (expand-file-name "~")))
      ;; append magit repos at root with depth 1
      (dolist (root +my/repo-root-list)
        (setq magit-abs-repos (append magit-abs-repos (magit-list-repos-1 root 1))))
      (setq magit-abs-repos (append magit-abs-repos (magit-list-repos)))

      ;; convert abs path to relative path (HOME)
      (dolist (repo magit-abs-repos)
        (setq repo (concat repo "/"))
        (string-match home repo)
        (push (replace-match "~" nil nil repo 0) magit-repos))
      (setq projectile-known-projects magit-repos)))

  ;; set projectile-known-projects after magit
  (with-eval-after-load 'magit
    (update-projectile-known-projects))
  )
```

Since loading `magit` takes me roughly 1.5 seconds on my machine and I don't really need to update
projectile repos on booting Emacs, I hook the update func after `magit`. And I bind a key for
`update-projectile-known-projects` to manually trigger it if needed.

Thats all for this post. I hope you enjoy it.
