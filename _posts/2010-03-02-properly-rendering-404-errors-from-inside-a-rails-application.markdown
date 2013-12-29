---
author: admin
comments: true
date: 2010-03-02 16:43:31+00:00
layout: post
slug: properly-rendering-404-errors-from-inside-a-rails-application
title: properly rendering 404 errors from inside a rails application
wordpress_id: 175
categories:
- ruby
- web
tags:
- google
- rails
- ruby
---

I just migrated a site that had a bunch of links that have been in in the search engines for a while. Oddly it seems that the only thing hitting those links seem to be the crawlers themselves. I needed a way to invalidate those links, since I couldn't create a proper redirect because of changing IDs.

/records/show/12345 used to be valid, but has been replaced with the RESTful version /records/00123. The ID is now also meaningful instead of a MySQL generated id.

My first attempt was to just redirect to the 404 page.
`record = Record.find(params[:id]
rescue ActiveRecord::RecordNotFound
redirect_to("/404.html")`

But as I watched the logs, I noticed that this really wasn't right since it was still returning a 302 (redirect) and the a 200 (OK) code for those links. The crawlers were getting the instruction that you should just display the 404 page for those links. That might seem OK, but really I wanted them to get the 404 immediately and remove the page from their databases.

`record = Record.find(params[:id]
rescue ActiveRecord::RecordNotFound
render(:file => "#{RAILS_ROOT}/public/404.html", :layout => false, :status => 404)`

By rendering the 404.html directly and including the 404 status code, it should help to fix the situation.
