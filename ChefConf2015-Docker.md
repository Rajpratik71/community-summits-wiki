Chef + Docker: replace or augment or "other"?

Opening question:  What do people currently do?



We have a few notes here: https://public.pad.fsfe.org/p/Containerdays-Austin-Chef-Containers

Why use docker at all?
+ It solves the "works on my machine but not in production" problem.  literally the same condainer gets run on staging and production.  same artifacts, etc
  + assuming you have the same kernel
  + could actually create this issue, if dev kernel is different from prod kernel and is missing a feature (noted by Daniel Steen (tradeify))
+ could theoretically do with VMs, but is much faster to do with docker.  milliseconds vs minutes
+ manage the host with chef, and lays down the infrastructure to run containers (one way to do it, done by FIXME)
  + means that you don't have to replace all your AWS instances (slow process), just the containers (quick process)
  + chef can do things to the machine without having to muck with the application
+ jenkins slaves (but not the master)
+ value knowing that the docker image is always the same, vs a chef converge that may or may not have worked perfectly every time

might want to have a jenkins job to build docker images, tag them as staging/prod/etc

Running chef within a docker image. and then converging it, is that a good way to run?
+ yes, can do that, some people do but have a long spin-up time of 30 seconds (or minutes) vs milliseconds
+ jenkins job to build artifact, create container, run chef to converge, and spit out a container (instead of an AMI).  If all tests succeed, win.  Used by tradeify

If you've already solved the 80/20, docker may give you the 20.
The 20 controls dependencies, ie you don't have to worry about repos going down.  If you build them in 100% to the docker image, you're golden.
There can be an annoyingly high failure rate for external packages. (even 5%).  adds time.  if you have the failure during build, that's more better than having the same problem at deploy time.  win with docker.


What about levareging something like CoreOS as the base image for the containers, and leveraging chef to build out the containers and ship them out?

If you build AMI with chef, then spin-up is quick for EC2 instance.  Docker pull can be slow for large images, but then start up quickly.

Random note: may want to disable notifies if you have chef on the host, otherwise all your docker instances might restart at once

Docker doesn't change how you send your logs (to logstash, etc).  nxlog works to get logs out of containers.

at large scale, btrfs et al fall over   devicemapper sometimes doesn't have the device mapped in time.  aufs is horrible.  race conditions happen a lot if docker images spin up and down a lot.
btrfs can break memory model in that each container eats up a lot of memory
50 instances x 1000 containers = problems

if you're a go shop, docker is a walk in the park

service discovery:
+ There was a good meetup in austin:  http://www.meetup.com/Docker-Austin/events/219194587/
+ consul, etcd
+ smartstack it'll be nice to have a link for this
  + cleint-side load balancing through HAProxy
  + fast failover
  + works great for microservices, always know port on what server
  + random note:  zookeeper is easy to set up and you can forget about it, it just runs.

Attendees:
    JJ Asghar jj@chef.io
    Ross Dickey  rdickeyvii@gmail.com
    Daniel Steen  daniel@steenfamilies.com
    Robb Kidd @robbkidd

[View original notes in etherpad](https://e.chef.io/p/docker)