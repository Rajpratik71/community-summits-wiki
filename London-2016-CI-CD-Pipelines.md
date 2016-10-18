# CI/CD Pipelines

What software are you using to create a pipeline?

* CircleCI
* Travis-CI
* Jenkins
* Gitlab CI

How do you do dependency resolution?

Berkshelf

Version pinning with Berkshelf can be problematic with depsolver when you version pin.

New depsolver silimar to Berkshelf from Heavywater called Batali

git autotag / thor-scmversion for automated version tagging

One Jenkins pipeline works by automatically bumping version tags by patch version

Some push git tags up and when the build is successful that version ships

Having shared cookbooks between multiple teams someone has built a tool that pulls in shared cookbook changes which then prompts them with a changelog and merge button to ship those changes into their own separate pipeline.

Horror Stories:
* Running and versioning roles in a CI/CD pipeline are very complex. When roles fail the tests, everything turns red and nothing could be shipped.
* Running test kitchen via Travis-CI and using an external service like GCE or EC2 is very hard. Need to copy encrypted information to each repo which can't be automated. Also leaves around test instances that you eventually get billed for if they are not properly destroyed.
* Doing something similar with Jenkins and Vagrant where it running in parallel can cause bugs during testing. Their solution was to switch to kitchen-ec2 instead because of Windows based testing not being available with Docker.
* Version pinning can be difficult to handle in CI with moving minor release version pins up manually. Developers can get lazy and keep bumping patch releases automatically so you end up with version 1.1.19081 instead of 1.2

"Don't trust developers with anything and you won't go wrong"

There is an alternative CI solution written by someone who went through the pain of Jenkins. Cyclid is such an alternative. cyclid.io

Someone automates via a cookbook their syncing between chef organizations and their jenkins build pipelines. If it notices there is a new project and no pipeline, it creates one, but has trouble keeping things in sync. It's a very hard thing to automate.

Jenkins pipeline is awesome. Works better than previous versions. Can write the pipeline in code via a jenkins file to instruct jenkins how to build it via a pipeline. There is a default build that developers can extend and override if they need to. Jenkins is fairly familiar to a lot of developers. Some use rake files that Jenkins builds. The Jenkins build pipeline is in Groovy. It's Groovy, but it's usable. Each job is a loop so it's not very hard to setup. Setting up global defaults could be difficult to manage.

Chef has multiple large Jenkins installs (focused on application packages, not cookbooks). They manage their build pipelines separately from the code which can make it hard to change the pipeline behavior for those not familiar with updating a pipeline. Better to store the build pipeline with the project being built.

Jenkins can be difficult to setup and configure via Chef. There are pre-built AMIs to run it as well. There is a community Jenkins cookbook with resources, but it doesn't detect changes peple make to the jobs via Jenkins. Chef can enforce those configurations for you anyway.

In Jenkins 2 global security is enabled by default which can break the Chef cookbook.
* Jenkins cookbook is in active refactor to ease complexity and get to a point where can install Jenkins 2.
* Jenkins cookbook isn't the right place for the management of jobs. We've considered a Jenkins jobs cookbook (kind of like artifactory has a cookbook to install, and one to manage artifacts). That way we can keep the complexity down.
Consider managing the base install of Jenkins with Chef (Jenkins as well as the plugins) but do the jobs in Jobdsl/Groovy/Pipeline ... => create the seed job with chef and go from there.

Someone is trying to setup a lab to test Chef Automate. The default workflow is very prescriptive so the stages are very fixed so bringing an existing pipeline in to Automate can be a lot of work. Chef may not recommend Automate if you already have an existing workflow that cannot be altered enough to fit within Workflow. Someone is still wondering if Automate can be a fit for them. Can be difficult to setup all the infrastructure needed to run Automate versus just a standalone CI server.

A bare metal customer was not a good fit for Automate because of the extra systems required to run the workflow and the level of effort needed for the small ops team made it less of a fit. It's still customizable for its build steps, but it still wasn't a good fit.

Continuous Delivery:

Can use berks upload and berks apply to deliver cookbooks to various environments.

Delivery can be easier to build than CI

Someone builds a tarball and ships that out.

Is anyone providing any UI to a product manager who hits a button to ship? Someone does, but it is proprietary.

Someone uses Chef Solo after creating an image that makes the deployments immutable. It's mostly immutable. Mostly.

Someone presses a button in Jenkins to do code deploys out to Amazon.

Someone else uses Chef to build an image which then is released to production.

Immutable infrastructure can be a mixed blessing. When you need to change small things like user accounts instead of a code deploy then you need to reinstall all the servers affected by that change. A way to avoid that is to have a separate service which manages the faster moving changes, but then you run more risk by changing things. Immutable infrastructure helps avoid drift because you can easily trash a system and reinstall to get the exact same software and configurations.

Canary deploys? Testing deploys in production without taking everything down. One does this by using a Chef environment with a limited set of production nodes that can be easily taken out of production without taking the system down. The deploys are also done in a blue/green pattern which wll eventually go into a CD pipeline.

One person uses a chef run as a way to test if deploys will work which can be a good way to do delivery if you have a lot of testing.

