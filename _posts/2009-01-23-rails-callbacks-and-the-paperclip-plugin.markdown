---
author: admin
comments: true
date: 2009-01-23 20:28:54+00:00
layout: post
slug: rails-callbacks-and-the-paperclip-plugin
title: Rails callbacks and the Paperclip plugin
wordpress_id: 10
tags:
- rails
---

I had an issue with adding my own before_destroy hook to remove some files from S3 after deleting a record. Paperclip has a before_destroy hook that removes the attachments, and I was using the filename it provides to delete the remote files. It seems that the order of the before_destroy lines is important (which makes sense) but you need to be aware if it exists in a plugin you're using.

In the case of Paperclip, I needed to put my custom hook before the has_attached_file declaration.

This comment helped me out [http://apidock.com/rails/ActiveRecord/Callbacks/before_destroy#43-Where-you-declare-before-destroy-matters](http://apidock.com/rails/ActiveRecord/Callbacks/before_destroy#43-Where-you-declare-before-destroy-mattersre-before-destroy-matters)
