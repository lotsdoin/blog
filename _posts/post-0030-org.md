---
title: Org
date: Sun Jul 30 19:09:16 CST 2017
---

Org
===

Install org additionally
------------------------

```lisp
(setq load-path (cons "~/path/to/orgdir/lisp" load-path))
(setq load-path (cons "~/path/to/orgdir/contrib/lisp" load-path))
```
wirte `require 'org-install` in `.emacs`, documents autoload with the startup
of emacs not autoload with org-mode startup.

### 激活


Add following lines in `.emacs`.
```lisp
;; The following lines are always needed. Choose your own keys.
(add-to-list 'auto-mode-alist '("\\.org\\'" . org-mode))
(add-hook 'org-mode-hook 'turn-on-font-lock) ; not needed when global-font-lock-mode is on
(global-set-key "\C-cl" 'org-store-link)
(global-set-key "\C-ca" 'org-agenda)
(global-set-key "\C-cb" 'org-iswitchb)
```
open `*.org` emacs will go to `org-mode`.

文档结构
--------

``` elisp
* Top level headline
** Second level
*** 3rd level
    some text
*** 3rd level
    more text

* Another top level headline
```

