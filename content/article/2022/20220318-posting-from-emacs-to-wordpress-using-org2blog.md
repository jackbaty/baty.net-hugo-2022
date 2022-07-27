---
title: Posting from Emacs to WordPress using Org2Blog
author: Jack
date: 2022-03-18T10:57:00+00:00
url: /2022/posting-from-emacs-to-wordpress-using-org2blog/
categories:
  - Misc
tags:
  - Blogging
  - Emacs
  - Org mode

---
 

I’ve settled on WordPress for this blog. (“settled” is a fluid word for me, but let’s assume I mean it for now). However, I prefer to do most of my writing in Emacs and Org mode. To help with this, I’ve configured [org2blog][1] and I’m writing this post with it.

I’m using org2blog pretty much right out of the box. Just a single blog configuration with the following tweaks:

```emacs-lisp
<div class="org-src-container"><pre id="nil" class="src src-emacs-lisp"><span style="color: #4078f2;">(</span><span style="color: #e45649;">setq</span> <span style="color: #6a1868;">org2blog/wp-track-posts</span> <span style="color: #a626a4;">(</span><span style="color: #b751b6;">list</span> <span style="color: #50a14f;">"~/org/baty.net/.org2blog.org"</span> <span style="color: #50a14f;">"wordpress"</span><span style="color: #a626a4;">)</span><span style="color: #4078f2;">)</span>
<span style="color: #4078f2;">(</span><span style="color: #e45649;">setq</span> <span style="color: #6a1868;">org2blog/wp-default-categories</span> <span style="color: #4078f2;">'</span><span style="color: #a626a4;">(</span><span style="color: #50a14f;">"Misc"</span><span style="color: #a626a4;">)</span><span style="color: #4078f2;">)</span>
<span style="color: #4078f2;">(</span><span style="color: #e45649;">setq</span> <span style="color: #6a1868;">org2blog/wp-default-tags</span> <span style="color: #4078f2;">'</span><span style="color: #a626a4;">(</span><span style="color: #50a14f;">""</span><span style="color: #a626a4;">)</span><span style="color: #4078f2;">)</span>
<span style="color: #4078f2;">(</span><span style="color: #e45649;">setq</span> <span style="color: #6a1868;">org2blog/wp-show-post-in-browser</span> <span style="color: #4078f2;">'</span><span style="color: #986801;">ask</span><span style="color: #4078f2;">)</span></pre></div></code></pre>
```


I haven’t figured out how to use authinfo.gpg for logging in automatically yet, so for now I’m typing my password in each new emacs session.

There’s a nice “which-key”-like UI for everything.<figure class="wp-block-image">

![_20220318_082434org2blogUI.png][2] </figure> 

It’s been years since I’ve done this. It seems to have gotten quite capable. I’ve yet to exercise things but so far, so good.

If you’re reading this, everything worked.

One downside is that this workflow suffers from some of the same issues as static blogs. Specifically, if I’m reading a post and find something I’d like to edit, instead of just hitting the “Edit” button, I need to go find the post in Emacs, make the change, and re-publish. We’ll see if I hate it. Maybe I’ll use Emacs for initial drafts and first edits and then simply live in the WordPress editor for future edits.

 [1]: https://github.com/org2blog/org2blog
 [2]: https://baty.net/wp-content/uploads/2022/03/20220318_082434org2blogUI-1.png