---
author: admin
comments: true
date: 2011-06-07 18:48:45+00:00
layout: post
slug: serving-assets-in-rails-3-1-with-nginx
title: Serving assets in Rails 3.1 with nginx
wordpress_id: 245
categories:
- ruby
- web
---

I decided to create a site that uses the new Rails 3.1rc. I have a nice setup for nginx to serve my static assets and I was able to get it working with rails 3.1. There's nothing really too tricky since it's setup to do it, but you need to make sure that you pre-compile your assets when deploying. The only confusing bit is that you should remove all of your assets before running the rake task to make sure you're not duplicating files and/or serving the wrong thing. I did a bit of testing and found it was necessary to remove the files and re-compile before starting the server to get the correct files served. I've added a small snippet of code below to show how I did it. I also decided it wasn't necessary to symlink the files into the shared directory since they were getting removed on every deploy anyway. I'm sure there's a way to only delete the files that changed, but for now this works.



