
---
layout: post
title:  "Holy Atomic Operating Systems, Batman!"
date:   2016-03-03 07:01:00
tags: [ docker, atomic host, kubernetes ]
comments: True
summary: Trying out AtomicHost for the first time.
---

This one is going to be short. My company has a weekly 'Docker Roundup' that the 'Misfits of Docker' participate in. We use an hour each week to explore what all of us are working on that's related to containers and container orchestration.

Additionally, we've recently started having a 'theme' for the meeting, a task to accomplish related to containers or container orchestration.

For the last one, I requested that we cover Atomic Hosts. We followed [this guide](http://www.projectatomic.io/docs/gettingstarted/) -- I should point out that we followed the directions almost exactly, even though some strings had changed, with the exception of the 192.\* IP addresses.  We replicated the steps on an AWS cluster.

It was a bit odd to instantiate a pod directly in kubernetes ( rather than a replication controller ), so we moved onto another guide that included an expose command, and that's about where our success ended: Amazon and Kubernetes don't know each other well enough for Amazon to respond to the expose command.

Other than that, though, the experience went pretty well: We were able to get a modern kubernetes cluster working that could create a single pod ( or replicated pods ) in under an hour. This was, by far, the fastest way to get a kubernetes cluster working on the cloud. Everything else that we've tried - CentOS guides and coreOS guides - have resulted in more work than an hour's worth. Recently I found one in Kubernetes/Contrib that uses Vagrant to set up the entire cluster, but doesn't work -- at least not without OpenStack.

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQ5MDkwNDAxXX0=
-->