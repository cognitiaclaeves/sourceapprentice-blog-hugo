---
layout: post
title:  "Blogging with VDJG: Part 1.75 - Vagrant, Docker & Jekyll - Return from the Void"
date:   2016-04-16 14:24:00
tags:
 - blogging-w-vdjg
 - vagrant
 - docker
 - github
 - jekyll
 - blogging
 - blog v1
 - vagrant blog
 - reconstitute
 - split between blogs
draft: True
comments: True
---

Walking away from a project and coming back about a month later is a great way to test the user-friendliness / accessibility of a solution! I must have forgotten ... nearly everything ... about how I set this blog up. ... When I went to make an update, I even started out in the wrong place!

So here are the gotcha's that became apparent to me as I tried to break back into blogging.

###Gotcha #1

The [short cut](../2016-03-08-blogging-with-vagrant-docker-jekyll-shortcut) that includes a custom Vagrantfile meant to encapsulate my custom script for executing Jekyll inside of docker inside of Vagrant ... leaves the git repo for phusion's baseimage-docker in a mixed state:

{{< highlight text >}}

➔ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   Vagrantfile

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        data/
        exec-jekyll.sh

no changes added to commit (use "git add" and/or "git commit -a")

personal/phusion-jekyll/baseimage-docker on master [!?]

{{< /highlight >}}

While this looks like something was left incomplete, it's not. I might revisit this in the future.

###Gotcha #2

`vagrant up` is not the only thing that needs to be executed to get jekyll going. `vagrant up` by itself really only sets up phusion's baseimage. When it runs, it prints out this ( somewhat confusing ) message:

{{< highlight text >}}

==> default: Machine already provisioned. Run `vagrant provision` or use the `--provision`
==> default: flag to force provisioning. Provisioners marked to run always will still run.

{{< /highlight >}}

One might wonder: why run `vagrant provision` when the message just said that the machine is already provisioned. In fact, running `vagrant provision` is exactly the the thing needed to kick off my custom script ( which kicks off jekyll - within Vagrant )

{{< highlight text >}}

➔ vagrant provision
==> default: Running provisioner: shell...
    default: Running: /var/folders/9s/320v29913qs9j6kzxnqv7smclw01rh/T/vagrant-shell20160416-8
3777-1t0dsij.sh
==> default: stdin: is not a tty
==> default: jekyll_runtime
==> default: jekyll_runtime
==> default: Running Jekyll!
==> default: Github does not allow user dependencies.
==> default: Configuration file: /srv/jekyll/_config.yml
==> default:             Source: /srv/jekyll
==> default:        Destination: /srv/jekyll/_site
==> default:       Generating...
==> default:                     done.

{{< /highlight >}}

So, two gotcha's later, and I'm back in business. As far as ramping back up on cold projects goes, that's not too bad.

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTE5ODM1NzIzXX0=
-->
