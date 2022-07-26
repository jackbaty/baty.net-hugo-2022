+++
title = "Searching Org-roam files"
date = 2022-04-21T06:16:00-04:00
lastmod = 2022-04-28T14:59:03-04:00
slug = "searching-org-roam-files"
categories = ["Emacs"]
draft = false
weight = 0
+++

[Org-roam](https://www.orgroam.com/) is "A plain-text personal knowledge management system" using Emacs and Org-mode and I put nearly all my notes in there. While it's easy to find notes in org-roam based on filename, there's no obvious way to search the _contents_ of notes. Weird, right?

<!--more-->

I could use the default `projectile` search, but my org-roam files live within my main ~/org directory, so the results are littered with all my other org documents. I'd prefer to only search in `~/org/roam`

I use a simple lisp function to help with this. It uses `consult-ripgrep`:

```emacs-lisp
(defun jab/search-roam ()
 "Run consult-ripgrep on the org roam directory"
 (interactive)
 (consult-ripgrep org-roam-directory nil))
```

I added a keybinding for it to my other org-roam bindings:

```emacs-lisp
(map!
 "\C-c n f" 'org-roam-node-find
 "s-u" 'org-roam-node-find
 "\C-c n i" 'org-roam-node-insert
 "\C-c n t" 'org-roam-dailies-goto-today
 "\C-c n d" 'org-roam-dailies-capture-today
 "\C-c n c" 'org-roam-capture
 "\C-c n s" 'jab/search-roam               ;; <-- my new keybinding
 "\C-c n l" 'org-roam-buffer-toggle)
```

Now, with a quick `C-s n s` I can search my org-roam files using the blazingly fast [ripgrep](https://github.com/BurntSushi/ripgrep).

If there's a better way to do this, I'm all ears.

[//]: # "Exported with love from a post written in Org mode"
[//]: # "- https://github.com/kaushalmodi/ox-hugo"
