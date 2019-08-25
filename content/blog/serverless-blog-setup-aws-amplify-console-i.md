+++
author = "cognitiaclaeves"
comments = true
date = "2019-08-04"
discussionId = ""
lastmod = "2019-08-25T04:00:00+00:00"
orig_date = "2019-07-20T05:00:00+00:00"
summary = ""
tags = ["walkthrough", "blogging", "high-level", "serverless blog"]
thread = "serverless-blog-setup"
title = "Serverless Blog Setup - AWS Amplify Console"

+++
I wasn't really sure how Amplify Console was going to work out for me, so I took a shortcut to testing out a [proof of concept](https://aws.amazon.com/amplify/console/getting-started/ "Get Started with Amplify Console"). When I started thinking about this, I had planned on building my own server-less components using Flask, Pelican, and a few clever lambdas. But I've also been meaning to start working with go -- so I figured I could give Hugo a try:

<div style="text-align: left"><img src="https://s3-us-east-2.amazonaws.com/sourceapprentice-blog-media/hugo-quickstart.png" style="width: 30%;text-align: left;display: inline-block;"></div>

This got me here:

![](https://s3-us-east-2.amazonaws.com/sourceapprentice-blog-media/amplify-console-hugo-poc.png)

Notice that Github is assumed. My repo was in Gitlab, so I ended up mirroring the repo to Github. While the eventually-consistent process was good enough for a POC, I knew it wouldn't be long before I started hating on myself if I actually implemented it this way. Shortly, I had a working server-less blog that would update when I pushed to master. Nice! Having that blog on my own domain name would be another matter.

## DNS Settings

I became pretty confused when trying to figure out how to get the domain name working. As a result, I may not have documented what transpired very well. One issue I ran into [when attempting to set up my domain through the Amplify Console](https://docs.aws.amazon.com/amplify/latest/userguide/custom-domains.html#custom-domain-third-party) was that I was using Namecheap to host my DNS, not the two options (GoDaddy|Google Domains) that [were used as examples in the Amazon instructions](https://docs.aws.amazon.com/amplify/latest/userguide/howto-third-party-domains.html) - both of which didn't support ALIAS records. This was what my working setup looked like:

![](https://s3-us-east-2.amazonaws.com/sourceapprentice-blog-media/namecheap-adv-domain-for-amplify.png)

## Ok, Now, to HuGo

[This crash course got me started](https://zwbetz.com/make-a-hugo-blog-from-scratch/ "A simple and cleanly styled Hugo blog").

Later, I also found [this blog post](https://willschenk.com/articles/2018/building-a-hugo-site/ "Hugo blog that uses Bootstrap"), which shows construction of a Hugo site using bootstrap, and [this one was also of interest to me](https://blog.webjeda.com/dark-theme-switch/ "Dark Theme Switch"), as I had planned on having a switchable light/dark theme. Finally, later, I found [this blog](https://regisphilibert.com/blog/2018/04/hugo-optmized-relashionships-with-related-content/ "Stylin' hugo blog"), which seems to be a very rich presentation for a Hugo site designed by someone who really knows what they're doing.

## Hugo++

I'm actually updating this content about a month after I originally wrote it. I've become pretty comfortable with modifying the Hugo templates. To date, I've implemented ideas that I saw in the crash course into my own spin-off of a Solaris Hugo theme, added the handling of a last modified date, when it appears in the front matter, light/dark CSS switching capability, and just today, the capability of listing articles that are part of the same series of articles, in order to make it is easy to navigate as possible when I write a series, like I did for the steps I took to set up a server-less blog. So far I've found the experience pretty enjoyable. I don't seem to get stuck for long, and the solutions appear to be pretty clean. All of the changes I've made to date are in templates -- and those changes have felt easier and cleaner then when I made similar changes in Jekyll.

## Writing Tools

I've been taking as many short-cuts as possible with this project -- so I've had my ear to the ground looking for options for tools to handle WYSIWYG Markdown publishing. Originally, I started out using StackEdit.io. For my purposes, though, SE was a little kludgy, and there came a time when I couldn't figure out why I couldn't see a post from SE. So I was pretty stoked when I found Forestry.io, which seemed specifically designed for the purpose I wanted to use it for: as a CMS for statically generated sites! I'll be writing a post on what I needed to do to get Forest.io up and running at a later date.

## Some Theme-Switching Ideas

* [simple? Javascript approach](https://www.thesitewizard.com/javascripts/change-style-sheets.shtml "Simpler Javascript only theme switching approach")
  * ( I ended up modifying this to suit my needs )
* [Much prettier bootstrap version](https://github.com/nathancday/min_night/blob/master/layouts/partials/js.html "Pretty Bootstrap theme with light and dark switch")
  * ( But no easy way to make it Solarized )
* [Bootstrap Solarization](https://bootswatch.com/solar/ "Solarized Bootstrap theme")