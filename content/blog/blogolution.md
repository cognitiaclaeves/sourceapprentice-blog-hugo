---
title: "Blog-o-lution"
date: 2019-07-29
tags: [ blogging, lifestyle, oversharing, reconstitute, rant, imposter syndrome ]
comments: True
---

I've been trying to start a blog for years now. I've had a lot of issues with sustainability. Each time I figure out a way to take another layer of maintenance out. This time around, I've kept old posts long enough to see some patterns.

Since some of these blogs are difficult for me to read through today, I've summarized the stages below and moved most of the related entries into archives. "That thing never happened ... unless you are looking for information on how to do that thing, yourself, in which case, see the links below." Needless to say, I recommend jumping straight to the end and saving time.

#### BlogV0: ???? - 2016-01-12

In BlogV1, I reference a Wordpress site. So apparently, there was once a blog that was done in Wordpress. I don't know where, I just have to take my own word for it.

#### BlogV1: 2016-01-12 - 2016-04-16 : Jekyll (and Hyde)

In a meetup for CloudAustin, I got pretty excited about the prospect of writing in Markdown and publishing a static site in HTML. It seemed like a good idea, at first, using vagrant to run the static-site-generation software (Jekyll) -- but I had a number of issues, and when my laptop died and I needed to get the blog back online on a new laptop, I found three years of excuses not to follow through.

TLDR; It can be painful, even to run a site-generator locally:

- [The Next Blog](../2016-01-17-the-next-blog/)
- [Blog Fail](../2016-01-16-blog-fail/)
- [Blogging w/ Vagrant: Docker-Jekyll-Github](../archive/2016-03-03-blogging-with-vagrant-docker-jekyll-github/)
- [Blogging w/ VDJG - Shortcut](../archive/2016-03-08-blogging-with-vagrant-docker-jekyll-shortcut/)
- [Blogging w/ VDJG - Shortcut++](../archive/2016-04-16-blogging-with-vagrant-docker-jekyll-shortcut-revisited/)

#### BlogV2: 2019-01-20 - 2019-02-17 : Destination Serverlvess (with Stackedit.io)

During those three years, I thought about how I could make a blog more accessible to someone like me. I conceived an idea to write blog posts in a front end driven by AWS's Amplify -- that would save the contents to S3 buckets. When the S3 buckets were updated, those updates would be processed by Lambda functions that used Pelican, a Python-based static-site generator. In the interim, I figured out how to write blog posts using Stackedit.io that would be saved in gitlab.

#### BlogV3: 2019-07-20 - Current : Amplify Console (Iterations in AWS + Gitlab editor)

After my most recent contract ended, I was looking for something to do to cope with the imposter's syndrome I feel when interviewing for a tech job while being unemployed. Now that I'd given some serious thoughts to the requirements of the thing that I would need (all of it running in the cloud), I asked the peeps at #hangops if the thing I wanted had already been built yet. I was surprised to find that I should be able to use Amplify Console for it, a technology that I'd first learned about only days earlier (Jul 18th), via the AWS Innovate online conference.

With all the pieces theoretically figured out, I set out to materialize the new blog. I had an issue with StackEdit.io not seeing files that were in gitlab, so I started using the online IDE in gitlab to write the blog posts.

- [Amplify Console, Part 1](../2019-07-20-amplify-console-1/)
- [Amplify Console, Part 2](../2019-07-20-amplify-console-2/)

