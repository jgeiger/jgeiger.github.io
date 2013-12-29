---
author: admin
comments: true
date: 2010-08-06 17:18:12+00:00
layout: post
slug: bundler-and-deploying-difficult-to-build-gems
title: Bundler and deploying difficult to build gems
wordpress_id: 221
categories:
- ruby
- web
tags:
- bundler
- deploy
- mysql
---

With Bundler 1.0.0.rcx you can specify the build options for gems. This is nice because certain gems (mysql, rsruby) are sometimes painful to build.

There is a bit of manual labor here which could be automated in some way you'd think, but for now it does work and that's good enough for me.




	
  1. Login as your deploy user.

	
  2. Go to the deploy current directory where there is a Gemfile.

	
  3. type 'bundle config build.mysql --with-mysql-config=/usr/local/bin/mysql_config'



This will now append the commands to the end of the build command for mysql allowing it to build when you deploy your application. It works quite well and I think it's a simple solution for one of the biggest issues I had with trying to use Bundler in production.

The 'bundle config' step also creates a .bundle/config in the user's home directory that will then use those options for all bundle builds of that gem on the server. So if you're installing 4 different apps on the server, you'll only have to setup that command once and bundler will pick it up on each deploy.

Some examples
`bundle config build.mysql --with-mysql-config=/usr/local/bin/mysql_config
bundle config build.rsruby --with-R-dir=/usr/local/lib/R/
bundle config build.rmagick --no-ri --no-rdoc
`

To view the options you can also type 'bundle config' alone in a directory that contains a Gemfile. (Not sure why it needs a Gemfile to exist, but again, not a hard requirement)
