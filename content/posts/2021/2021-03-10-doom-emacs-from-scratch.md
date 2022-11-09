---
title: Doom Emacs from scratch
author: Jack
date: 2021-03-10T15:38:32+00:00
url: /2021/doom-emacs-from-scratch/
featuredImage: /wp-content/uploads/2021/03/doom.png
categories:
  - Misc
tags:
  - Doom
  - Editor
  - Emacs
  - Tech

---
<!--kg-card-begin: html-->A week ago I decided to cancel 

[Doom Emacs][1] and go back to building [Emacs from Scratch][2], and once again I was reminded what a terrible idea that is.

Seriously, stock Emacs, even with a leg up from [Nano Emacs][3], gets so many things &#8220;wrong&#8221; that I could spend the rest of my life fixing things and still wanting more. I thought building from scratch would help me _avoid_ [Configuration Fatigue][4]. Wow, was I wrong.

So, back to Doom. I started from scratch with the usual&#8230;

<pre class="wp-block-code"><code>git clone --depth 1 https://github.com/hlissner/doom-emacs ~/.emacs.d~/.emacs.d/bin/doom install</code></pre>

Then I edited init.el and enabled just a few non-stock things. &#8220;Zen&#8221; mode, org-journal, and pandoc-mode. Otherwise, it&#8217;s right out of the box.

I copied the gotta-haves from my original config.el. Most of these are around file paths, Org mode, and LaTeX. Plus a few of my favorite key bindings. Otherwise, I left it alone. So far.

Doom Emacs is simply too good to pass up. It handles all of the little behavioral and visual tweaks that would otherwise take forever to learn about and modify on my own. Half of the things it does for me I just expect to be part of Emacs, and am surprised when I find they&#8217;re not.

I&#8217;m still using the default Doom theme, which isn&#8217;t my favorite, but I&#8217;m trying to resist farting around with that for at least a couple of days while I get settled back in.

<!--kg-card-end: html-->

 [1]: https://github.com/hlissner/doom-emacs
 [2]: https://www.baty.blog/2021/emacs-from-scratch-again
 [3]: https://github.com/rougier/nano-emacs
 [4]: https://www.baty.blog/2021/configuration-fatigue