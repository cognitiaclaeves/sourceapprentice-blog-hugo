---
layout: post
title: "The Next Blog"
date: 2016-01-12
tags: [ blogging, blog design, wordpress, jekyll, lifestyle, linux, oversharing, blog v1, vagrant blog, reconstitute, rant ]
comments: True
lastmod: 2016-01-17 06:20:00
orig-date-maybe: 2015-01-12 06:20:00
---

## Goodbye Wordpress

I lost my desire to blog with Wordpress the first time I watched it mangle my spacing, and then enforce whatever it was doing by not taking changes ... until my efforts to make it  accept my deisred whitespace wiped out the entire post. I remember feeling particularly angry that I had found a bug report mentioning this ... that was ... ... years ... old. Or maybe it was when I was messing around with themes, and I did something in the theme that caused the entire site not to load. Or maybe it was the day that I realized that all the posts are stored in a database, so there's no easy way to backup. And restoring a Wordpress site? By the time I considered that nightmare, I was determined to avoid that level of hell by avoiding blogging altogether.

It was beginning to feel a lot like Microsoft tech: big, bloated interfaces that save your data in secret places that are a nightmare to back up. ... crashes, wasted time ... wasted hours, days, ( which I projected would later be followed by weeks and months ).

And I was supposed to maintain a spririt of creativity throught that? Shaking my fists at inanimate computer screens ( which aren't even part of the problem ) -- is not my idea of time well spent.

My experience with Wordpress wasn't all bad. It gave me standards for a blogging platform:

- I wanted to be able to edit files off-line
- I wanted the posts to be as effortless to maintain as possible
- I didn't want everything in a database
- As a matter of fact, maybe not a dynamic site, at all
- I wanted the data backed up to the cloud somewhere
- I wanted solid revision control
- I wanted the site to be easily restorable


If you've ever worked with Wordpress, you might notice that the list above is sort of the antithesis of Wordpress.

And while I wanted convenience, I still wanted the end result to be more customizable ( and less expensive! ) than those website-in-a-box kind of places.

And then I happened to see a demo where someone had married static site generation ( with Jekyll ) with devops style cleverness. ( I talk about how this site is set up [here](http://localhost:4000/tags/light/blogging-w-vdjg). )

I just knew this was my ticket to a blogging platform that would be a better fit for me.

And it just so happened that this solution came with free revision control (backups) AND free hosting? I hadn't even dared put on my list of standards that I didn't want to manage a web hosting account for the site. I didn't dream I'd find such a thing.


## Hello Chaos

So, I took the time to duplicate what I saw in the demo, and suddenly found myself confronted with a new, empty page; with chaos. Where the page was once taken up by "helpful" fluff of all kinds, now it was like the page was staring back at me.

> Well, what are you going to do now? 

It was a feeling similar to the feeling I had when I finally succeeded in switching to Linux: I had been used to hand-holding, and suddenly confronted with so much more potential than my hand-holding-conditioned mind could fathom. All of the layers that I had once been comfortably unaware of now held key clues that I needed to understand to use my system efficiently.

What did I want?

My mind boggled at the sheer potential. If I could do anything, what would I do?

I wanted my blog to be friendly to human beings and different devices.  It seemed like Jekyll themes already considered mobile devices and computer screens, out of the box, but friendly to people? How could I ( who am not a web developer ) make such a thing? How would I make it human-friendly?

That was when I remembered my favorite theme: Solarized -- which has light and dark choices, both designed to be easy on the eyes. And that was when I realized, that if Jekyll builds static pages in files saved locally to my hard drive, then I could tap into my scripting aptitude to mangle the static files after the build, and create the effect of a dynamic ( theme-switchable ) site with all of the advantages of a static one.

So, apparently, when confronted with chaos, I can build something that I would have never conceived of without staring down the void.

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4MTM0MTAyMTVdfQ==
-->