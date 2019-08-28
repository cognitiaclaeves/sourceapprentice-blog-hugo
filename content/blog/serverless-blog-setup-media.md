+++
author = "cognitiaclaeves"
comments = true
date = "2019-08-24T21:00:00+00:00"
discussionId = ""
summary = ""
tags = ["unimplemented children", "aws s3", "forestry.io", "serverless blog", "high-level", "walkthrough", "blogging"]
thread = "serverless-blog-setup"
title = "Serverless Blog Setup - Media"

+++
When I thought about what I wanted in a server-less blogging solution, I knew that adding images to my blog entries was likely going to be a thing. I had anticipating needing to write my website that I'd use to manage images. That day might still come. But not today.

This morning I found [Forestry.io](https://forestry.io), which is effectively a CMS that can be used for static web site generators. I write it about it [here](../serverless-blog-setup-forestry-io "Forestry.io setup"). I started using it for maintaining the content of my site immediately.

While I was working my through the setup process, I noticed that it has some kind of setup for using AWS S3 for media (among other choices). If things go really well, this means that I won't have a pressing need to write my own site to do this. To set this up, I'll be following [their documentation](https://forestry.io/docs/media/s3/ "Forestry.io media setup for S3").

With the exception of the permissions descriptions for AWS S3 bucket changing, following the instructions seemed pretty straight forward. It's also possible that the permissions were a little lax -- I may go back and figure out how to set the permissions so that the entire bucket can't be deleted by the new user.

The good news is that this means my hypothesis was correct -- I do not need to custom-roll an app to manage WYSIWYG Markdown + Image management! Score!

At this point, I've got all the requirements I need to blog freely!