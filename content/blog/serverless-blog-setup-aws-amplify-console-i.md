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
title = "Serverless Blog Setup - AWS Amplify Console I"

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

[This crash course got me started](https://zwbetz.com/make-a-hugo-blog-from-scratch/).

Later, I also found [this blog post](https://willschenk.com/articles/2018/building-a-hugo-site/) and [this one was also of interest to me](https://blog.webjeda.com/dark-theme-switch/).