---
title: Adding an RSS feed to my wiki
author: Jack
date: 2022-03-10T14:03:32+00:00
url: /2022/adding-an-rss-feed-to-my-wiki/
wabi_accentColor:
  - is-quarternary-accent
categories:
  - Meta
tags:
  - Blogging
  - TiddlyWiki

---
[TiddlyWiki][1] is a single static HTML file. It does not generate an RSS feed of new entries. It doesn&#8217;t _generate_ anything.

I treat my wiki at [wiki.baty.net][2] more like a blog than a wiki, so not having an RSS feed feels like an omission. Most of the time I consider this to be a feature. I like that I can write any old nonsense and it doesn&#8217;t actively go out and bother anyone. It&#8217;s my little secret, that you can read if you want.

On the other hand, I find it annoying when I&#8217;m interested in someone else&#8217;s writing and they don&#8217;t provide any feeds. So, I&#8217;ve decided to make it easier to follow me. I suppose if you deliberately subscribe to the wiki&#8217;s feed, you _want_ to be bothered by the stuff I write there.

My solution is based on [this article][3]. The short version is that I created a new tiddler named &#8220;RSS Feed&#8221; containing the following:



```
\define MyFilter(MyTag,domain)
[tag[$(MyTag)$]!sort[created]limit[10]]
\end

<?xml version="1.0" encoding="UTF-8" ?><br />
<rss version="2.0"><br />
<channel><br />
     <title>
{{$:/SiteTitle}}
</title><br />
     <link>{{$:/discoverfeed!!serverdomain}}</link><br />     <description>
{{$:/SiteSubtitle}}
</description><br />
     <lastBuildDate><$list filter="[!is[system]get[modified]!prefix[NaN]!sort[]limit[1]]" variable=modified><$list filter="[!is[system]modified<modified>]"><$view field="modified" format=date template="[UTC]ddd, 0DD mmm YYYY 0hh:0mm:0ss GMT"/></$list></$list></lastBuildDate><br />
<$set name="MyTag" value=Feed>
<$set name="domain" value={{$:/discoverfeed!!serverdomain}}>
<$list filter=<<MyFilter>>>
<item><br />     <title>
<$view field="title"/>
</title><br />
     <link><<domain>>#<$view field="title" format="urlencoded"/></link><br />
     <guid><<domain>>#<$view field="title" format="urlencoded"/></guid><br />
     <pubDate><$view field="modified" format=date template="[UTC]ddd, 0DD mmm YYYY 0hh:0mm:0ss GMT"/></pubDate><br />
     <description><![CDATA[<$view field="text" format=htmlwikified/>]]><br />     </description><br /></item><br />
</$list></$set></$set>
</channel><br /></rss><br />
```

This tiddler runs a filter finding the last 10 tiddlers tagged with `Feed` and renders them as RSS-formatted XML.

Extracting the rendered text from that tiddler out to an RSS file is done using my Makefile using the [TiddlyWiki node.js module][4]. The command is as follows:

`tiddlywiki --load index.html --render "&#91;&#91;RSS Feed]]" "rss.xml" text/plain`

This generates a file at ./output/rss.xml containing the rendered RSS text/xml. Later in the Makefile, I rsync rss.xml up to the server along with the rest of the wiki files. Here&#8217;s the complete Makefile:

```make
SERVER_HOST=server01.baty.net
SERVER_DIR=/home/jbaty/apps/rudimentarylathe.wiki/public_html
PUBLIC_DIR=~/Sync/wikis/rudimentarylathe/
TARGET=server01.baty.net

.POSIX:
.PHONY: checkpoint deploy

build:
        tiddlywiki --load index.html --render "&#91;&#91;RSS Feed]]" "rss.xml" text/plain

checkpoint:
        git add .
        git diff-index --quiet HEAD || git commit -m "Publish checkpoint"

deploy: build checkpoint
        git push
        @echo "\033&#91;0;32mDeploying updates to $(TARGET)...\033&#91;0m"
        rsync -v -rz --checksum --delete --no-perms $(PUBLIC_DIR)index.html $(SERVER_HOST):$(SERVER_DIR)
        rsync -v -rz --checksum --delete --no-perms $(PUBLIC_DIR)output/rss.xml $(SERVER_HOST):$(SERVER_DIR)
        rsync -v -rz --checksum --delete --no-perms $(PUBLIC_DIR)files $(SERVER_HOST):$(SERVER_DIR)
``` 

All this means is that you can now subscribe to the daily posts at [wiki.baty.net][5] using the following URL: <https://wiki.baty.net/rss.xml>.

The odd thing is that I normally create each daily post first thing in the morning and update it throughout the day. I&#8217;m not sure how different RSS readers will handle this, but it&#8217;s a start.

I haven&#8217;t added the discovery links yet, but should. I also don&#8217;t think the RSS tiddler needs all those non-breaking spaces so I may play with that later.

**Update March 11, 2022**: Saq Imtiaz sent a link to his [experimental plugin for generating RSS and JSON feeds][6]. Worth a look!

 [1]: https://tiddlywiki.com
 [2]: https://wiki.baty.net/rss.xml
 [3]: https://radar231.com/RSS%2520Feed%2520for%2520Tiddlywiki%2520SSG%2520Website.html
 [4]: https://www.npmjs.com/package/tiddlywiki
 [5]: https://wiki.baty.net/
 [6]: https://github.com/saqimtiaz/tw5-feeds
