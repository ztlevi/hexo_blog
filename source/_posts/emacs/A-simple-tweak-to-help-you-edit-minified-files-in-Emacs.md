---
title: A simple tweak to help you edit minified files in Emacs
categories: emacs
tags: emacs
date: 2018-07-01 23:51:13
---

Emacs "stucks" at editing long line files. It does but that's not Emacs's fault. Emacs has excellent [gap buffer](chrome-extension://gfbliohnnapiefjpjlpjnehglfpaknnc/pages/pdf_viewer.html?r=https://www.common-lisp.net/project/flexichain/download/StrandhVilleneuveMoore.pdf) for large file editing. It's due to the mode you apply to the file. These modes might freeze your Emacs when editing large file or minified files.

## Check Minified files

So here is a simple trick, I just check the first line of the opened file. If first line is over 500 in width, then it just enable `fundamental-mode` which works perfectly for these files.

```emacs-lisp
;; if the first line is too long, enable fundamental by default
(defun get-nth-line-length (n)
  "Length of the Nth line."
  (save-excursion
    (goto-char (point-min))
    (if (zerop (forward-line (1- n)))
        (- (line-end-position)
           (line-beginning-position)))))
(defun check-if-first-line-too-long ()
  (> (get-nth-line-length 1) 500))
(add-to-list 'magic-mode-alist (cons #'check-if-first-line-too-long 'fundamental-mode))
```

<!--more-->

## Check Large File

This piece of code is from spacemacs, we have to set a couple variables. But you could have your own version.

```emacs-lisp
(setq spacemacs-large-file-modes-list '(archive-mode tar-mode jka-compr git-commit-mode image-mode
                 doc-view-mode doc-view-mode-maybe ebrowse-tree-mode
                 pdf-view-mode))

(setq dotspacemacs-large-file-size 1)

;; check when opening large files - literal file open
(defun spacemacs/check-large-file ()
  (let* ((filename (buffer-file-name))
         (size (nth 7 (file-attributes filename))))
    (when (and
           (not (memq major-mode spacemacs-large-file-modes-list))
           size (> size (* 1024 1024 dotspacemacs-large-file-size))
           (y-or-n-p (format (concat "%s is a large file, open literally to "
                                     "avoid performance issues?")
                             filename)))
      (setq buffer-read-only t)
      (buffer-disable-undo)
      (fundamental-mode))))

;; Prompt to open file literally if large file.
(add-hook 'find-file-hook 'spacemacs/check-large-file)
```
