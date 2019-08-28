---
title: The Site
date: 2019-07-21T22:30:21.000+00:00
author: cognitiaclaeves
comments: false
tags: []
lastmod: 2019-08-27T21:00:00+00:00
thread: ''
summary: ''
orig_date: 
discussionId: ''

---
This blog is written to share high-level ideas and implementations concerning dev-ops related topics. The blog is generated from its markdown source stored in GitLab by Hugo, powered by AWS Amplify -- in other words, the blog and its content are completely server-less. I use forestry.io to actually write the content. There is a [series on this site](../../serverless-blog-setup-repo/ "How I built this blog") that details how I built the blog.

### blogging is hard for me

At the time when I'm writing this post, the approach I've taken to build this blog is fairly novel. Writing a blog needs to be super convenient for me, otherwise, I'll find a reason not to do it. ... I think I've got it right this time: the blog lives in the cloud, powered by several automated pipelines, accessible by cloud-based tools, protected by SSO with 2FA. I think I've considered everything ... that could get in the way later.

### design considerations

When I broke away from canned blogging solutions, I found myself faced with a question -- what should my blog look like? I thought it should use a Solaris theme, and the theme should be switchable between light and dark modes. To me, this represented an approach that thought about the reader first. From there, it was all about utility -- I added in tags, a way to display the date last modified, if it differed from the creation date, because that date becomes important with the speed of technology, and a way to group together blog series so that it's easy to follow. I'm not sure where the blog will go from here, but I suspect any additions I make to the structure will have similar practical applications.