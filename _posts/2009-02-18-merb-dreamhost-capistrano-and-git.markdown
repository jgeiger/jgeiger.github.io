---
author: admin
comments: true
date: 2009-02-18 16:07:15+00:00
layout: post
slug: merb-dreamhost-capistrano-and-git
title: merb, dreamhost, capistrano and git
wordpress_id: 30
categories:
- ruby
tags:
- capistrano
- dreamhost
- git
- merb
---

I've been trying to use merb a bit more just to get prepared for the forthcoming rails/merb merger.

For what I've been doing, dreamhost has been really nice. Shell login, unlimited domains/transfer/storage with the ability to compile your own software has been a really nice thing for a low cost provider.

For this to work, you need to install git on your dreamhost account.
[Nice step by step walkthrough](http://craigjolicoeur.com/blog/2008/04/hosting-git-repositories-on-dreamhost/)
[Official Wiki Entry](http://wiki.dreamhost.com/Git)

I'm not going to get into the details of using git or merb, since there are resources out there already. From here I'm going to focus on the setups for capistrano, and how to set it up to deploy your merb application from a git repository on your dreamhost account.

Here is the main capistrano configuration file which lives inside the config directory of my merb application.

deploy.rb


The configure script includes the utility methods to create the shared directories, link the database.yml and [unpack the merb gems](http://splendificent.com/2008/12/merb-dependencies-and-bundler-conquered-screencast/).

deploy/configure.rb


Once this is setup properly, you can just type "cap deploy" and it will use the git repository setup on your dreamhost account. If you have setup SSH keys, you won't have to type your password. (You have setup SSH keys, right?)

There is one trick that I figured out, that may or may not be a good idea. For me right now, I'm ok with doing it.

Even if you have an SSH key setup to log into your shell account, it will still end up needing to SSH into itself to check out the git repository. (This is a tradeoff for the ability to move the git repository anywhere else, such as github.com, without changing a lot of the configuration) If you don't do this, you need to enter your password in the middle of the deploy. I just created another SSH key for the username, put it into ~/.ssh and added the id_rsa.pub into the authorized keys. The deploy now works with nothing more than "cap deploy".

