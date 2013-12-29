---
author: admin
comments: true
date: 2010-05-17 14:38:18+00:00
layout: post
slug: i-beat-dreamhost-how-to-really-get-rails-3-bundler-and-dreamhost-working
title: I beat Dreamhost. How to really get rails 3, bundler and dreamhost working.
wordpress_id: 203
categories:
- ruby
- web
tags:
- bundler
- dreamhost
- git
- rails 3
- ruby
---

Please check out [my earlier post](http://blog.joeygeiger.com/2010/02/08/rails-3-bundler-git-and-dreamhost/) so you can get the whole git/capistrano setup working as well.

So I've been trying to get rails 3 running with bundler on Dreamhost for a while. I've had a few posts on here about how to do it. In the end, they didn't work completely. I've sent requests into Dreamhost to upgrade rubygems to 1.3.6 so the newest versions of bundler would work. I was told 'No' but go to [this wiki site](http://wiki.dreamhost.com/RubyGems).

I wasn't too happy about that since the top of the page has a big warning 'DON'T DO THIS'. If you're here looking at this you probably have the tech knowhow to do this and realize the world won't end when you do.

So here's the step by step directions for how I got it working.
You can check out the original wiki instructions at [http://wiki.dreamhost.com/RubyGems](http://wiki.dreamhost.com/RubyGems).

Add this to your .bashrc
This will setup your shell to use local gems installed in your .gems directory, setup the path to check there first and opt/bin as well.  Next we need to install a newer version of rubygems. 

This will get rubygems installed and make sure you run your version before dreamhost's. You then install bundler and rake. These are the only two gems I install in the system as I prefer to have all of my apps use their own gem versions. Putting everything into system is a big mess and a dependency nightmare on updates.

Next we need to make sure your app is setup to use the bundler gem. You need to modify your environment.rb and boot.rb

Make sure you change the application name to your name. Really you're only adding the single line for the GEM_PATH 

I was using the suggestions in the wiki but I eventually figured out that Dreamhost wasn't properly picking up my gems even with the changed GEM_PATH. Adding the 'Gem.clear_paths' to boot.rb allowed the gems to be seen. This is what finally cracked the problem.

Hopefully this works for you.
