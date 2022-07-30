---
title: "Searching this site using Pagefind"
date: 2022-07-30T07:50:35-04:00
draft: false

categories: ["Blogging"]
tags: ["Webdev"]
toc: false
author: ""
---

I was made aware of [Pagefind](https://pagefind.app/) via a [post by Bryce Wray](https://www.brycewray.com/posts/2022/07/pagefind-quite-find-site-search/).

Page find is...

> Pagefind is a fully static search library that aims to perform well on large sites, while using as little of your users’ bandwidth as possible, and without hosting any infrastructure.
>
> [Pagefind.app](https://pagefind.app)

<!--more-->

They had me at "...without hosting any infrastructure". The [theme I used to use](https://hugoloveit.com) included a nice search using [Lunr](https://lunrjs.com). [My new theme](https://github.com/Lednerb/bilberry-hugo-theme) uses Algolia, which I don't love because it involves a separate, commercial service and requires rebuilding and pushing an updated index to the Algolia service every time I post something.

As an alternative to Algolia, I thought I'd try [Pagefind](https://pagefind.app/). Turns out it's quite good and very easy to implement. Here's a quick summary of what I did to add Pagefind search here at baty.net.

First, I created a search page at [/search/](/search/). The search form looks like this:

```
<link href="/_pagefind/pagefind-ui.css" rel="stylesheet">
<script src="/_pagefind/pagefind-ui.js" type="text/javascript"></script>
<div id="search"></div>
<script>
    window.addEventListener('DOMContentLoaded', (event) => {
        new PagefindUI({ element: "#search", 
        showImages: false,
        });
    });
</script>
```

The only change there from the default is the addition of `showImages: false;`. This is a new option which disables image thumbnails on the search results. I found it much faster to leave images out.

Then, to build the index, I run the following:

`npx pagefind --source "public"`

Pagefind publishes a wrapper package through npm, so running the above takes care of everything, no installation required. Eventually I'll run it via a local binary. Since Pagefind is built using Rust, it's just a single binary with no other dependencies. I love not having dependencies.

And that's all I needed to have search up and running on my site.

However, I noticed that it was indexing _everything_, including the home page, tag listing, category pages, etc. This was too much, so I needed to add `data-pagefind-body` to the "article-wrapper" div, like so... `<div class="article-wrapper u-cf single" data-pagefind-body>`. Here's what that does (from the docs):

> If `data-pagefind-body` is found anywhere on your site, any pages without this attribute will be removed from your index. This means that if you tag your blog post layout with `data-pagefind-body`, other pages like your homepage will no longer appear in search results. This is usually what you want — if not, just add `data-pagefind-body` there as well.
> 
> [Pagefind docs](https://pagefind.app/docs/indexing/)

That made the results much cleaner.

All that remained was to make sure the index was updated when publishing. I don't use any fancy CI business for publishing. I use `rsync` to copy the /public folder up to my server.

I simply added the `npx` command to my Makefile, which now looks like this:

``` Makefile
SERVER_HOST=server01.baty.net
SERVER_DIR=/home/jbaty/apps/baty.net/public_html
PUBLIC_DIR=/Users/jbaty/sites/blog/public/
TARGET=server01.baty.net

.POSIX:
.PHONY: build checkpoint deploy


build:
	rm -rf $PUBLIC_DIR
	hugo --gc --minify
	npx -y pagefind --source public
	
checkpoint:
	git add .
	git diff-index --quiet HEAD || git commit -m "Publish checkpoint"

deploy: build checkpoint
	git push
	@echo "\033[0;32mDeploying updates to $(TARGET)...\033[0m"
	rsync -v -rz --checksum --delete --no-perms $(PUBLIC_DIR) $(SERVER_HOST):$(SERVER_DIR)
```

For my blog, it takes less than half a second to generate the necessary indexes:

```
Running Pagefind v0.5.3
Running from: "/Users/jbaty/sites/blog"
Source:       "public"
Bundle Directory:  "_pagefind"
Walking source directory...
Building search indexes...
Found a data-pagefind-body element on the site.
↳ Ignoring pages without this tag.
Indexed 291 pages
Indexed 5405 words
Indexed 0 filters
Created 5 index chunks
Finished in 0.430 seconds
```

So far this works swimmingly. [Try it yourself](/search/) and [let me know](mailto://jack@baty.net) if you have any issues.
