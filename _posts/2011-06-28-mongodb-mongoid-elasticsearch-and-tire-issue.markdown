---
author: admin
comments: true
date: 2011-06-28 18:18:20+00:00
layout: post
slug: mongodb-mongoid-elasticsearch-and-tire-issue
title: MongoDB, mongoid, elasticsearch and tire issue
wordpress_id: 251
categories:
- mongodb
- ruby
tags:
- elasticsearch
- mongodb
- mongoid
- ruby
---

I just setup a quick app with MongoDB, mongoid, elasticsearch and the tire gem. The system seems to work nicely but there is an issue you should be aware of. Since tire uses the 'after_save' callback to insert data into elasticsearch it will be pretty automatic, which for the most part is nice.

The issue occurs when you have a unique index in mongodb but don't have a 'validates_uniqueness_of' in your model. With this combination and two similar records, mongo will reject the new record, but it will still insert into elasticsearch giving you a record in elasticsearch that doesn't exist in mongodb. This is potentially a nasty bug.

The quick fix is to make sure that any unique index in your database also includes the 'validates_uniqueness_of' validator in your model.
