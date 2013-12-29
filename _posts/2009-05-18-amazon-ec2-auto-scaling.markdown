---
author: admin
comments: true
date: 2009-05-18 13:43:34+00:00
layout: post
slug: amazon-ec2-auto-scaling
title: Amazon EC2 Auto Scaling
wordpress_id: 96
---

> **Q: How does Auto Scaling decide which Amazon EC2 instance in the Auto Scaling Group to terminate when the scaling condition is met?**
    Auto Scaling will randomly pick and terminate any Amazon EC2 instance from your Auto Scaling Group if the scaling condition is met.



Really? Random? You couldn't pick the one that was the closest to the 1 hour cutoff and remove it? So, the one I just launched, that I've used for 5 minutes, but paid for my full hour, can get randomly deleted before the one I've used for 57 minutes?

That seems like it needs a re-write to add some intelligence.

