---
author: admin
comments: true
date: 2012-04-21 03:22:58+00:00
layout: post
slug: capistano-and-bundler-working-for-a-git-deploy
title: Capistano and bundler working for a git deploy
wordpress_id: 285
categories:
- ruby
- web
tags:
- bundler
- capistrano
- github
- ruby
---

I've been using the "git" deploy that [github talked about so long ago](https://github.com/blog/470-deployment-script-spring-cleaning) for a while now. I finally got around to deploying something new and decided to use the built in bundler code for capistrano. A long time ago I had to fight with it and eventually gave up. I think they finally fixed it so you can override "current_release" which lets you work in a strategy that doesn't force releases on you.

    
    set :application, "myappname"
    set :bundle_roles, "/www/#{application}/current"



Adding the above lines somewhere in your deploy (change as needed) will allow you to override the default and get the deploy working.

It's interesting that they don't list "current_release" as an option you can change but if you look at the code it's being pulled in just like all the others.

