---
author: admin
comments: true
date: 2009-09-21 18:02:20+00:00
layout: post
slug: why-ruby-on-rails-isnt-ready-for-ruby-1-9-x
title: Why Ruby on Rails isn't ready for Ruby 1.9.x
wordpress_id: 117
categories:
- ruby
- web
tags:
- rails
- ruby 1.9.1
---

I've spend the better part of the last two weeks dealing with upgrading my operating system to Snow Leopard. Honestly, I haven't seen much difference, but I believe that there is an improvement. Things just _feel_ faster.

One of the big changes I was going to make was moving all my development to ruby 1.9.1, since it's now the preferred ruby as stated by ruby-lang.org.

I was able to install it, add gems and such based on various tutorials I read on the net. My problem started as soon as I tried to deal with rails 2.3.4 and textmate. Time after time, I tried to run tests, and ended up with the same issue. 

**invalid multibyte character**

Here's a test for you. Fire up an irb shell using ruby 1.9.1.


    
    
    irb
    control      = %Q|\x00-\x1f\x7f-\xff|
    CONTROL_CHAR  = /[#{control}]/n
    



The next thing you should see is:


    
    
    ArgumentError: invalid multibyte character
    	from (irb):2
    	from /usr/local/bin/irb:12:in `<main>'
    



Those two lines are taken from actionmailer-2.3.4/lib/action_mailer/vendor/tmail-1.2.3/tmail/utils.rb:115-117

That's the tmail-1.2.3 that's vendored in the gems used for rails. A few searches on the net and you find:

[http://github.com/mikel/tmail](http://github.com/mikel/tmail)

The first line of text in the readme?
**Note... as of 1.2.5, TMail is not compatible with Ruby 1.9.1.**

Huh.

So, my guess is, anyone who's using rails with ruby 1.9.1 has just been getting lucky up to this point. I was not so lucky, and that's why I've moved back to ruby 1.8.7.  I'm a lot happier right now.

