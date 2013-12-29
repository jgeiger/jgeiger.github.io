---
author: admin
comments: true
date: 2010-04-06 19:28:45+00:00
layout: post
slug: mongodb-mongoid-will_paginate-and-sorting
title: mongodb, mongoid, will_paginate and sorting
wordpress_id: 193
categories:
- mongodb
- ruby
- web
tags:
- mongodb
- mongoid
- ruby
---

Had a bit of an issue with will_paginate and mongoid. I couldn't find an example of how to sort the pagination query and paginating without a defined sort order defeats the purpose.

`paginate(:page => page, :per_page => size, :sort => [['ontology_term_id', :desc], ['_id', :asc]])`

Instead of using "order" or "order_by" you can just use "sort" with an array of arrays.
