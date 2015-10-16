Welcome to the Bento Room!

Check out here for awesome Bento-ness https://github.com/chef/bento

+ We want Windows Bento boxes now!!!
+ In the Chef world a Bento box comes from a source box or a customized Bento box
+ Everytime you start up kitchen or cookbook genrate you have a name field that maps towards a magic box, this in Bento
+ Moved to Atlas 
+ Vagrant update/vagrant box update
+ Moved to a new pipeline
+ Parrells, fusion, QMU is coming
+ Its effectively an opinionated virtual box
+ Tracing - avalible in Git - trackable
+ Hyper V images are coming, Altas has support for it
+ User use case is open stack images
  + forked - hard stuff is done - update templates
+ Bento is for vagrant - how do we hack this? Privatize this?
+ Pull requests are welcome against the repo
+ Open stack is ready
+ ReadME is avalible and its accurate now
+ Box cutter is awesome
+ Clone the repo, packer installed, check out the crazy rake file to see tests

What is the purpose of this session
+ more the the raw packer experince 
+ no real inheretance 
+ specifically with Windows boxes - i want to put in my own key
+ pass a key/password via command line
+ Packer has no way to template

Joe Fitzgerald packer/windows

Download a box - kitchen init - centos 6.6 - 7 is out therefore 6.6. doesnt exist. People want to test 6.6/6.5. Would it be valuable to 'download latest'. Aka remove the .

Back filling platforms

Debian takes down thier files from the mirror

Single repo for Bento boxes will reduce replication moving forward

------------------

Open sec images
Hyper V support
Windows templates
kitchen -vagrant pointong to atlas
No more S3
Back filling old platforms OS . release - Seth said he will do boxes no matter what