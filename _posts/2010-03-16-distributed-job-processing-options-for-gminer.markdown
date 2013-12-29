---
author: admin
comments: true
date: 2010-03-16 18:45:31+00:00
layout: post
slug: distributed-job-processing-options-for-gminer
title: distributed job processing options for GMiner
wordpress_id: 180
categories:
- ruby
- web
tags:
- cloud crowd
- gminer
- mcw
- rabbitmq
- rails
- redis
- resque
- ruby
---

I've been working on a project that requires the processing of a series of jobs. I had originally written my own system for doing this because I wanted to know more about how they work. After a time, I decided to modify it, and found that I had broken it. Instead of trying to fix it, I decided to see if there was anything out there that someone else had done that would work better for me.

**[Resque](http://github.com/defunkt/resque)**

My first attempt was to use resque. It worked, but as I started to scale things up, I ran into some issues that I didn't like.
It polled the DB a lot. While it was in memory, it was a lot of "do I have a message?" checks which seemed messy.
It wasn't fast. There was a lot of overhead. Things "felt" slow as they were running.
It was memory based. [Redis](http://code.google.com/p/redis/) will store data to the disk, but it's meant as an in memory system which gives it the speed. 

What I did like is that it worked. The jobs finished and there was a nice web interface to see what was going on.

**[Cloud Crowd](http://wiki.github.com/documentcloud/cloud-crowd/)**

I had looked at Cloud Crowd before and it seemed interesting. I like the web dashboard but it was also one of the biggest problems with Cloud Crowd. According to the authors, it was created to handle a small number of very expensive jobs. I have no doubt based on my experience that it would excel in that environment. My problems consists of a very large number of small fast jobs. Cloud Crowd ground to a halt pretty quickly. The dashboard was taking too much time to render which began to multiple the render time and eventually it needed to be turned off.
The other big issue I ran into was with how the workers processed their jobs. It wouldn't start another job until all of the other jobs it had created finished. If you have a scheduling job that launches 10 processing jobs, the system gets stuck waiting for the 10 processing jobs to finish before it can start another scheduling job. Again, it works very well. Everything gets done and you get a result string but it was slow.

**[RabbitMQ](http://www.rabbitmq.com/)**

I decided to figure out what was wrong with my system since it was working at one point. I'm using RabbitMQ as a message broker to pass the jobs back and forth between daemons running on linux machines. I believe my issue was caused by using a topic exchange with a key per worker. I was running into issues where some processors were picking up messages from the topic that were not assigned to their key. Once I realized this was happening I decided to go back to a queue per worker. I wanted to get away from that since originally I had been creating multiple queues in rabbit that never disappeared. I changed the queues to be exclusive. Exclusive means that only one client (processor) can read from that queue. It also makes the queue self-delete when the consumer disappears.

I'm attaching the code for my system below. I'll post more about how each of the parts works later. I hope to add a bit more control into the system, but as of now it's pretty self healing and very fast.

[http://github.com/mcwbbc/gminer_scheduler](http://github.com/mcwbbc/gminer_scheduler)
[http://github.com/mcwbbc/gminer_node](http://github.com/mcwbbc/gminer_node)
[http://github.com/mcwbbc/gminer_processor](http://github.com/mcwbbc/gminer_processor)
[http://github.com/mcwbbc/gminer_databaser](http://github.com/mcwbbc/gminer_databaser)

