+++
author = "cognitiaclaeves"
comments = true
date = "2019-08-27T05:45:00+00:00"
discussionId = ""
draft = true
lastmod = ""
orig_date = ""
summary = ""
tags = ["aws amplify", "walkthrough", "blogging", "high-level", "serverless blog"]
thread = "serverless-blog-setup"
title = "Serverless Blog Setup - Test Site"

+++
It wasn't long after I got my blog working that I wanted to make changes that could break the whole thing. Time to set up a test/dev instance!

## Connecting Branch to (production) App

The easiest way is to follow the prompt at the top, once the master branch is set up:

![](https://s3-us-east-2.amazonaws.com/sourceapprentice-blog-media/amplify-console-test-version-of-site.png)Clicking `Set up a test version of your site by connecting a feature branch`, gives the option to choose the branch:

![](https://s3-us-east-2.amazonaws.com/sourceapprentice-blog-media/amplify-console-add-respository-branch.png)After the branch is chosen, a new instance is available:

![](https://s3-us-east-2.amazonaws.com/sourceapprentice-blog-media/amplify-console-sa-instances.png)Note how the test instance is using the default test.*amplify.com domain. The themes that I'm using require a domain name.

Here's my first attempt at fixing this:

![](https://s3-us-east-2.amazonaws.com/sourceapprentice-blog-media/amplify-console-shared-domain-mgmt.png)![](https://s3-us-east-2.amazonaws.com/sourceapprentice-blog-media/namecheap-test-sa.png)

> // before the change:
>
> $ ping test.sourceapprentice.com
>
> ping: cannot resolve test.sourceapprentice.com: Unknown host
>
>   
> // after a few minutes:
>
> $ ping test.sourceapprentice.com
>
> PING d1qzcdre2mr5ze.amplifyapp.com (143.204.158.70): 56 data bytes
>
> 64 bytes from 143.204.158.70: icmp_seq=0 ttl=246 time=43.013 ms

And, of course:

![](https://s3-us-east-2.amazonaws.com/sourceapprentice-blog-media/test-sa-site-loaded.png)Success!

With that out of the way, however, there is a wrinkle in this solution, that does not fit my requirements: There is only one 'Build settings' option for the entire app, and I want to be able to work on new themes for the test instance, which is controlled in build settings.

![](https://s3-us-east-2.amazonaws.com/sourceapprentice-blog-media/amplify-console-build-settings.png)So, [onward to the next attempt](https://docs.aws.amazon.com/amplify/latest/userguide/custom-domains.html#custom-domain-subdomains "Adding only subdomain").

## Creating New App for Test Site

![](https://s3-us-east-2.amazonaws.com/sourceapprentice-blog-media/amplify-console-connect-new-test-app.png)I appreciate the info/warning, above. It tells me I'm on the right track.

![](https://s3-us-east-2.amazonaws.com/sourceapprentice-blog-media/amplify-console-new-test-app-build-settings.png)I was then able to specify my build settings as desired.

![](https://s3-us-east-2.amazonaws.com/sourceapprentice-blog-media/amplify-console-build-new-test-app.png)But the build was a little odd. I wonder if that will cause an issue on the 77th build ... 

The first thing I noticed after following the above steps was that everything was working. ... but I'm not sure that it should be, at this point. When I added the test branch to the (production) app earlier, it didn't work, until after I set up the test.sourceapprentice.com domain.

I went to build it again, this time with the old theme, which I'm pretty sure won't work if the domain doesn't match. It appeared that it just wouldn't rebuild. But after refreshing the screen, I was able to restart the build, and I discovered that some kind of self-correction appeared to have been made:

![](https://s3-us-east-2.amazonaws.com/sourceapprentice-blog-media/amplify-console-build-new-test-app-self-corrected.png)Sure enough, switching to dark mode didn't work. I'll use this as my litmus test. First I need to change the subdomain for the (production) app off of the subdomain I plan on using for test: 

![](https://s3-us-east-2.amazonaws.com/sourceapprentice-blog-media/amplify-console-domain-mgmt-test2-sa.png)Along with the matching NameCheap config:

![](https://s3-us-east-2.amazonaws.com/sourceapprentice-blog-media/namecheap-new-test-cname.png)(The new CNAME value matches the default host for the new test app.)

After disabling for the root, and inputting the test subdomain:

![](https://s3-us-east-2.amazonaws.com/sourceapprentice-blog-media/amplify-console-test-app-real-domain-mgmt.png)... it was time to wait:

![](https://s3-us-east-2.amazonaws.com/sourceapprentice-blog-media/amplify-console-test-app-ssl-verification.png)... and wait a little more:

![](https://s3-us-east-2.amazonaws.com/sourceapprentice-blog-media/amplify-console-domain-mgmt-test-app-domain-activation.png)... but I hate waiting, so of course I'm going to check early:

![](https://s3-us-east-2.amazonaws.com/sourceapprentice-blog-media/test2-sa-solarized-dark.png)I was able to switch themes on test2 ...

![](https://s3-us-east-2.amazonaws.com/sourceapprentice-blog-media/test-sa-min-night.png)... while having a different theme on test. ... One more test left:

![](https://s3-us-east-2.amazonaws.com/sourceapprentice-blog-media/final-test-sa-solar-dark.png)Finally:

![](https://s3-us-east-2.amazonaws.com/sourceapprentice-blog-media/amplify-console-final-domain-mgmt-test-app.png)