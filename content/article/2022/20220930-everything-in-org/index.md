+++
title = "Everything is in ~/org"
date = 2022-09-30T06:19:00-04:00
slug = "everything-is-in-org"
draft = false
tags = ["Emacs", "Org-roam", "PKM"]
+++

The more notes I put into [Org-roam](https://www.orgroam.com/), the more I _want_ to put there.

My Org-roam directory has always been in ~/org/roam, meaning that my database was limited to files I put in that directory. The rest of my org files have been in ~/org, so they're out of "reach" of Org-roam. Sometimes, though, I wanted link from, say, my Daybook.org file to one of my Org-roam files, thereby making that daybook entry part of my org-roam database. 

I started wondering what would happen if I put _everything_ into Org-roam. Or, at least made everything available to Org-roam. To that end, I changed my `org-roam-directory` to my top-level `~/org` folder. Now _anything_ can be an Org-roam node. All I need to do is add an ID property to a heading or file by running `org-id-get-create`. 

So far I don't see a downside to this approach. I have made Org-roam nodes out of  Daybook headlines, Journal entries, even TODO items. All linked up and networked as part of my database. I don't know how well this will scale over time, but I'll cross that bridge when I get to it.
