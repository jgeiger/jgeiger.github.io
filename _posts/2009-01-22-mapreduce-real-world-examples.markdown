---
author: jgeiger
date: 2009-01-22 16:34:50+00:00
layout: post
slug: mapreduce-real-world-examples
title: Map/Reduce real world examples
tags:
- aws
- ec2
- github
- google
- map/reduce
- mcw
- vipdac
---

Why is it every example of Map/Reduce is counting words in a big textfile? Isn't there someplace offering something of substance?

Also, the examples also seem to gloss over the fact that you need to get the data to the nodes in order to process it. Google's got GFS hooked up to all 1000+ nodes, but how do you pull that off on EC2? EBS is only hooked to one node at a time...

I'm working on a system to do large scale analyses, and hopefully will be posting updates on the issues I've found.

You can follow the project at [http://github.com/mcwbbc/vipdac/tree/master](http://github.com/mcwbbc/vipdac/tree/master)
