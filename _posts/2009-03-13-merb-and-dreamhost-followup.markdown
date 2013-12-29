---
author: admin
comments: true
date: 2009-03-13 14:50:42+00:00
layout: post
slug: merb-and-dreamhost-followup
title: merb and dreamhost followup
wordpress_id: 85
categories:
- ruby
- web
---

If you deploy a merb application on dreamhost using passenger, be sure you remove the .htaccess file inside the public directory. It seems to cause some issues when you go to any other action besides the root.
