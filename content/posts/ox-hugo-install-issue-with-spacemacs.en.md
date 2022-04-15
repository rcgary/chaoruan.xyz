+++
title = "ox-hugo Install Issue with Spacemacs"
date = 2019-10-23T18:42:00+11:00
lastmod = 2022-04-15T15:24:12+10:00
tags = ["emacs", "org"]
categories = ["programming"]
draft = false
weight = 2003
+++

While I try to install [ox-hugo](https://ox-hugo.scripter.co/) on my [Spacemacs](http://spacemacs.org/), I found an issue:

<!--more-->

After reading the install and [usage guide](https://ox-hugo.scripter.co/#usage). I added `ox-hugo`
to `dotspacemacs-additional-packages` and also did this:

```emacs-lisp
(defun dotspacemacs/user-config ()
  ;; Other stuff
  ;; ..

  ;; ox-hugo config
  (use-package ox-hugo
    :ensure t          ;Auto-install the package from Melpa (optional)
    :after ox))
```

**Everything works fine until I restart emacs**:

`ox-hugo` been marked as **an orphan package** and got removed first then
reinstalled back immediately.

By searching and digging around the Spacemacs documentation, I found the
Spacemacs `org layer` already has [org-hugo support by default](http://develop.spacemacs.org/layers/+emacs/org/README.html#hugo-support) (`development`
branch only). So we **don't need to follow** the [ox-hugo](https://ox-hugo.scripter.co/) usage guide.
we can do this in `.spacemacs`

```emacs-lisp
(setq-default
 dotspacemacs-configuration-layers
 '((org :variables
        org-enable-hugo-support t)))
```

Orphan package and reinstall issue should be fixed now.
