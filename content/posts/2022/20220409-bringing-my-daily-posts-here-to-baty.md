---
title: "Bringing my Daily posts here to baty.net"
date: 2022-04-09T11:48:00-04:00
lastmod: 2022-04-09T12:12:19-04:00
slug: "bringing-my-daily-posts-here-to-baty.net"
tags: ["Hugo"]
categories: ["Meta"]
draft: false
weight: 0
---

Now that I've moved my blog back to a static site generated with [Hugo](https://gohugo.io), I noticed that I was writing both my [Daily notes](https://daily.baty.net) and my blog posts in side-by-side Emacs buffers. It got me thinking about consolidating my sites even further.

<!--more-->

The challenge was that I didn't want to simply shuffle the daily posts in with the "regular" posts. I wanted a "Daily" section. But, I also wanted today's Daily post to show on the home page, since that's where the action is.

I'm the first to admit the Hugo's templating system is a complete mystery to me. I've been using Hugo for _years_ and I still don't know what gets rendered where or how. I mostly just throw stuff at the wall until something sticks.

After several hours of Google and wild guesses, I've gotten it close enough to publish. You're soaking in it. The home page shows the most recent post in the `/daily/` folder. Then at [baty.net/daily/](https://baty.net/daily/) I show a reverse-chronological list of daily posts.

I've added a couple of tweaks. The list of Daily posts differs from the home page in that I display the full posts and not just the "summary". That was surprisingly difficult to wrangle.

I have a new attribute in the front matter, `weather`, which is displayed on daily posts. This lets me display the weather differently from the posts' content. The cool feature here is that I'm adding the weather attribute automatically when creating new posts. I create posts using YASnippet, which can call custom functions at the time of expansion. Here's my "daily" snippet:

```org
  # -*- mode: snippet -*-
  # name: Hugo Daily Post
  # key: daily
  # uuid: daily
  # --
  *** TODO ${1:title} :@Daily:
  :PROPERTIES:
  :EXPORT_HUGO_BUNDLE: `(format-time-string "%Y-%m-%d-%A")`
  :EXPORT_FILE_NAME: index
  :EXPORT_HUGO_SLUG: `(format-time-string "%Y-%m-%d")`
  :EXPORT_HUGO_CUSTOM_FRONT_MATTER: :weather "`(jab/insert-weather)`"
  :END:

  $0
```

Note the ``:EXPORT_HUGO_CUSTOM_FRONT_MATTER: :weather "`(jab/insert-weather)`"`` property. I have a custom function called `jab/insert-weather` which calls the `wttr` service and outputs the current weather conditions. Surrounding the function with backticks causes the function to be evaluated while the snippet is expanded. Neat! Note that I also dynamically generate the filenames based on the current date.

This all means that, in my posts.org file, I can type `daily` and hit tab, enter the title, and I'm ready to publish.

[//]: # "Exported with love from a post written in Org mode"
[//]: # "- https://github.com/kaushalmodi/ox-hugo"
