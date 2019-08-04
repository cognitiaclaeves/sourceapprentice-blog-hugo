---
layout: post
title:  "Blogging with VDJG: Part 1 - Vagrant, Docker & Jekyll"
date:   2016-03-03 08:08:00
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

> This blog is set up to be able to add and view new entries offline ( as text files ), and then push changes into a source repository to trigger live site updates ( as website files ). I use a Jekyll Docker container running in Vagrant to take the site from text files to HTML.
> 
> My process was inspired by a blogging process demonstrated by Boyd Boyd Hemphill at a devops / docker / cloud meetup, which he published on [his blog](http://behemphi.github.io/github-pages/docker/2015/12/02/github-pages-with-docker.html)
> 
> This series covers the process I set up, in detail. In the first part, I cover everything short of publishing it live. In the second part, I cover publishing it live, and in the third part, I cover what it looks like when I create a new blog entry.

I like to show all my work.  But if you just want to get a blog up in a hurry with this method, I made a [short cut](../2016-03-08-blogging-with-vagrant-docker-jekyll-shortcut)!


( This post is currently in progress; there will be clean-up later. )

{{< highlight plaintext>}}
~/personal
➔ mkdir phusion-jekyll; cd phusion-jekyll

~/personal/phusion-jekyll
➔ git clone https://github.com/phusion/baseimage-docker.git
Cloning into 'baseimage-docker'...
remote: Counting objects: 1193, done.
remote: Total 1193 (delta 0), reused 0 (delta 0), pack-reused 1193
Receiving objects: 100% (1193/1193), 1.48 MiB | 1.57 MiB/s, done.
Resolving deltas: 100% (699/699), done.
Checking connectivity... done.

~/personal/phusion-jekyll
➔ cd baseimage-docker

personal/phusion-jekyll/baseimage-docker on master
➔ ls
CONTRIBUTING.md Makefile README_zh_tw.md install-tools.sh
Changelog.md README.md Vagrantfile test
LICENSE.txt README_ZH_cn_.md image tools

personal/phusion-jekyll/baseimage-docker on master
➔ vagrant up
{{< /highlight >}}


> Warning: The next line causes vagrant to allow running VM instance to access the files on your local machine. Know what you're doing when you give any VM or container access to your local machine.

For the sake of convenience, I want a folder in the VM to directly reference my work folder (future github) folder, so I add this line:

```config.vm.synced_folder "data", "/home/vagrant/data"```

{{< highlight plaintext>}}
➔ tail -6 Vagrantfile
    config.vm.provision :shell, :inline => $script
  end

  config.vm.synced_folder "data", "/home/vagrant/data"

end
{{< /highlight >}}

Then I create the data folder and restart the vagrant box:

{{< highlight plaintext>}}
personal/phusion-jekyll/baseimage-docker on master [!]
➔ mkdir data; vagrant halt; vagrant up

==> default: Attempting graceful shutdown of VM...

Bringing machine 'default' up with 'virtualbox' provider...
...
{{< /highlight >}}

My new folder is at the top of this list:

{{< highlight plaintext>}}
==> default: Mounting shared folders...
default: /home/vagrant/data => /Users/jno/personal/phusion-jekyll/baseimage-docker/data
default: /vagrant/baseimage-docker => /Users/jno/personal/phusion-jekyll/baseimage-docker
default: /vagrant => /Users/jno/personal/phusion-jekyll/baseimage-docker
{{< /highlight >}}

Next, I run the following in the vagrant session, to build the initial files:

{{< highlight plaintext>}}
cd data
docker run \
  --interactive \
  --label=jekyll \
  --publish 4000:4000 \
  --rm \ 
  --tty \
  --volume=$(pwd):/srv/jekyll 
  jekyll/jekyll:pages jekyll new . --force
{{< /highlight >}}

> The volume specification above is similar to the shared folder mount earlier, except for containers. At this time, this is considered more dangerous, by some. In this case, it's pretty safe, as it only allows the docker container direct access to a path in the VM, and not your localhost.

I was going to include a screenshot here of what it should look like when the above command is run, but I spent the time making the [short cut](../2016-03-08-blogging-with-vagrant-docker-jekyll-shortcut) instead.

.. and create this file (phusion-jekyll/baseimage-docker/exec-jekyll.sh), to run the jekyll container:

{{< highlight docker>}}
cd /home/vagrant/data
docker stop jekyll_runtime 2> /dev/null
docker rm -v jekyll_runtime 2> /dev/null
docker run \
    --env FORCE_POLLING=true \
    --env JEKYLL_ENV=development \
    --env VERBOSE=true \
    --label=jekyll \
    --name=jekyll_runtime \
    --publish "0.0.0.0:4000:80" \
    --rm \
    --volume="$(pwd):/srv/jekyll" \
    jekyll/jekyll:pages jekyll build --watch
{{< /highlight >}}

... and make the file executable:


{{< highlight plaintext>}}
➔ chmod +x exec-jekyll.sh
{{< /highlight >}}

To make the webserver in the container accessible, and to execute my new script, I add these lines to the Vagrantfile that I edited before:

{{< highlight plaintext>}}
...

  config.vm.synced_folder "data", "/home/vagrant/data"
  config.vm.network :forwarded_port, guest: 4000, host: 4000
  config.vm.provision "shell", path: "exec-jekyll.sh"
end
{{< /highlight >}}

```vagrant provision``` runs the script:

{{< highlight plaintext>}}
personal/phusion-jekyll/baseimage-docker on master [!]
➔ vagrant provision
==> default: Running provisioner: shell...
        default: Running: /var/folders/9s/320v29913qs9j6kzxnqv7smclw01rh/T/vagrant-shell201
60302-97040-1s32frt.sh
==> default: stdin: is not a tty
==> default: jekyll_runtime
==> default: Github does not allow user dependencies.
==> default: Configuration file: /srv/jekyll/_config.yml
==> default: Source: /srv/jekyll
==> default: Destination: /srv/jekyll/_site
==> default: Generating...
==> default: done.
==> default: Auto-regeneration: enabled for '/srv/jekyll'
{{< /highlight >}}

Now, I can browse to: http://localhost:4000, and click on the "Welcome to Jekyll" link.

This link was generated from data/_posts/[date]-welcome-to-jekyll.markdown

I switch to another terminal and edit the file locally:

{{< highlight yaml>}}
---
layout: post
title: "Welcome to Jekyll!"
date: ... 
categories: jekyll update
---
You’ll find this post in your `_posts` directory. ...
{{< /highlight >}}

I change the above to:

{{< highlight yaml>}}
---
layout: post
title: "Welcome to Jekyll!"
date: ... 
categories: jekyll update
---
You’ll find this SAMPLE post in your `_posts` directory. ...
{{< /highlight >}}

and when I save the file, I see activity in the previous terminal session:

{{< highlight plaintext>}}
...
==> default: done.
==> default: Auto-regeneration: enabled for '/srv/jekyll'
==> default: Regenerating: 1 file(s) changed at 2016-03-02 23:47:21
{{< /highlight >}}

Finally, when I refresh the localhost:4000, it's updated! 

When I'm finished updating my site, I take the vagrant box down:

{{< highlight plaintext>}}
==> default:       Regenerating: 1 file(s) changed at 2016-03-03 15:00:13
==> default: ...done in 0.860794742 seconds.
^C==> default: Waiting for cleanup before exiting...
^C==> default: Exiting immediately, without cleanup!

personal/phusion-jekyll/baseimage-docker on master [!?]
➔ vagrant halt
==> default: Attempting graceful shutdown of VM...

personal/phusion-jekyll/baseimage-docker on master [!?]
{{< /highlight >}}

That's the process. Be sure to check out my shortcut for a handy script that does all the work for you!

I actually do a little more work to get the switchable theme in my static website. This work amounts to mangling the generated files with the use of a bash and a python script.

For the next blog in this series, I'll post how to easily work github pages into this, and then my steps to create a new blog entry, after all the setup is done.

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTgxNTU0ODQ0MV19
-->
