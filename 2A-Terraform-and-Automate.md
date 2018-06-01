Managing de-provisioning through an AWS Lambda. [AWS Labs example code](https://github.com/awslabs/lambda-chef-node-cleanup). Can be pretty easily modified to use Paramiko to ssh into Automate or Winrm to connect to a Windows AD and run whatever command to cleanup objects. I'll see if I can sanitize my fork of the example code to cleanup and make it public.

Statefile management - using Gitlab for state file management
Statefiles have passwords in them so need to be encrypted.
Looking at using Hashicorp Vault for the secrets part.
Can use Consul to store state files
To bootstrap in a pipeline, can use cloudinit for Linux.
Use Opswork Chef Automate for AWS
delivery review, goes off to pipeline.  Terraform layer can change number of nodes, but delete action on Chef is challenging to
* figure out what other things to cleanup.  AD cleanup. Chef Cleanup.
* Use TF deprovisioner for Chef.
One deploy should build in multiple clouds.
Use AWS Lamda for autoscaling groups so when take one down it does the cleanup
Cleanup have it ssh in and delete.
Terraform - best at provisioning.  Chef best at managing the state of those resources.
Terraform AWS driver is great
Terraform can manage the load balancers.  Chef Client can query load balancer to get state.
A lot of issues validating JSON used inline in a terraform template
* Validate clean JSON first
* Use module w/ local exec to verify
Heavily variabilized TF templates.  Templates for each platform.  Front end in build cookbook populates the TF variables.
Getting information on node such as Ohai.  Also knife search.  Push non-sensitive information local.  Query AWS metadata.
Use file provisioner to push token down that gives access to Vault.  One time admin access.
* Need to manage the token.  Take Chef out of token management.
* Use Consul template.
Terraform should handle the destroy layer