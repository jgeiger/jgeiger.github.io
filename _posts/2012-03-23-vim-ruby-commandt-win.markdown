---
author: admin
comments: true
date: 2012-03-23 03:22:25+00:00
layout: post
slug: vim-ruby-commandt-win
title: Vim + Ruby + CommandT = win
wordpress_id: 263
categories:
- ruby
- web
tags:
- ruby
- vim
---

So I've been trying to get vim working on my macbook with the command-t plugin for file searching. I spent quite a while trying to get it working a while ago and finally did a really simple thing and it just worked.


    
    cd ~
    git clone git@github.com:jgeiger/vim-config.git ~/.vim
    cd ~/.vim
    git submodule update --init
    ln -s ~/.vim/vimrc ~/.vimrc
    sudo mv /usr/bin/vim /usr/bin/vim72
    brew install https://raw.github.com/Homebrew/homebrew-dupes/master/vim.rb
    cd .vim/bundle/command-t/ruby/command-t/
    /usr/bin/ruby extconf.rb
    



I'm using rbenv with ruby 1.9.3-p125 as my main ruby, but you need to make sure that you compile command-t against whatever ruby vim as compiled with. The homebrew-dupes forumla uses the system ruby (which lives at /usr/bin/ruby) and even if you have rbenv global set to another ruby, you can always directly use the system ruby.

Thanks to:
[https://github.com/Casecommons/vim-config](https://github.com/Casecommons/vim-config)
[https://github.com/Casecommons/casecommons_workstation/blob/master/recipes/vim.rb](https://github.com/Casecommons/casecommons_workstation/blob/master/recipes/vim.rb)
