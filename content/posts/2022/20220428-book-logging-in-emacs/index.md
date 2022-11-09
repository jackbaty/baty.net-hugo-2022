+++
title = "Book logging in Emacs"
date = 2022-04-28T14:55:00-04:00
lastmod = 2022-05-03T10:10:11-04:00
slug = "book-logging-in-emacs"
tags = ["OrgMode"]
categories = ["Emacs"]
draft = false
weight = 0
+++

I've kept a list of books I've read as a plain text (well, technically, Markdown) file for years. I wrote about it [here](/2021/book-logging-in-plain-text-2/). The public version is rendered using Github Pages at [books.baty.net](https://books.baty.net).  This is fine, but at some point last year I also started logging books in an Org mode file, just to see how it felt. It felt pretty good!

<!--more-->

My books.org file is just an outline with some custom properties. An entry looks like this:

```org
** DONE Leonardo da Vinci
CLOSED: [2022-04-11 Mon 11:10]
:PROPERTIES:
:author:  Walter Isaacson
:year:    2017
:name:    Leonardo da Vinci
:url:     https://www.goodreads.com/book/show/34684622-leonardo-da-vinci
:pages:   600
:rating:  *****
:END:
```

The outline looks like this:

{{< figure src="Outline.png" caption="" >}}

That's fine, but doesn't show much information other than a short title. That's where Org's [Column View](https://orgmode.org/manual/Column-attributes.html) comes in. Column view shows a summary of a set of headings in a customizable view. The setup for mine is this:

`#+columns: %50ITEM(Title) %author(Author) %pages(Pages){+} %8rating`

This sets columns, widths, titles, and even a total of the number of pages (via the `{+}` flag). Then, I have a block which generates and saves the column view for me. Here's that block.

```org
#+BEGIN: columnview :hlines 1 :id global :skip-empty-rows t :indent t :match "-noexport"
#+END
```

Pressing `C-c C-c` on that block header generates a nice table view of my book attributes. Here's what the file looks like, including the column block:

{{< figure src="BooksDotOrg.png" caption=" My books.org file" >}}

I like it. It's like a little plain-text database.

I probably won’t bother backfilling it with earlier entries, but I plan to keep it updated from now on. I haven’t yet created any fancy org-mode “Capture templates” because let’s be honest, I don’t finish enough books to benefit from that kind of automation. I simply copy and paste an earlier entry and modify that. Maybe I’ll do something smarter at some point, just for fun.

Org mode is pretty great and can do just about anything.

[//]: # "Exported with love from a post written in Org mode"
[//]: # "- https://github.com/kaushalmodi/ox-hugo"
