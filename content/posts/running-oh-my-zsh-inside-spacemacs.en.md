+++
title = "Running Oh-My-Zsh inside Spacemacs"
date = 2019-10-26T10:58:00+11:00
lastmod = 2022-04-15T15:23:49+10:00
tags = ["emacs", "zsh"]
categories = ["programming"]
draft = false
weight = 2002
+++

When I start using [Spacemacs](http://spacemacs.org/), I was hoping there is a way to using my own configured [zsh](https://ohmyz.sh/)
inside the Spacemacs workflow, after a look through the documentation, of
course we can do it

<!--more-->

First, we need to let Spacemacs load zsh when it setup `shell`, and I found
you can do a pop-up buffer style with 30% of the current height from the
bottom.

So in `.spacemacs` we can set this in `dotspacemacs-configure-layers`:

```emacs-lisp
(shell :variables
       shell-default-term-shell "/bin/zsh" ;; find your zsh path using `$ whereis zsh`
       shell-default-height 30
       shell-default-position 'bottom)
```

This change is the basic setup, **but since I enabled `vi` key bindings in my
zsh, it starts conflicts with Spacemacs [evil-mode](https://github.com/emacs-evil/evil).** after a play around with different
settings, I found the best option for me is to disable the evil-mode inside
[ansi-term](https://www.emacswiki.org/emacs/AnsiTerm).

Add following code in `dotspacemacs/user-config`:

```emacs-lisp
(evil-set-initial-state 'term-mode 'emacs)
```

This change allows us navigation in ansi-term, but we can not editing
anything in the input line. We need to do **one more change**:

```emacs-lisp
(evil-set-initial-state 'term-mode 'emacs) ;; turn off evil-mode for ansi-term
(setq term-char-mode-point-at-process-mark nil) ;; allow editing in normal mode
```

After `SPC f e R`, we can now using zsh inside Spacemacs


## Reference {#reference}

-   [syl20bnr/spacemacs#8642 Cannot edit shell commands in normal mode.](https://github.com/syl20bnr/spacemacs/issues/8642)
-   [spacemacs/layers/+tools/shell at develop · syl20bnr/spacemacs · GitHub](https://github.com/syl20bnr/spacemacs/tree/develop/layers/+tools/shell)
