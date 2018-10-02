# 2018 Seattle - Train Plugins and Accelerating InSpec Cloud Resources

## Topics Discussed
  - Merging of two topics, Train plugins and accelerating cloud resource development
  - What is Train? - Provides a connect to a target and handles running commands reading files etc 
  - InSpec Iggy - Build InSpec from Terraform state file (minimal resources, no easy button, but provides a great starting point)
  - Running InSpec as a Terraform provisioner (bundle resources with InSpec tests)
  - Aaron is having to copy InSpec resources between profiles. These resources have to setup a connection to DNSimple API. The group recommended abstracting that out to Train plugin.
  - InSpec 1 > 2 > 3 progression (No API -> API bundled -> Plugins)
  - Pain around documentation for Custom Resources and Test Kitchen usage (What directory do I put my tests)
  - Resource support for OS X.
  - Example "Plugins" AWS/VMware/etc
  - Deep dive into Train plugin exposed methods (connection/caching/etc)
  - Overview of an [example Train plugin documentation](https://github.com/inspec/train/tree/master/examples/plugins/train-local-rot13)
  - Ran out of time!!! So many great topics

## Attendees
  - Clinton Wolfe - Submitter
  - Jerry Aldrich - Facilitator
  - Aaron Kalin
  - Jacob
  - Dominik Richter
  - Heath
  - Sam Lavenick
  - Elijah