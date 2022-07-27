---
title: Writing everything in TiddlyWiki and publishing just the public parts
author: Jack
date: 2021-05-08T09:58:15+00:00
url: /2021/writing-everything-in-tiddlywiki/
categories:
  - Misc
tags:
  - Notetaking
  - Tech
  - TiddlyWiki

---
<!--kg-card-begin: html-->I take all my notes in 

[TiddlyWiki][1] now, and publish most of them to [rudimentarylathe.wiki][2].

For the past few years, I’ve published my wiki using TiddlyWiki. I write daily, publicly sharable notes there. Private stuff goes elsewhere…or did, until yesterday.

It’s the “elsewhere” part that drove me nuts. I have a private [Roam][3] database in which I would track things I _don’t_ want to share. Or maybe I should write it in [Org mode][4]. Or [Obsidian][5], or [Craft][6], or or or. The difficult part for me has been that I want to take a note about, say, a new camera purchase. There are two components to it, the information about the camera itself, and information about the purchase. The former is public, the latter is private. This means I create one note in TiddlyWiki and one in, let’s say, Roam. There are dozens of examples like this, and it’s crazy-making. I thought I could manage this using links or copy/paste but it sucks trying to do that. I could also make everything public or private. Neither of these are feasible.

If only I could keep everything in one place, but only publish things I wanted public. Then, a few days ago, Soren Bjornstad came to the rescue with his video, [A Tour Through My Zettelkasten][7].

Wow, other than building an amazing Zettelkasten, Soren has implemented nearly everything I needed in order to go all-in with TiddlyWiki for my own wiki.

A few highlights:

  * Public and Private tiddlers
  * Sensible tagging and organization
  * Override the “copy permalink” feature to substitute public URL when on localhost
  * Scripted rendering and publishing of public wiki
  * Specific behavior when viewing public vs private editions
  * A number of other nice touches

I borrowed some of these and integrated them into [Rudimentary Lathe][2]. Now, I’m taking all my notes in TiddyWiki. I’ll describe the process a little.

**Editing the wiki locally**.

I use TiddlyWiki as a local Node.js app. While one of TiddlyWiki’s great features is that can be just a single HTML file, running it locally as a single-page web app via node.js makes things a bit more flexible. Also, it’s the easiest way to allow for saving changes in Safari. The file structure looks like this:

<pre class="wp-block-code"><code>├── files/
├── plugins/
├── tiddlers/
└── tiddlywiki.info</code></pre>

All tiddlers are kept as separate “.tld” files in the tiddlers folder. Here’s an example:

<pre class="wp-block-code"><code>created: 20201220181044760
creator: jack
modified: 20210505182021507
modifier: jack
revision: 0
tags: Public
title: Leica APO-Summicron-SL 35mm ASPH
type: text/vnd.tiddlywiki

&#91;img&#91;files/2020/leica-apo-summicron-sl-35mm.jpg]]

I prefer primes, so this is the one I've chosen for the &#91;&#91;Leica SL2-S]]. Watching Peter Karbe admit it's is desert-island lens and suggesting it's the best lens Leica has ever produced made the decision a little easier.</code></pre>

I have over 2300 of them currently. Another nice side effect is that git diffs are much more usable on individual text files than on a giant HTML file.

**Public vs Private content**.

Any tiddler I want to be public gets a “Public” tag. That’s it. The export script is smart enough to automatically include all system tiddlers, etc so that everything works.

As a useful helper, each tiddler displays a “Publish this tiddler” checkbox to make adding the tag easier, as well as serving as a handy indicator of private vs public status. The export script updates one of the configuration tiddlers so that the published version doesn’t show this checkbox.

I can’t tell you how huge this is. Not having to choose the tool or app for new notes is so liberating. I can now write and link freely with _everything_ and can still share most of it publicly.

**Hosting**

I’ve never used Github Pages for hosting any content, so thought this would be a good opportunity to try it. Basically, I keep a separate repo of the public version and pushing to that repo automatically publishes it. Super easy to set up.

**Publishing workflow**.

Soren was kind enough to share a version of the script for publishing his wiki (publish.sh), which I’ve modified slightly. Here are the highlights.

<pre class="wp-block-code"><code>PRIV_FOLDER="rl-wiki"
PUB_FOLDER="public-wiki"

FILT='&#91;is&#91;system]] &#91;tag&#91;Public]] -&#91;&#91;$:/plugins/tiddlywiki/tiddlyweb]] -&#91;&#91;$:/plugins/tiddlywiki/filesystem]] -&#91;prefix&#91;$:/temp]] -&#91;prefix&#91;$:/state]] -&#91;prefix&#91;$:/sib/StorySaver/saved]] +&#91;!field:title&#91;$:/sib/WriteSideBar]]'

WIKI_NAME="index.html"ext_image_folder="extimage"</code></pre>

“FILT” is the tiddlywiki filter for determining which tiddlers to include (and exclude). The `[tag[Public]]` bit is the key to the public/private thing.

Then we export tiddlers based on the filter and settings above.

<pre class="wp-block-code"><code>"$(npm bin)/tiddlywiki" "$PRIV_FOLDER" --savewikifolder "$pub_wiki" "$FILT"</code></pre>

Next, generate a single HTML version of the wiki and copy over the separate image files..

<pre class="wp-block-code"><code>"$(npm bin)/tiddlywiki" "$pub_wiki" \
    --render "$:/core/save/all" "$WIKI_NAME" text/plaincp -r "$pub_wiki/output"/* "$pub_ghpages"cp -R "$PRIV_FOLDER/files" "$pub_ghpages"</code></pre>

Isn’t TiddlyWiki amazing!?

Finally, we commit and push the public wiki to Github…

<pre class="wp-block-code"><code>if &#91; "$1" = "--push" ];
then
echo "Pushing compiled wiki to GitHub..."    
cd "$pub_ghpages" || exit 1    
git add .    
git commit -m "publish checkpoint"    
git push
else    
echo "Not pushing the wiki to GitHub because the --push switch was not provided."
fi</code></pre>

And voilà!

**A few nice odds and ends**.

Soren’s “Reference Explorer”, seen at the bottom of individual tiddlers, replaces my handmade backlinks display. His is much fancier. I removed a few tabs I don’t use, and may exclude the tags at some point. I conditionally exclude the explorer from my Daily Notes pages. (anything tagged “DailyNote” hides the explorer.) Another nice tweak is that if I add a “refexplorer-hide” field to any tiddler and set it to “true”, the explorer is not shown on that tiddler. Nifty.

TiddlyWiki comes with a button for copying a permalink to each tiddler. The problem with that for me is that when I’m running the wiki locally, permalinks look like this

http://localhost:8080/#CommandLineInterface, which obviously won’t work. Soren’s version of the button replaces localhost:8080 with the live hostname, e.g. https://rudimentarylathe.wiki/#CommandLineInterface. This saves me a ton of copy/paste/edit hassles.

**Putting it all together**.

When I’m ready to publish, I open a terminal and type `prl` (for “publish rudimentary lathe”)

prl is a script…

<pre class="wp-block-code"><code>#!/bin/shcd ~/Sync/rudimentarylathe./scripts/publish.sh --push</code></pre>

That’s it.

I wish more people would spend time getting to know TiddlyWiki. It’s amazing. It’s a [Quine][8], which makes it ridiculously flexible and powerful. And yet it’s very simple. It’s also a free, local-first, easily-distributable, storable, backup-able single HTML file.

TiddlyWiki is fun, fancy, and  
future-proof. I live there now.

 [1]: https://tiddlywiki.com
 [2]: https://rudimentarylathe.wiki
 [3]: https://roamresearch.com
 [4]: https://orgmode.org
 [5]: https://obsidian.md
 [6]: https://www.craft.do
 [7]: https://www.youtube.com/watch?v=GjpjE5pMZMI
 [8]: https://en.wikipedia.org/wiki/Quine_(computing)