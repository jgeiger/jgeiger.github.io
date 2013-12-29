---
author: admin
comments: true
date: 2010-02-24 22:02:48+00:00
layout: post
slug: bundler-times-two
title: bundler times two
wordpress_id: 171
categories:
- ruby
tags:
- bundler
- rails
- rails 3
- ruby
---

I wish they would have made a bigger deal about this, but it seems that bundler now has two different gems.

bundler08 is for bundler 0.8.4 and such, which plays really well with rails 2.3.5

bundler is for bundler 0.9.x and beyond which plays well with rails 3 (and rails 2.3.5 if you can get it to work...)

This is a really good thing because you can now install both of them at the same time and the warning that you must un-install all previous versions of bundler is now moot. Really helpful if you're running on dreamhost with mixed rails 2/3 sites.
