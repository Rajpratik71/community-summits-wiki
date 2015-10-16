chef-reference is a cookbook Chef has been working on to manage Chef's internal CI infrastructure. 
It uses all the best practices listed in the documentation (ok not all but the ones that make sense) and all the latest `Chef technologies (Policyfile, chef-provisioning, etc...) 
This cookbooks is developed against AWS but other backends can be subsituted. It uses chef-ingredient primitive for installation and configuration.
There are 4 nodes in the architecture: server-backend (chef-server & reporting) server-frontend (manage) analytics-server & supermarket
This cookbook goes through a Chef Delivery pipeline that can run the provisioning recipe on a build node which will build the cluster.
Goal is to pick up the latest version of all the Chef products deployed in a live infrastructure. 
This will give us the ability to test all the latest versions before they go out and catch issues before they hit our users.

Q) Is this a model you're proposing for everyone?
A) This is more specific to Chef's product suite. You can use this to deploy and configure your Chef Server.

There are some great patterns in chef-reference that you can copy in your infrastructure.
We use chef primitives as much as possible and we do not use things like IAM roles, vault etc. Because of this we can switch from AWS to Azure easily.
Eg: data bags for secrets, discovery via chef search, provisioning via Chef Provisioning, cookbook locking via Policyfiles, file copy via Chef Provisioning.

Will we see a reference HA architecture?
Currently the only reference architecture is in documentation. We are working towards having backends that can be directly deployable for HA with stateless frontend nodes.

provision cookbook => Has a _setup recipe which can be changed to change where the nodes will be provisioned
all provisioning code lives under provision cookbook

rakefile => codifies the way to launch the cluster.

Chef Delivery will eventually use this cookbook to provision the infrastructure (e.g. using the rake tasks)

Q) Are there any plans to do rolling upgrades with zero downtime?
A) Zero downtime is a myth :) It will be as minimal as possible.

chef-reference cookbook will be open sourced after some housekeeping tasks.