+++
author = "cognitiaclaeves"
comments = true
date = "2019-08-24T20:00:00+00:00"
discussionId = ""
lastmod = ""
orig_date = ""
summary = ""
tags = ["forestry.io", "walkthrough", "blogging", "high-level", "serverless blog"]
thread = "serverless-blog-setup"
title = "Serverless Blog Setup - Forestry.io"

+++
When I envisioned setting up a server-less blog, I had thought I was going to need to build the piece that handled WYSIWYG Markdown editing as an AWS Amplify app. As a temporary measure, I used StackEdit.io as a way of writing the Markdown, but had some issues with it. When I couldn't get it to display content, and couldn't figure out why, I moved on to use GitLab's Web IDE. It was much friendly to use, in the sense that it took difficult to see/solve mysteries out of composing the posts, but it didn't manage media. This was what I had envisioned would make it necessary to build my own app.

And then I found [Forestry.io](https://forestry.io "Forestry.io - a CMS for static blogs").

![](https://s3-us-east-2.amazonaws.com/sourceapprentice-blog-media/forestry-io-blog-entry.png)

The interface was cleaner than anything I had seen so far, and it looked like they handled the media piece. When I set up my first repo, I tried to use their default 'quick/SSO' setup, but this resulting in seemingly never-ending cursor spin. So I turned that off and used the the [manual setup](https://forestry.io/docs/git-sync/manual-setup/#public-key "Forestry.io manual setup") instead.

In the first post of this blog series, I mention that I've set up a blogging user in GitLab that can basically only contribute content (as opposed to being able to manipulate the repo itself.) This was meant as a security measure.

I had no trouble setting this up in Forestry.io:

![](https://s3-us-east-2.amazonaws.com/sourceapprentice-blog-media/forestry-io-collaborators.png)

As you can see, there's even room to use some kind of teams abstraction with the pro plan.

I did have some concern with kicking off a new build with each change in forestry.io, so I set up a separate branch that forestry.io commits to, that I then merge into the test branch. When I merge the changes into the test branch, the test instance of the site gets updated. If everything looks good, I then merge test into master, and the live site gets updated.

Forestry.io is really one of the best user experiences I've had to date. The interface is nice and clean. Sometimes it seems a bit slow, but I haven't worked out if that's on their side or mine. I'd also appreciate a way to collapse the front matter, but there is adequate space to write, as is. If you have a static blog, I highly recommend giving setting up forestry.io.