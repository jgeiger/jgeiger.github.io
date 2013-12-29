---
author: admin
comments: true
date: 2010-02-09 14:49:18+00:00
layout: post
slug: bundler-and-future-updates
title: bundler and future updates
wordpress_id: 160
categories:
- ruby
- web
tags:
- bundler
- capistrano
- git
- rails 3
---

There was a [new post](http://yehudakatz.com/2010/02/09/using-bundler-in-real-life) about bundler which addresses a few of the issues that I've been having as part of my install.



> When running bundle install in the future, Bundler will use packed gems, if available, in preference to gems available in other sources.


This will be nice and solve my issue of re-installing all the gems on each deploy.



> You will want to run bundle unlock to remove the lock, then bundle install to ensure that the new dependencies are installed on your system, and finally bundle lock again to relock your application to the new dependencies.

We will add a command in a near-future version to perform all these steps for you (something like bundle install –relock).


This will also replace the unlock, update, lock steps I've got in the callbacks.rb for my deploy scripts. Not a huge deal, but fewer commands is better.

The combination of these two updates should speed up the deploy a lot.

