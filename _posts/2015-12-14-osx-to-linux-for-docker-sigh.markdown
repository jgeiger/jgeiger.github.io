---
author: jgeiger
date: 2015-12-14 21:36:46+00:00
layout: post
slug: osx-to-linux-for-docker-sigh
title: OSX to Linux for docker
---

So I've made my quarterly attempt to switch to linux ([mint](http://www.linuxmint.com/)) from OSX since you can use [docker](https://www.docker.com/) without boot2docker or a VM.

While I was able to get things working a bit better this time (highdpi, some keyboard shortcuts, etc) I was still stopped by a couple of issues.

First, Go in linux using [gb](http://getgb.io/) doesn't build static binaries without a lot of extra "gunk". This is a major pain compared to the OSX build, which because it's not linux, auto builds static binaries for linux.

Second, Docker doesn't seem to perform better. Running my rails database migrations on OSX goes very quickly. On linux it seems to just slowly chug along.

Performance aside, I think the Go building issue is too painful to overcome (in addition to all of the other linux related things)

We'll see what happens next quarter...
