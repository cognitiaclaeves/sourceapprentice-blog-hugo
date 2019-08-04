
---
layout: post
title:  "Blogging with VDJG: Part 1.5 - Vagrant, Docker & Jekyll - Shortcut!"
date:   2016-03-08 23:00:00
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

I just finished going through all of the steps of how I created the vagrant-docker-jekyll combo that I use to blog with.

... And then I realized ... the whole point of vagrant and docker is to be able to create an environment that can be replicated ... so it should theoretically be possible for me to set up the entire environment and provide a few short lines to get the whole thing working, right?  Right.

{{< highlight text >}}

git clone https://github.com/phusion/baseimage-docker.git
cd baseimage-docker
mkdir data
curl https://raw.githubusercontent.com/cognitiaclaeves/source.cognitiaclaeves.github.io/develop/source-files/Vagrantfile > Vagrantfile
curl https://raw.githubusercontent.com/cognitiaclaeves/source.cognitiaclaeves.github.io/develop/source-files/exec-jekyll.sh > exec-jekyll.sh
chmod +x exec-jekyll.sh
vagrant up

{{< /highlight >}}

> Update 4/16/2016 --
> If you don't see
> {{< highlight text >}}
> ==> default: Running Jekyll!
> ==> default: Github does not allow user dependencies.
> ==> default: Configuration file: /srv/jekyll/_config.yml
> ==> default:             Source: /srv/jekyll
> ==> default:        Destination: /srv/jekyll/_site
> ==> default:       Generating...
> ==> default:                     done.
> {{< /highlight >}}
> 
> Then enter this:
> `vagrant provision`

For more details, see [the next post in the series](../2016-04-16-blogging-with-vagrant-docker-jekyll-shortcut-revisited).

<!--stackedit_data:
eyJoaXN0b3J5IjpbODEwMjMzMjQ2XX0=
-->
