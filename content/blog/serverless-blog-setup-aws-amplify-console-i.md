+++
author = "cognitiaclaeves"
comments = false
date = "2019-07-20T05:00:00+00:00"
discussionId = ""
draft = true
summary = ""
tags = ["walkthrough", "blogging", "high-level", "serverless blog"]
thread = "serverless-blog-setup"
title = "Serverless Blog Setup - AWS Amplify Console I"

+++
I'm following this guide [for setting up hugo in AWS Amplify Console](https://thetestlabs.io/post/continuous-deployment-for-hugo-with-aws-amplify). I anticipate adding something to the amplify build settings file, amplify.yml, not named in the above blog post.

#### DNS Settings

One issue I ran into [when attempting to set up my domain through the Amplify Console](https://docs.aws.amazon.com/amplify/latest/userguide/custom-domains.html#custom-domain-third-party) was that I was using Namecheap to host my DNS, not the two options (GoDaddy|Google Domains) that [were used as examples in the Amazon instructions](https://docs.aws.amazon.com/amplify/latest/userguide/howto-third-party-domains.html) - both of which didn't support ALIAS records. This was what my setup looked like: