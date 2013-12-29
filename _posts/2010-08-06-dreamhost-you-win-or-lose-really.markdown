---
author: admin
comments: true
date: 2010-08-06 13:19:43+00:00
layout: post
slug: dreamhost-you-win-or-lose-really
title: Dreamhost... you win... or lose really.
wordpress_id: 218
categories:
- ruby
- web
tags:
- dreamhost
- linode.com
- passenger
- rails 3
---

> You have already activated rack 1.1.0, but your Gemfile requires rack 1.2.1. Consider using bundle exec.



So with the impending release of Rails 3 there is a little dependency that was added. Rack 1.2.1. Dreamhost is using passenger which also requires a version of Rack. The problem is that it's 1.1.0. I'm pretty sure it's not going to be possible to get Rails 3 running on Dreamhost without the servers being upgraded...

If you're a Dreamhost customer please be sure to vote this suggestion up.
[Get Ready for Rails 3](https://panel.dreamhost.com/index.cgi?tree=home.sugg&category=_all&search=get%20ready%20for%20Rails%20)

Please be sure to file a support ticket as well.

For me, if this isn't fixed within the next few weeks I plan on moving to linode.com
