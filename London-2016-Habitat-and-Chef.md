# Habitat and Chef

* systemd kicks off the build
* hab is a static binary
* hab start calls hab-sup

* hab start core/redis if not on the local machine will pull from the depot

* leader-followe
  * one will become the leader
* upgrade strategy
  * bring one down, or do a carney style, and the default at this moment is "do it when you need to"

* Figuring out the failure conditions and the escape system

* the elections are deturmed via the swim, it uses the eventual consistancey
* the leader is determined via a bully protocal,

* it's closer to serf, not for leader election

* basic authentication via the proxy
  * we don't have kerbos but it would be interesting

* full chef runs a few
* capstrano a couple
* a package build

* how do you control your build?
  * shell?
  * chatops?
  * rundeck?

* any one deploying directly out of the CI?
* gating through a human seems more reasonable

* A CD pipeline building the code in bamboo, to bulid the ami, and human :+1: it

* In a hart package can have "default attriubtes"
* there are a few different ways to override
1. write a file
2. environment variables
3. run time can be given a toml to a service group

* chef-vault with habitat
  * there is some work that it's needed with secrets on disk
  * upload_file could be encrypted and shipped around the ring and only targeted for a specific machine

* dependencies between different packages?
  * we are starting down this path
  * it's mainly around binding
  * I'm an app server, but i need a postgres, give myself a label to say hey i need a database
  * through the members in the ring the supervisor and labels i can write out the config

* the tomcat package dependencies are captured in the pkg metadata

* a better describe of the "Ring" is an interconnected-mesh, not an actual ring

* you probably want a staging ring, and a production ring, but you probably don't want them to talk, but you can if you have some shared services

* what's the process from a commit to being deployed?
  * build a plan to make a new version pushed to the depot and the supervisors will update when they are ready, per default setting above

* the depot has "channels" which allow for promotion

* what's the migration path?
  * what is the first good canitates for the harts?
  * what is the service that you can start with

* This feels backwards, bash to chef, now you're telling me chef to bash, this feels backwards
* The split between the teams of an app team and infurstruce team is more focused here
* you wouldnt run chef if you want to build a yum package

* you can vendor everything if you need to in side the package

* depsolving is done at build time not install time

* where is the line between the application and infurstrucre?
  * where i want to use habitat, if you are drawing out like mysql, webserver circels, image them as services
  * the host needs to be started and configured via Chef
  * the service is where habitat runs

* the last 20% of automating your stack is hard, this is where habitat goes

* habitat doesnt replace chef, but there is bleed through