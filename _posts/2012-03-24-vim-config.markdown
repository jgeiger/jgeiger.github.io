---
author: admin
comments: true
date: 2012-03-24 23:24:04+00:00
layout: post
slug: vim-config
title: vim config
wordpress_id: 267
categories:
- ruby
tags:
- ruby
- vim
---

I've been working on a project which has a really nice set of vim plugins with a decent configuration. I've been trying to send in a few patches but it was a bit of a pain to use mine but keep it updated with the main repo. A bit of searching gave me a nice setup.

This clones my fork and also adds the parent as the upstream remote.

    
    cd ~
    git clone git@github.com:jgeiger/vim-config.git ~/.vim
    cd ~/.vim
    git submodule update --init
    ln -s ~/.vim/vimrc ~/.vimrc
    git remote add upstream https://github.com/Casecommons/vim-config.git
    



Now if you add this to your .gitconfig you can do an easy **git pu** to pull in changes from both branches.

    
    [alias]
      pu = !"git fetch origin -v; git fetch upstream -v; git merge upstream/master"



Thanks
[http://gitready.com/intermediate/2009/02/12/easily-fetching-upstream-changes.html](http://gitready.com/intermediate/2009/02/12/easily-fetching-upstream-changes.html)

