```
Tools being used for pipelines:
	GitLab/GitLab CI
	Jenkins, Jenkins X
	Travis
	VSTS
VSTS -  build own Automate server
Jenkins as a build tool.  Artifacts go into Artifactory.  Promotion pipeline using policy groups for environments.
	Each group of systems always get correct versions at the correct times.
Challenges: change management, approvals
        Have pipelined deployment mirror existing process to ease the integration with existing processes.
        standard CR's - once proven, cookbook calls API, opens API, tests, closes ticket.
	Using Sharewell.  API is difficult so wrote wrapper API to it.  Most ticketing systems let you do this.
	Custom resource for open/close, goes in build cookbook.
Instead of CR w/ implementation/backout plan, it's always the same because cookbooks are always moving forward.
	Just push small changes.  For 5hrs of code, write 10-15hr for testing.
Challenges: multinode testing
Separate pipeline for PROD. Pause in there for extra approvals.
Jenkins X is Jenkins for the cloud - works better with container.  Solves the blob problem.  Specify which container to stand up.
	Overlaps with Spiniker
Issue is Jenkinsfile is per project.  Hard to change something across projects globally.
Write wrapper to Delivery Truck cookbook to do things like get credentials.  Build main.tf file for Terraform that ends up on an Automate Runner.
	Most runs out of provision.rb.  If anything in the pipeline that bootstraps does a reboot, it causes it to fail and Terraform doesn't write to a statefile.
Challenge of deploying to multiple clusters and orchestration:
	Can be done w/ Chef, but need something to orchestrate and fence off (temporarily stop chef-client to eliminate randomness) and determine it is safe to upgrade.  Push jobs can be used, but Chef recommends getting away from Push Jobs and not doing anything new with them.  This client-pull based model is difficult without another tool to do things in a certain order.
```