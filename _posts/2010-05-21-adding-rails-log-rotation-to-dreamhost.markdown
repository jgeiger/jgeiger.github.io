---
author: admin
comments: true
date: 2010-05-21 19:12:04+00:00
layout: post
slug: adding-rails-log-rotation-to-dreamhost
title: adding rails log rotation to dreamhost
wordpress_id: 210
categories:
- ruby
- web
tags:
- dreamhost
- logrotate
- rails
- ruby
---

While Dreamhost may rotate the apache logs for you there is nothing automatic to rotate the rails production logs. This may not be an issue since you have "unlimited" disk space but it's a good idea anyway.

You need to install logrotate since it doesn't exist by default on the server and then place it in a location where it can be run. You also need to create the configuration file and status files. Once that is set up, you can install a cron job via the Dreamhost panel.







Now it should be rotating your application logs nightly. You can add more sites to the conf file as needed.
