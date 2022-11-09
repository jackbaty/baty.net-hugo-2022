---
title: Weight logging with Tinderbox
author: Jack
date: 2021-12-28T12:09:53+00:00
url: /2021/weight-logging-with-tinderbox/
categories:
  - Software
tags:
  - Tinderbox

---
I kept a &#8220;daybook&#8221; using [Tinderbox][1] for years. I drifted away from Tinderbox for a few years after I became infatuated with Linux or iOS or other &#8220;cross-platform&#8221; systems. Right now, I&#8217;m back with a vengeance.

While rebuilding my Daybook, I wanted to make logging my weight easier. It&#8217;s not like it was difficult, but I wanted to tweak it.

Tinderbox is an outliner, so my weight entries are collected under a &#8220;Weight Log&#8221; node. It looked like this (I obviously wasn&#8217;t consistent with tracking last year).<figure class="wp-block-image size-full">

<img loading="lazy" width="335" height="177" src="http://baty.net/wp-content/uploads/2021/12/CleanShot-2021-12-28-at-05.37.28.png" alt="" class="wp-image-2389" srcset="https://baty.net/wp-content/uploads/2021/12/CleanShot-2021-12-28-at-05.37.28.png 335w, https://baty.net/wp-content/uploads/2021/12/CleanShot-2021-12-28-at-05.37.28-300x159.png 300w" sizes="(max-width: 335px) 100vw, 335px" /> </figure> 

The weight is stored in a numeric User Attribute called, surprisingly, &#8220;Weight&#8221;. The outline shows a custom &#8220;DisplayFormat&#8221; so that it reads nicely:

`$Weight + " pounds on " + format($StartDate,"MM D")`

To enter a new weight, I&#8217;d select an existing item in the outline, hit Return to create a new note, type in the weight, hit Return to save the note, then use the mouse to click the &#8220;Weight&#8221; attribute and re-enter the weight there. So much clicking! &nbsp;????.

What I wanted to do was to type the weight once in the note&#8217;s Name and have the Weight attribute populated automatically. Tinderbox notes can have &#8220;Rules&#8221; which are commands that run periodically and can update a note&#8217;s attributes based on just about any criteria. I could have created a rule that set the Weight based on the Name, but that seemed like overkill since this only ever needs to happen once per note.

With some help from Michael Becker, I think I&#8217;ve got it. (You should check out his [video series on Mastering Tinderbox][2] for all sorts of great Tinderbox content.)

There&#8217;s an OnAdd action which sets the Prototype, Date, and Name of the note. (Setting the Name of the new note to &#8220;Enter Weight&#8221; is a nice touch.)

<pre class="wp-block-code"><code>$Prototype="pWeightLogEntry";$Date|=date(today);if($Name=="untitled"){$Name="Enter Weight"};</code></pre>

Then, the new note gets a Rule (via the pWeightLogEntry Prototype) which sets the Weight attribute based on the value of Name:

<pre class="wp-block-code"><code>$Weight|=$Name;
if($Weight&gt;0){
$Name=$Date("l");
$RuleDisabled=true};</code></pre>

The trick here is setting `$RuleDisabled=true`. What this does is force the Rule to run only once, which is all I need. I wasn&#8217;t aware of the $RuleDisabled attribute, so thanks to Michael for that tip.

Now, to add a new Weight Log entry, I hit Return, type my weight, and hit Return again. Couldn&#8217;t be any easier! On my Daybooks &#8220;Dashboard&#8221; I can graph my weight over time, like so&#8230;<figure class="wp-block-image size-large">

<img src="http://baty.net/wp-content/uploads/2021/12/weight-graph.png" alt="" class="wp-image-2391" /> </figure> 

For those of you unfamiliar with Tinderbox, I&#8217;m sorry if I made too many assumptions here. Explaining Tinderbox can be an entire job in itself!

 [1]: http://www.eastgate.com/Tinderbox/
 [2]: https://www.youtube.com/watch?v=AQCp8tVRJSg&list=PL6MVDtSfcKxd2XLpenMAd9H4VknDyn6oz