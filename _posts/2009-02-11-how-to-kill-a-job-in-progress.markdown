---
author: admin
comments: true
date: 2009-02-11 16:18:23+00:00
layout: post
slug: how-to-kill-a-job-in-progress
title: How to kill a job in progress
wordpress_id: 28
tags:
- mcw
- rails
- ruby
- vipdac
---

I'm building a web application the analyze large data sets. The simplified process is: upload a data set, split it into multiple chunks, process the chunks and then zip the results together.

While you can kill a job in progress right now, all it's really doing is removing it from the database. The queue is still clogged full of tasks that need to complete for a job that doesn't exist anymore. I'm referring to this as a push model, since I've pushed all the tasks onto the queue and the workers consume them as fast as they can. The problem lies in the fact that to remove the job messages from the queue, you need to kill the queue. (Using [beanstalkd](http://xph.us/software/beanstalkd/) right now) This is fine if you have a single job on the queue, and you can ssh into the server, but it's still a pain.

After some thought, I'm going to try to impliment a pull model. Each worker will announce it's available to the head node when it starts up. The head node will note it's existence in a 'workers' table, with the status of available. When a job gets submitted, the head node looks to see if any workers are available. If so, it drops the message onto the worker queue. It doesn't matter if the worker that was available gets the job, just that there was one available. When the worker pulls the task off the queue, it sends a message back to the head queue saying that it's now busy. The process continues once we have a series of tasks backing up on the head node, where the head will see if we have available workers, and if so, drop a task onto the worker queue.

What we gain from this is the ability to kill the job, and all associated tasks on the head node before they're put into the worker queue. The tasks that are in process will still complete since we can't go in and stop them, but that's ok. Once they've all finished, we clean up the working files, and remove the job and other valid jobs can continue on without any issues.

Another gain is the ability to pause jobs, or better assign priorities. We don't want a job that's 95% done to be trumped by a higher priority job, since the system would think it's stuck.
