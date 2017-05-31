---
title: Emacs
date: 2017-05-20
---

Emacs
=====

```lisp
(package-initialize)
;;close the bell
(setq visible-bell t)
;;close the bar
(tool-bar-mode -1)
;;close the scroll-bar
(scroll-bar-mode -1)
;;open the line-number
(global-linum-mode t)
;;close the welcome mode
(setq inhibit-splash-mode t)
;;open init fast use F1
(defun open-my-init-file()
  (interactive)
  (find-file "~/.emacs.d/init.el"))
(global-set-key (kbd "<f1>") 'open-my-init-file)
;;open the recentf-mode
(recentf-mode t)
;;company you should install first
;;(global-company-mode t)
;;change the type of the cursor
(setq-default cursor-type 'bar)
;;no backup
(setq make-backup-files nil)

(delete-selection-mode t)

(require 'org)
(setq org-src-fontify-natively t)

(require 'recentf)
;;open the recentf-mode
(recentf-mode t)
(setq recentf-max-menu-items 15)
(global-set-key "\C-x\ \C-r" 'recentf-open-files)

(setq initial-frame-alist (quote ((fullscreen . maximized))))
(global-hl-line-mode t)
(add-hook 'emacs-lisp-mode-hook 'show-paren-mode)
```

