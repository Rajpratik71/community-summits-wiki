Ansible (orchestrating aws/cf, then chef)

Cloudformation

Terraform - good for provisioning

https://www.terraform.io/docs/provisioners/chef.html

How to share knowledge in multi-tool environments

Capturing the new starter experience, as a method to expose oddness/weirdness

Mcollective (Puppet) - asset discovery that calls chef and vice versa

How to decide which tool to use?

Desired state orchestration/automation

What is the source of truth in multi-tool environments?

Chef provisioning: https://github.com/chef/chef-provisioning

Apache Brooklyn: https://brooklyn.apache.org/learnmore/blueprint-tour.html

Brooklyn with Chef: https://brooklyn.apache.org/v/0.9.0/yaml/chef/creating-blueprints.html

Consul service discovery/config - fighting over templates with chef

Can you upload a data bag via an interface? Yes - templates and builds via pull request

  * Break attributes into sections
  * Possible race condition if try to update during a chef run

OR: Chef Server API - Ruby,  PyChef, .NET, Java

Approval on data bag changes - github/jenkins

You can kinda use a data bag as a db

Control databag access through ACLs

How to manage tool upgrades - beta environment, try and see, containerisation, minting packages

Make sure dev is using current versions of tools

Terraform ate my infrastructure - test test test, and examine every `destroy` command - definitely check out https://github.com/newcontext/kitchen-terraform

Chef is semi-safe, as it’ll just fail, whereas other orchestration may cause bigger problems

Run terraform/tools through jenkins

Is there tool code coverage reporting for ChefSpec/InSpec? Possibly - shows attempts to do things

Should you test on existing infrastructure, or spin up a new environment? Depends

Workflow is good at testing the process of upgrades, rollout, but not so much long running tasks

Is there any integration between Kitchen and Terraform? - Yes, maybe, possibly incoming

Splunk

ChefGuard - in front of the chef server

For Windows - Powershell will keep searches in memory, BLU will mitigate this https://github.com/schubergphilis/blu
