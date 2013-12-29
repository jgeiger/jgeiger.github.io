---
author: admin
comments: true
date: 2009-02-25 22:44:01+00:00
layout: post
slug: rabbitmq-and-monit
title: rabbitmq and monit
wordpress_id: 69
categories:
- web
tags:
- monit
- rabbitmq
---

I was looking around trying to figure out how to get rabbitmq working with monit. First I had to get rabbitmq working at all.

It's much easier if you decide to use packages from apt or yum, since many of the dependencies are taken care of for you and the startup scripts are added to /etc/init.d automatically.

If you want to build it from scratch, here are a couple of good resources.
[
rabbitmq on OSX](http://hopper.squarespace.com/blog/2008/11/15/how-i-install-rabbitmq-on-osx.html)
[rabbitmq main generic unix
](http://www.rabbitmq.com/install.html#generic-unix)

The important line in this, is "make -j run". For some reason this isn't mentioned anywhere in the generic unix install, but I needed to do it before I could start the server with rabbitmq-server.


**If you didn't install the packages, you need to create an /etc/init.d/rabbitmq file.**
If you did install the packages, you will need to edit your file to include the line 
`sed 's/.*,\(.*\)\}.*/\1/' /var/lib/rabbitmq/pids > /var/run/rabbitmq.pid`
since monit needs a pid file that only contains the number. You add it right above the echo SUCCESS line in the start_rabbitmq function.



**And then you need to create a monitrc file.**

