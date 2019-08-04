---
layout: post
title:  "Initial Thoughts on Ansible"
date:   2016-04-16 20:11:00
tags:
 - configuration management
 - ansible
comments: True
---

At this point, I've read many blogs that paint a very rosy picture of Ansible.

My initial experience was not so rosy. In fact, it was pretty frustrating. In future blogs, I'll provide examples. The purpose of this post is to record my initial impressions.

I become fixated on learning Ansible when I realized that I was starting to repeat the same patterns while maintaining servers, and worse, the steps that I took to maintain them were not being documented, so I'd have to remember how it went each time. This was manageable, up to a point. After that point, I started looking into configuration management systems.

I was working in a tight time-frame, one where I had not budgeted time for learning configuration management systems.

Our team currently uses Foreman to deploy servers within our department (in a Puppet fashion). The Foreman server is an undocumented mystery. And without it, apparently, new servers won't be deployed.

The pull-deploy architecture of Puppet felt like the wrong direction to me.

I kept hearing about how a few employees here favored Ansible, so I looked into it.

A book was available on Safari ( Up And Running With Ansible ), so I read it. It took me about a week to make it through the book. ( I'm a slow reader, and it was a quick read. )

I immediately liked the push ( optional pull ) deploy architecture, and especially liked that ad-hoc commands could be entered on the command line. I also liked the design of roles, and that the modules were implemented to be idempotent. It looked like it was going to be smooth sailing from the start.

That, however, was not the case.

I found the restrictions of entering the instructions in YAML+Jinja2 to be rather unintuitive. What this looked like, in practice, for me was to try to enter instructions with no quotes, at first, and try to run it. If that failed, I'd add single quotes, then double quotes, and maybe double parentheses. When that failed, I'd arbitrarily switch around the quotes. And when that failed, I'd get on IRC and ask what I was doing wrong.

The error messages that I was seeing from Ansible didn't seem to point to the line where the error occurred. It turns out, that I'd often be pointed to the beginning of the block of the instructions instead. It also happened that there would be useful information right at the beginning of the error, and right at the end would be the beginning of the block. There was plenty inbetween that was not useful and distracting.

It often seemed like I was ignored when I asked questions on IRC. But that seemed to get a little better with time. I was also a little unhospitable, at first. I was on a time-crunch, and the thing that stood in the way was not being able to interpret how I should be using quotes to correctly escape blocks of instructions.

Eventually, it became evident that one problem I was having was that I wasn't running the latest version of Ansible. It was an easy upgrade and a shell script so that I didn't need to remember the exact commands to pull the latest code down and getting it running in single instances of bash.

Another issue I was having was that Ansible seemed to sometimes treat json as an object, and sometimes as text. To make matters worse, I wasn't really sure how to determine what the structure was of the variable I was working with. That was very aggravating, as the json provided by Kubernetes is non-trivial, and I wanted to parse it.

When I figured out how to write my own custom modules, and then my own custom filters, Ansible suddenly became a very usable tool.

Now my process looks like this: Write the instructions without any quotes; if it fails, correctly identify the block where the error is occuring and comment out lines that are more complex, until the block itself doesn't error. Then add the lines back in, one at a time, until the error occurs. Add quotes / double-quotes and parentheses, if needed. If that fails, write a filter for what I'm trying to do instead, and then ask what I'm doing wrong on IRC.

Since I've now got a work-around, it's not an issue for it to take some time to get a response. Though, in truth, it seems the responses are coming pretty quickly these days.

I've since heard about Salt.

I don't really feel like I have time to learn another configuration management system, however, and Salt also uses a mast/minion architecture, which makes it seem like it would take longer to get running and learn.

I think Ansible is a good match for my grunge-style system administration tasks.

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTMzNzcxOTE1NV19
-->