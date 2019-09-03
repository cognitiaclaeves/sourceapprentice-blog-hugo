+++
author = "cognitiaclaeves"
comments = true
date = "2019-09-01T20:00:00+00:00"
discussionId = ""
lastmod = "2019-09-03T14:00:00+00:00"
orig_date = ""
summary = ""
tags = ["talkyard.io", "walkthrough", "blogging", "high-level", "serverless blog"]
thread = "serverless-blog-setup"
title = "Serverless Blog Setup - Talkyard Comments"

+++
When I went to implement comments, I found that Disqus had started to charge for not showing ads. I did see that there should be a way to self-identify for self-served non-commercial blogs, but it wasn't clear how to do this from the site. It turned out that I just needed to send an email. But by the time I figured this out, I had already implemented [Talkyard](https://www.talkyard.io/blog-comments "Talkyard Comments").

The only two tricks to TalkYard config are:

* start [here](https://www.talkyard.net/-/create-site/embedded-comments "Implement Talkyard from Here")
* make sure to enter all possible domain names for the blog

  ![](https://s3-us-east-2.amazonaws.com/sourceapprentice-blog-media/sa-blog-talkyard-setup-comments.png)  
  Note that I included all subdomains I use for the live or test sites. If a subdomain is not included, then the comments will not load for that subdomain.

Additionally, I did something a little different, with concern to the hugo template code I use:

    {{ if .Params.comments }}
    	<comments>
        <script>talkyardServerUrl='{{ .Site.Params.talkyardServerUrl }}';</script>
        <script async defer src="{{ .Site.Params.talkyardScriptUrl }}"></script>
        <!-- You can specify a per page discussion id on the next line, if your URLs might change. -->
        <div class="talkyard-comments" data-discussion-id="{{ .Params.discussionId | default .File.BaseFileName }}" style="margin-top: 45px;">
        <noscript>Please enable Javascript to view comments.</noscript>
        <p style="margin-top: 25px; opacity: 0.9; font-size: 96%">Comments powered by
        <a href="https://www.talkyard.io">Talkyard</a>.</p>
        </div>
    	</comments>
    {{ end }}

The suggestion to provide for a way to override the `discussionId` is given in the Talkyard documentation. It is suggested to prevent the change of the URL from causing an apparent loss of the comments. However, this means that a matching `discussionId` needs to be determined when this happens. Since it's not already set by default, it wasn't clear to me what change would need to happen when I imagined imagine trying to figure out what change I would need to make when this comes up a single time in a few years.

With my approach, the base file name is used by default -- no need to even manipulate the front matter, either when the post is made or if the URL is changed -- it will be the same. (Because it's far less likely that the filename will be changed.) -- But, in the case that the filename is changed, the HTML source will show the original `discussionId` before the change is made, which will just need to be put into the front matter to override the new default.

There's one other thing built into the code block above: If a setting for the `comments` field in the front matter does not evaluate to True, then the comment block won't even be displayed.