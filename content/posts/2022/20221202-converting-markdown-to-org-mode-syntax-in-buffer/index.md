---
title: "Converting Markdown to Org-mode syntax in current buffer"
date: 2022-12-02T12:48:00-05:00
lastmod: 2022-12-02T12:55:42-05:00
slug: "converting-markdown-to-org-mode-syntax-in-buffer"
categories: ["Emacs"]
draft: false
weight: 0
---

There are some great tools for bringing web content into Markdown files, but few that offer the same utility for Org-mode ([Orgdown](https://gitlab.com/publicvoit/orgdown)) files.

For example, I use Markdownload extension all the time. It works great with nearly every site I use it on, but instead of Markdown, I'd prefer having Org syntax, so I've worked around it by creating a function which converts the current region from Markdown to Org.

```emacs-lisp
(defun jab/md-to-org-region (start end)
  "Convert region from markdown to org, replacing selection"
  (interactive "r")
  (shell-command-on-region start end "pandoc -f markdown -t org" t t))
```

I copy the Markdown from the Markdownload window, paste it into an Org buffer, and run the function. It's not perfect, but until someone creates an "Orgdownload" extension, it'll do. (Pretty please, will someone create an Orgdownload extension?)


[//]: # "Exported with love from a post written in Org mode"
[//]: # "- https://github.com/kaushalmodi/ox-hugo"