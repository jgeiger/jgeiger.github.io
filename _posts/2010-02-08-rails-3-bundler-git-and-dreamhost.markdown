---
author: admin
comments: true
date: 2010-02-08 22:18:57+00:00
layout: post
slug: rails-3-bundler-git-and-dreamhost
title: rails 3, bundler, git and dreamhost
wordpress_id: 158
categories:
- ruby
- web
tags:
- bundler
- capistrano
- dreamhost
- git
- rails 3
---

**UPDATE: How to setup your Dreamhost shell account [update available here](http://blog.joeygeiger.com/2010/05/17/i-beat-dreamhost-how-to-really-get-rails-3-bundler-and-dreamhost-working/)**.

Now that rails 3 has hit beta, I decided to see if I could get it running on my dreamhost account. I'm already running a few rails applications using bundler 0.8.1, so the forced upgrade to 0.9.3 (as of this writing) is actually a point of pain, since both versions cannot co-exist.

If you're not running an old version of bundler, this should be an easy update. If you are, it gets complicated to the point that for now, it's not worth updating since bundler 0.9.3 still seems to have issues with rails 2.3.x.

The first thing I did was to install the bundler gem in your usual location for dreamhost. This isn't going to be a "how do I set up rails and custom gems for dreamhost?" post as those resources exist on the web already.

On dreamhost:
`gem install bundler`

Now you want to setup your rails 3 application, get it into a git repository and push it there. The main point of this post is to include my deploy files which are based on the [github 'git' deploy strategy](http://github.com/blog/470-deployment-script-spring-cleaning), which is really nice. I've added in some code for [jammit](http://documentcloud.github.com/jammit/) as my asset packager, and some custom bundler callbacks.

I've included a gist below with my deploy code. Make sure the files are in the proper directories.


