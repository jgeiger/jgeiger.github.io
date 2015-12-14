---
author: jgeiger
date: 2015-10-13 21:36:46+00:00
layout: post
slug: kubernetes-and-docker
title: Kubernetes and Docker
---

It's been a bit harder getting [Kubernetes](http://kubernetes.io/) working with a docker image and docker machine, but here's a setup using the most recent(1.0.6) docker images.

I'm using [my fork of dinghy](https://github.com/jgeiger/dinghy) and the [Docker toolbox](https://www.docker.com/toolbox).

My fork removes the dependency on brew's docker and docker-machine.

Command to SSH pipe docker-machine. Replace dinghy with your machine's name.

```console
ssh -i ~/.docker/machine/machines/dinghy/id_rsa docker@$(docker-machine ip dinghy) -L 8080:localhost:8080
```
Copy/paste the docker-compose.yml file below into a directory and run docker-compose up.

Just don't name the directory k8s since it seems to cause some issues when starting up. Compose names the images like k8s\_master\_1 and k8s seems to be reserved in Kubernetes.

#### docker-compose.yml
```yaml
etcd:
  image: gcr.io/google_containers/etcd:2.0.13
  net: "host"
  command: /usr/local/bin/etcd --addr=127.0.0.1:4001 --bind-addr=0.0.0.0:4001 --data-dir=/var/etcd/data
master:
  image: gcr.io/google_containers/hyperkube:v1.0.6
  name: "master"
  net: "host"
  volumes:
    - /var/run/docker.sock:/var/run/docker.sock
  command: /hyperkube kubelet --api_servers=http://localhost:8080 --v=2 --address=0.0.0.0 --enable_server --hostname_override=127.0.0.1 --config=/etc/kubernetes/manifests
proxy:
  image: gcr.io/google_containers/hyperkube:v1.0.6
  net: "host"
  privileged: true
  command: /hyperkube proxy --master=http://127.0.0.1:8080 --v=2
```
