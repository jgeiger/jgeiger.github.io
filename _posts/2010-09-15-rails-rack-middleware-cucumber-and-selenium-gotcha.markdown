---
author: admin
comments: true
date: 2010-09-15 15:02:28+00:00
layout: post
slug: rails-rack-middleware-cucumber-and-selenium-gotcha
title: Rails, Rack Middleware, Cucumber and Selenium gotcha
wordpress_id: 224
categories:
- jquery
- ruby
- web
tags:
- capybara
- cucumber
- rack
- rails
- selenium
---

I'm testing a web application that includes an [AJAX file uploader](http://github.com/valums/file-uploader) which works fine when I run it in the browser but fails when running a Cucumber feature with Selenium. To process the upload in Rails I'm using a [Rack middleware](http://github.com/newbamboo/rack-raw-upload) that will put the file into the params for me.

Looking at the parameter output I saw that the file was being sent to the server, but not processed. In my config.ru file I had `use Rack::RawUpload, :paths => ['/searches/upload']`to setup the middleware, but running "rake middleware" didn't show it as being active. It seems there are two ways to activate the middleware and I was using the one that requires the server to be started with the config.ru file. The Cucumber/Capybara/Selenium uses Webrick which doesn't start that way. So I moved my middleware initialization into initializers/middleware.rb and now things are working nicely.
`Qtlhighliter::Application.config.middleware.use(Rack::RawUpload, :paths => ['/searches/upload'])`

