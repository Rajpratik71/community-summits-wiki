# Microservices, Containers, and Chef - October 14th 2015, 10:40am

## Kitchen-Docken
* Takes a bare container and dynamically creates a transport container (ssh/winrm in it)
* Uses a recipe as a Dockerfile
* Goal is to "keep Chef out of the containers"
* Soon to be released by Sean O'Meara

## Docker Cookbook (https://github.com/bflad/chef-docker)
* LWRPs for configuring Docker
* Composable cookbook

## Does Chef run in the container?
2 Stories
* Chef as a container build tool
  * You're replacing a dockerfile with a recipe. Your output is a container.
* Chef as a cluster orchestrator
  * Chef as docker compose
  * You get the notifications and subscriptions chain that you're familiar with from Chef
* Common story is to not run Chef within the container
  * For dev workstations - testing cookbooks with Kitchen and Docker is very powerful. In this case Chef does run within the container.
* Using Docker containers for testing purposes accelerates your iteration speeds and allows you to test on a lot of different platforms.
  * You can use Jenkins/Travis/etc to start up a container quickly and test/build your software within the container and get the results back on your build job
* Chef Resources represent a noun. They don't need to represent a file on your local file system
  * Traditionally resources acted upon things on the local machine itself. They could represent remote things such as:
    * A docker container
    * A configuration setting on a router/switch
    * A build job in Jenkins

# Chef 12.5 resources
* Historically creating resources has been a huge pain
  * A lot of boilerplate was required
  * Then we had the LWRP DSL which also required a lot of boilerplate
  * LWRPs are also a pretty big word that doesn't mean much to somebody
* Things are now in one file with much less boilerplate
  * Much easier to get started and start trying out resource centric development
* Old resources had "attributes" which is a bit of an overloaded term
  * Could have been "node attribute"
  * Or could have been the interface for how you configure a resource
* Resource "attributes" renamed to "properties" to disambiguate