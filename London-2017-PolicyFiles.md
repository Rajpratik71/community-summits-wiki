# Policy Files
A summary of policy files was given, what they are and what they attempt to overcome

* Databags
* Roles
* Environments

These are versioned artefacts, additional tooling or a cd/ci pipeline can be built around these to manage these changes but you will probably end up where you do not have a single version of the truth.
A policy file includes checksum of the cookbook, pinned with the hash of the contents of the cookbook


### Q. How do you manage Policy files?
Use the `chef` command not knife. 

### Q. How you export a policyfile to artefact? 
Need to use `chef` command the chef docs website explains this (https://docs.chef.io/ctl_chef.html#policyfile-commands) 
Someone shared that they use these policy file tar balls as part of their provision pipeline for AWS.  They generate the file, upload to the s3 and reference within `packer`
`terraform` also has support policy files.

There is also support within chef-solo.

### Q. Visualization of policy files within the chef server gui’s
Limited support with chef manage, literally it might just say that a policy has been assigned.  Chef Automate will have support for presenting a read only view of the contents of the policy file. 

### Q. Is there support within the chef server api to support assigning and the changing for policy files?
????

### Q .  Where to start?
As a suggestion ….. Write a policyfile around a single cookbook, export your environment data and map that into your policy file, define a run list and use `chef policy` command, export a tarball apply it to your kitchen instance.
There are some Pinned posts on the policyfiles community slack channel – there are also some some good blogposts by [Michael Hedgpeth](http://hedge-ops.com/) on how they implemented policyfiles within NCR.


### Q. Testing your policyfiles
There is a `Policyfiles` section within `.kitchen.yml` test-kitchen has support if but the documentation is a little light and could do with a PR…… (hint hint :)
Having a policy file exported as an artefact helps in the situation where you have an air-gaped network and you need to transport everything need for the node.

As a side - There is a knife command is available to nuke everything else apart from version of the truth that has been dictated as part of your policy bundle. 

### Q. How is it different from Berks
Berks is taken a cookbook and making sure it dependencies are there, policy file is not only taking into account the cookbooks but also taken into account what your nodes are going to run.
* On a chef-client run you will benefit from using Policyfiles in that it doesn’t have to perform dependency resolution 
* If you aren’t using policyfiles, for a free performance improvement consider removing old versions of your cookbook. 

_Policy file Community Suggestion_ – Anyone fancy writing a sample guide to help people migration from an environment model to policy files?
A benefit of using a policy files is the run-list within policy files can be named.


## Multiple Policy Files

At present you can only define a single policy file for a node

There is a multiple policy [RFC75](https://github.com/chef/chef-rfc/blob/master/rfc075-multi-policy.md) which defines the scenario of being able to run multiple policy files.  These will include being able , local file, git repo, specific policy from a chef server.   

This will be discussed on Thursday on the community slack #developer channel 17:00PM UK please come along, review Jon’s [PR](https://github.com/chef/chef-rfc/pull/280) associated with the RFC and add your suggestions and thoughts.
