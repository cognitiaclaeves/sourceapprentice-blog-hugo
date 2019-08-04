---
title: AWS Amplify Console, Part 1
date: 2019-07-20
author: cognitiaclaeves
tags: [reconstitute, blog v4, serverless blog, amplify console, fix]
draft: true
---

Recently I've discovered Amplify Console on AWS. This seems to be the last piece I needed to get a functional maintenance-free serverless 100% cloud-native blog with minimal coding work.

I'm currently using StackEdit to write markdown into a private gitlab repo. [I have this all set up the way I wanted](unimplemented_future_blog_post), so I thought I'd try [mirroring the private gitlab repo out to a public github one](https://docs.gitlab.com/ee/workflow/repository_mirroring.html#setting-up-a-push-mirror-from-gitlab-to-github-core).

[This required setting up a personal access token for the new github repo.](https://help.github.com/en/articles/creating-a-personal-access-token-for-the-command-line)

The mirror function appears to be eventually-consistent. If that turns out to be too annoying, I can always iterate over it later and figure something else out.

The repo I have set up has a directory structure that looks like this:

    develop:
    - pre-blog
        - stackedit-environment
        	- Trash
        	- Temp
        	- content
        	    - all blog entries
            - templates

    master:
    - pre-blog
        - ...

I'm probably going to need to address the fact that the blog entries are not at the root of the repo at some point.

I'm following this guide [for setting up hugo in AWS Amplify Console](https://thetestlabs.io/post/continuous-deployment-for-hugo-with-aws-amplify). I anticipate adding something to the amplify build settings file, amplify.yml, not named in the above blog post.

#### DNS Settings

One issue I ran into [when attempting to set up my domain through the Amplify Console](https://docs.aws.amazon.com/amplify/latest/userguide/custom-domains.html#custom-domain-third-party) was that I was using Namecheap to host my DNS, not the two options (GoDaddy|Google Domains) that [were used as examples in the Amazon instructions](https://docs.aws.amazon.com/amplify/latest/userguide/howto-third-party-domains.html) - both of which didn't support ALIAS records. This was what my setup looked like:

** FIX IMAGE
![Namecheap settings][namecheap settings]



#### Using Images in Markdown

[This was a little tricky](https://richardstudynotes.blogspot.com/2014/04/link-images-stored-in-google-drive-to.html).

#### Ok, Now, to HuGo

[This crash course got me started](https://zwbetz.com/make-a-hugo-blog-from-scratch/).

Later, I also found [this blog post](https://willschenk.com/articles/2018/building-a-hugo-site/) and [this one was also of interest to me](https://blog.webjeda.com/dark-theme-switch/).


[namecheap settings]: https://drive.google.com/uc?id=1mHRWYBBWX-TODv9CXpDNPouFYLccxfz8

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0ODk5MDA0MDEsMTE4NjM0ODgwMywtMj
kzMjMxNTUwLDEwODE5MjIxMzksLTE0MDE0MDA4NjEsMTY1MDc0
MjM2LDIwNTUwMTcxMjBdfQ==
-->
