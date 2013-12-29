---
author: admin
comments: true
date: 2012-07-04 05:04:21+00:00
layout: post
slug: ruby-1-9-x-and-american-dates
title: Ruby 1.9.x and American dates
wordpress_id: 295
categories:
- ruby
- web
tags:
- postgresql
- ruby
---

I'm not sure how I didn't run into this before but if you have a date field in ruby 1.9.x it will not parse it in the American format (mm/dd/yyyy). Combined with postgresql turning an invalid date to nil, it makes for some fun debugging.

I usually set dates in my factories to "1/1/2000" but from now on it will be "12/31/1999" so I can catch this issue way sooner.

Also check out [https://github.com/jeremyevans/ruby-american_date](https://github.com/jeremyevans/ruby-american_date) which will solve the issue quickly. (Note, this seems to break using non-American dates (dd/mm/yyyy)
