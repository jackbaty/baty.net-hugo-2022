---
title: Book logging in plain text
author: Jack
date: 2021-03-06T17:40:33+00:00
url: /2021/book-logging-in-plain-text-2/
categories:
  - Misc
tags:
  - Plaintext
  - Tech

---
<!--kg-card-begin: html-->Of all the ways I’ve logged books, I’m thinking that plain text remains the best. I’ve been adding books to a text (Markdown) file for while now and it’s not pretty, but it works. And it will always work.

I publish a copy at ~~www.baty.net/books~~ `   `  [books.baty.net](https://books.baty.net)

Like I said, it ain’t pretty. On the other hand, I use it regularly by simply running little searches. If I want to know how many books are read in 2020, it’s just `grep 2020- books.md | wc -l` and I get `14`. To see the actual books, it’s even easier: `grep 2020- books.md` which gives me this:


    A Gentle Madness: Bibliophiles, Bibliomanes, and the Eternal Passion for Books by Nicholas A. Basbanes (2020-01-05) | ★★★★
    How to Do Nothing by Jenny Odell (2020-02-05) | ★★
    The Instructions by Adam Levin (2020-02-15) | ★★★★
    The Wisdom of Insecurity by Alan W. Watts (2020-03-06) | ★★
    American Dirt by Jeanine Cummins (2020-03-09) | ★
    Recursion by Black Crouch (2020-04-05) | ★★★
    Devoted by Dean Koontz (2020-04-23) | ★★★
    The Soul of an Entrepreneur by David Sax (2020-05-04) | ★★★
    Shakespeare for Squirrels by Christopher Moore (2020-06-09) | ★★★
    Network Effect (The Murderbot Diaries, #5) by Martha Wells (2020-06-24) | ★★★★
    Dark Matter by Blake Crouch (2020-07-19) | ★★★★
    The Permanent Portfolio by Craig Rowland (2020-07-22) | ★★★
    More Effective Agile by Steve McConnell (2020-10-10) | ★★★
    Futuristic Violence and Fancy Suits (Zoey Ashe, #1) by David Wong (2020-12-27) | ★★★★

Or, how many books have I read by Christopher Moore? `grep 'Christopher Moore' books.md`:

    Coyote Blue by Christopher Moore (1999-01-01)
    The Lust Lizard of Melancholy Cove by Christopher Moore (1999-01-01)
    The Griff: A Graphic Novel by Christopher Moore (1999-01-01)
    Lamb: The Gospel According to Biff, Christ’s Childhood Pal by Christopher Moore (2008-12-24)
    Island of the Sequined Love Nun by Christopher Moore (2009-03-12)
    A Dirty Job by Christopher Moore (2010-12-28)
    Bloodsucking Fiends by Christopher Moore (2010-12-28)
    The Stupidest Angel by Christopher Moore (2011-01-01)
    Secondhand Souls by Christopher Moore (2015-11-12)
    Noir by Christopher Moore (2018-05-15)
    Shakespeare for Squirrels by Christopher Moore (2020-06-09) | ★★★

It’s not perfect, and leaves out any kind of social discovery, so I also enter books in both [GoodReads][1] and [StoryGraph][2], which honestly only takes a few minutes per book so it’s hardly a burden.

I love that my plain text book log is so lightweight and simple.

<!--kg-card-end: html-->

 [1]: https://www.goodreads.com/user/show/1259384-jack-baty
 [2]: https://www.thestorygraph.com/
