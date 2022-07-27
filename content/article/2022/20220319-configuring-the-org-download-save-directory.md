---
title: Configuring the org-download save directory
author: Jack
date: 2022-03-19T11:04:00+00:00
excerpt: Doom Emacs was stepping on my configuration for org-download. This is how I fixed it.
url: /2022/configuring-the-org-download-save-directory/
wabi_accentColor:
  - is-primary-accent
categories:
  - Software
tags:
  - Emacs

---
When I drag and drop an image into Emacs, I want the attached file to end up in `./img/YYYY/`. This is how I tried configuring [org-download][1] in my setup (I use Doom Emacs):



```emacs-lisp
(setq org-download-method 'directory
        org-download-image-dir (concat "img/"  (format-time-string "%Y") "/")
        org-download-image-org-width 600
        org-download-heading-lvl 1)
```
        
        
For some reason, `org-download-method` was being reset from `'directory` to `'attach` after loading, and this broke things. I thought maybe I needed to set the variables _after_ org-download was loaded, so I did this:

```emacs-lisp
(after! org-download
  (setq org-download-method 'directory
        org-download-image-dir (concat "img/"  (format-time-string "%Y") "/")
        org-download-image-org-width 600
        org-download-heading-lvl 1))
```

That didn’t work. At startup I was seeing this error:

<blockquote class="wp-block-quote">
  <p>
    Error (org-mode-hook): Error running hook “org-fancy-priorities-mode” because: (void-variable org-download-image-dir)
  </p>
</blockquote>

Huh. I guess not everything can be set after org-download, so I tried only setting `org-download-method`

```emacs-lisp
(after! org-download
  (setq org-download-method 'directory))
```


This worked. The other settings are done in the `(after! org` block.

It feels like I have to fight Doom too often, but the details and refinement of Doom is worth the trouble.

 [1]: https://github.com/abo-abo/org-download