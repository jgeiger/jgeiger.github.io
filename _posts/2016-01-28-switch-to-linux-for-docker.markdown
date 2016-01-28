---
author: jgeiger
date: 2016-01-28 07:29:46+00:00
layout: post
slug: switch-to-linux-for-docker
title: Switch to Linux for Docker
---

This is a follow up to my previous post where I made an attempt to switch to [linux mint](http://www.linuxmint.com/) to make my [docker](https://www.docker.com/) use easier.

I started over and this time was able to get fully switched over.

One of the main issues was building Go applications for Linux as static binaries. My solution was to ditch [gb](http://getgb.io/) and start using a [Makefile](https://gist.github.com/jgeiger/dae5bc65860c93881fb3) that included some specific commands. After doing this, things are working very nicely and I'm quite happy.

Other changes included using

* [Terminator](http://gnometerminator.blogspot.com/p/introduction.html) for my terminal
* [Scudcloud](https://github.com/raelgc/scudcloud) for my Slack client
* [Thunderbird](https://www.mozilla.org/en-US/thunderbird/) with [ExQuilla](https://addons.mozilla.org/en-US/thunderbird/addon/exquilla-exchange-web-services/) for my Exchange mail client
* [govendor](https://github.com/kardianos/govendor) for my Go vendoring strategy. I really like how this works.

The other big issue was mysql performance issues. It seems there's a [bug](http://bugs.mysql.com/bug.php?id=46959) in mySQL when running on ext4 file systems.
I was able to [_add_ some options](https://mariadb.com/blog/what-best-linux-filesystem-mariadb)

```console
noatime,data=writeback,commit=60,nobarrier
```
 to my /etc/fstab file when mounting the ext4 partitions and all the performance issues disappeared. It's now actually faster than the OSX version.
