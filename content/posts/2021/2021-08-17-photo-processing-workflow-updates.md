---
title: Photo processing workflow updates
author: Jack
date: 2021-08-17T11:13:07+00:00
url: /2021/photo-processing-workflow-updates/
featuredImage: /wp-content/uploads/2021/08/pm.png
categories:
  - Photography
tags:
  - Workflow

---
<!--kg-card-begin: html-->Take a look at this list from my notes about how I manage my photos:

  * 2019-01-01 I&#8217;ve decided I&#8217;ll be using Lightroom CC.
  * 2021-05-15 Don&#8217;t listen to 2019 me, I&#8217;m using Lightroom Classic
  * 2021-06-03 Don&#8217;t listen to May 2021 me, I&#8217;m using Capture One now.
  * 2021-08-12 Don&#8217;t listen to June 2021 me, I&#8217;m using Lightroom Classic again.
  * 2021-08-15 Don&#8217;t listen to last week&#8217;s me, I&#8217;m using Capture One.

Obviously, I struggle with which tool to use. I was certain I&#8217;d &#8220;permanently&#8221; settled on Lightroom Classic just a week ago. In my comparisons, Lightroom wins nearly every category. But there was this entry:

<blockquote class="wp-block-quote">
  <p>
    C1: I get better images, faster
  </p>
</blockquote>

I couldn&#8217;t get this advantage of Capture One out of my head. Somehow, with my digital files, Capture One&#8217;s defaults come really close to where I want to end up, whereas in Lightroom I always have work to do.

My head says, &#8220;Use Lightroom because it&#8217;s &#8216;standard&#8217; and works with everything.&#8221; but my heart says, &#8220;You know you like using Capture One better, so do that!&#8221;

The the other thing that settled it for me this last time was the realization that I want my editor and my library to be decoupled. Lightroom _really_ wants to be my library. In fact, I spent a good portion of last weekend importing 100,000 images into a single Lightroom Library. It&#8217;s an adequate library, but using it as my primary tool puts me in a situation I don&#8217;t want to be in: I&#8217;m relying on Lightroom (and Adobe) for _everything_. Much better to have a DAM tool that isn&#8217;t entirely dependent upon a specific photo/RAW editor.

This is where [Photo Mechanic Plus][1] comes in. I&#8217;ve been using Photo Mechanic for a decade or more, and there&#8217;s nothing better or faster for ingesting, culling, and applying keywords and metadata to photos. Now, with the new &#8220;Plus&#8221; version, it&#8217;s also a powerful DAM.

My process is currently as follows:

  * Ingest photos or scans using PM
  * Rename with PM (e.g. &#8220;YYYYMMDD-FILENAME.dng&#8221;)
  * Edit the RAW files in Capture One (using a temporary &#8220;session&#8221;)
  * Export a &#8220;burned&#8221; JPG from each edited RAW file in the same folder with the same name (but using .jpg rather than .dng or .tif)
  * Move files to wherever they belong (usually in &#8220;/Media/Photos/YYYY/MM-Month YYYY/&#8221;) using Capture One (so the edit settings travel with them)
  * Add exif data to any scanned film files using [Exiftool][2] or the [MetaImage][3] app
  * Add any metadata, keywords, etc. to every image (or at least _most_ of them) using PM.
  * Add new photos to the main PM catalog
  * Upload or share using PM as desired

Once the initial edits are done and I have created permanent JPGs, everything lives in organized folders on my hard drives and are viewed, searched, managed, shared using Photo Mechanic. If I want to do followup edits later, I can always open the RAW files in Capture One or whatever other app I might want to use.

I miss things from Lightroom. For example, to convert scanned color negatives I use [Negative Lab Pro][4], which only works in Lightroom. I miss some of the plugins and other tools, too. But I feel like this is better for my library and my photos for the long haul.

<!--kg-card-end: html-->

 [1]: https://home.camerabits.com/tour-photo-mechanic-plus/
 [2]: https://exiftool.org
 [3]: https://neededapps.com/metaimage/
 [4]: https://www.negativelabpro.com