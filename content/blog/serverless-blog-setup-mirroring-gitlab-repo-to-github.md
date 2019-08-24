+++
author = "cognitiaclaeves"
comments = true
date = "2019-08-24T22:54:00+00:00"
discussionId = ""
draft = true
summary = ""
tags = ["unimplemented children", "github", "gitlab", "high-level", "walkthrough", "serverless blog", "blogging"]
thread = "serverless-blog-setup"
title = "Serverless Blog Setup - Mirroring Gitlab Repo to Github"

+++
I've been doing a lot of work on setting up this blog lately. One thing I'm looking forward is having the ability to point to a public project important enough to me to work on over the weekend. This blog has a pipeline in Gitlab that interfaces with AWS Amplify to auto-generate this site when code changes are pushed, and I've made some interesting design decisions on how I implemented new features of the site that I think do a good job showing how I put thought into my work. I'd like to be able to point to this project in job interviews. So, I plan to replicate my private repo to Github.

When I experimented with this the first time, I set up the replication from gitlab to github, which was where my POC site was auto-configured to point to through AWS Amplify Console. From that experience, I learned that the replication is eventually-consistent, and it quickly became obvious that if I'm going to replicate between the two, I should do it in a way that doesn't impact the pipeline. So when I rebuilt it for keep-sies, I implemented it with Gitlab instead, with plans to replicate to Github for visibility.

I'm following [this guide](https://docs.gitlab.com/ee/workflow/repository_mirroring.html#setting-up-a-push-mirror-from-gitlab-to-github-core "Mirror from Gitlab to Github") to set up the mirror. The trickiest thing about the process was [setting up a personal access token](https://help.github.com/en/articles/creating-a-personal-access-token-for-the-command-line "Creating personal access token").