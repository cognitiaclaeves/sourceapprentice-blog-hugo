---
title: Serverless Blog Setup - The Repo
date: 2019-08-03
author: cognitiaclaeves
tags:
- blogging
- lifestyle
- walkthrough
- high-level
- serverless blog
- git
- gitlab
- unimplemented children
comments: true
discussionId: ''
summary: ''
thread: serverless-blog-setup

---
Most of the static blogs I've seen on the internet have their content saved in a git repo of some sort. In this blog post, I'm covering how I set up my blog repos. I put some thought into it because I want to be able to make blog changes from a compromised terminal without compromising my blog. (Not that I would ever knowingly do this, that's just the standard of security that I want to aim for: I got the idea while exploring play-with-docker.com -- there is a warning when you login that any creds you use are not safe -- my solution for this was to create a user whose credentials could be compromised without compromising the root of the git repo that user would be contributing to.) Considering I'm using 2nd factor for all the accounts, this approach should really be overkill. On the other hand, it's probably a way that someone could consider setting such a thing up in an enterprise -- there is a separation of concerns between the owner and any of the updaters -- so it gives me an opportunity to practice such a thing in my personal project.

## The Steps

* create a new online persona (updater) in gmail
  * second factor
  * optional firefox container
* create git account SSO'd to gmail persona
* create git repo with 'admin' account
* setup permissions for updater account

## High-Level Walk Through

My online git provider of choice is gitlab. This is because gitlab has a company culture that I just love. Since I'd love to work there, I figured I'd make it the home of my git repos as well.

To login to gitlab, I use SSO via gmail with 2nd factor configured. I capture the 2nd factor UPC in two applications - a browser-based extension called [Authenticator](https://addons.mozilla.org/en-US/firefox/addon/auth-helper/) which backs up its data to the cloud (I use DropBox, because I was able to configure DropBox to give access to its own directory for the app), and with [authy](https://authy.com/) on my android (The company that made authy, [Twilio](https://www.twilio.com/), is also an awesome company whose culture I admire.) It's possible to capture and confirm them both at the same time. For the reasons why I'm so anal about 2*2nd Factor, see this blog: [Unimplemented](Unimplemented).

So the first steps, then, is to create a new online persona in gmail that can be used for updating the repo, and to set up its 2nd factor.

I use Firefox, because they are guardians of privacy, and I create a new account container with the [containers](https://addons.mozilla.org/en-US/firefox/addon/multi-account-containers/) extension to use only with this identity. (This saves me from having to burn my privacy session and from needing to log out and in when switching identities.) I believe there is an equivalent built into the chrome browser.

Once the updater persona is set up, create a new account at GitLab (or your online git repo provider of choice).

Then, from the master gitlab account (Set this up, if it isn't already), create the new repo that will be used for the blog. Grant permissions for the updater persona to only make updates. For gitlab, this is assigning the developer role.

The end-game for this blog is for it to be entirely accessible and for it to live entirely in the cloud. Originally, I was using Stackedit.io to create / edit blog posts, but when I had some issues with files showing up, I discovered Gitlab's Web IDE, which works well enough until I create something specific to this purpose. The developer role gives the updater access to the web IDE, which is all that is needed to enter/update blog posts.

Then, when these changes are pushed to master, AWS Amplify infrastructure will build out the blog from the source and pulish the changes to the site.

Next: [How to Set Up AWS Amplify Hugo Blog](serverless-blog-setup-aws-amplify-console-i "Serverless blog setup with AWS Amplify Console")