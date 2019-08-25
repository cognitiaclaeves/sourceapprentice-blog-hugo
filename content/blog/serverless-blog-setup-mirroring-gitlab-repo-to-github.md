+++
author = "cognitiaclaeves"
comments = true
date = "2019-08-24T22:54:00+00:00"
discussionId = ""
summary = ""
tags = ["unimplemented children", "github", "gitlab", "high-level", "walkthrough", "serverless blog", "blogging"]
thread = "serverless-blog-setup"
title = "Serverless Blog Setup - Mirroring Gitlab Repo to Github"

+++
I've been doing a lot of work setting up this blog lately. One thing I'm looking forward to is having the ability to point to a public project important enough to me to work on outside of employment. This blog has a pipeline in Gitlab that interfaces with AWS Amplify to auto-generate the site when code changes are pushed, and I've made some interesting design decisions on how I implemented new features of the site that I think do a good job showing how I put thought into my effort. I'd like to be able to point to this project in job interviews. So, I plan to replicate my private repo to Github.

When I experimented with this the first time, I set up the replication from gitlab to github, which was where my POC site was auto-configured to point to (via point-and-click POC) through AWS Amplify Console. From that experience, I learned that the replication can be eventually-consistent, and it quickly became obvious that if I'm going to replicate between the two, I should do it in a way that doesn't impact the pipeline. So when I rebuilt it for keep-sies, I implemented it with Gitlab instead, with plans to replicate to Github, only for visibility.

I'm following [this guide](https://docs.gitlab.com/ee/workflow/repository_mirroring.html#setting-up-a-push-mirror-from-gitlab-to-github-core "Mirror from Gitlab to Github") to set up the mirror. The trickiest thing about the process was [setting up a personal access token](https://help.github.com/en/articles/creating-a-personal-access-token-for-the-command-line "Creating personal access token") and [configuring Gitlab to use it](https://docs.gitlab.com/ee/workflow/repository_mirroring.html#setting-up-a-push-mirror-from-gitlab-to-github-core "Configuring Gitlab to use Github Access Token").

This permission seems to work:

![](https://s3-us-east-2.amazonaws.com/sourceapprentice-blog-media/github-token-permission.png)

This should be the result after the token generates:

![](https://s3-us-east-2.amazonaws.com/sourceapprentice-blog-media/github-token-generation.png)

And then in Gitlab:

![](https://s3-us-east-2.amazonaws.com/sourceapprentice-blog-media/gitlab-mirror-with-github-token-2.png)

If this comes up, it means the permissions won't permit access:

![](https://s3-us-east-2.amazonaws.com/sourceapprentice-blog-media/bad-github-permissions.png)

Note: I had to refresh the screen to see the error.

With the correct permission:

![](https://s3-us-east-2.amazonaws.com/sourceapprentice-blog-media/gitlab-mirror-success.png)

Again: Had to refresh the screen.

And of course, everything should be visible in Github..