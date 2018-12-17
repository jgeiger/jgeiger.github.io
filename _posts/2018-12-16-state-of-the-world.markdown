---
author: jgeiger
date: 2018-12-16 19:00:00+00:00
layout: post
slug: state-of-the-world
title: State of the world
---

So it seems like a good time for a biennial update to this blog.

Some of my previous posts included information about switching from OSX to Linux for development. Interestingly enough, I've been using Mint for about two years and haven't looked back. I've also converted all my daily drivers to Mint.

I found that most of the issues that I ran into just don't seem to exist. Another surprising point is that Docker when used in OSX has become shockingly bad. It's pretty much unusable for development due to [really bad file sync issues](https://docs.docker.com/docker-for-mac/osxfs-caching/) and a new [memory leak](https://github.com/docker/for-mac/issues/3232) [(leaks?)](https://github.com/moby/hyperkit/issues/231) that's really just being ignored.

The software I was worried about missing has become a non-issue since there are some decent alternatives ([Hiri](https://www.hiri.com/) for mail, [DBeaver](https://dbeaver.io/) for database work)

Also, building Go on Linux works fine. A nice Makefile and everything works pretty easliy in a monorepo and for creating Docker containers.