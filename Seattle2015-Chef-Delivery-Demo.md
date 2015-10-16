
Presenters: Seth Falcon, Tim Duffield

I <3 Christine
#truth
OMG me too

## Day-to-Day interaction:
* Check out a feature branch
* Write some tests for the change you intend to make
* make changes to the code as needed
* Commit changes
* * Delivery creates a pipeline for projects, does tings like verify code and runs tests, moves package through pipeline
* Execute "delivery review"
* Pushes feature branch up to the remote, and creates the equivalent of a "GitHub PR" within Delivery
* Handles edge cases of force pushes necessary when commits are squashed/fixup'd, etc...
* Automated testing is kicked off, diffs provided for code review purposes, etc.
* Alternatively: use GitHub integration - create a PR and Delivery picks up from there.  PR will get labeled, comments added with phases and their statuses, etc.
* If verify phase passes:
* * if using GitHub integration:
* * * you tell the Delivery robot to move the change through the pipeline by commenting "@delivery approve" in the PR
* * * Delivery will merge the change into the branch and push the change through the pipeline
* * if using the Delivery server as the remote / using the UI:
* * * click the Approve button on the change in the UI

## Additional info:
* Code review as a team
* * approve the change, like merging the change into the pipeline
* After merge, you can watch the build
* * tests will run again against master
* * now you can build! or whatever 'build' means!
* Delivery Dashboard 
* * can see pass/failed in Verify
* Audit log
* * review changes that have gone through the system
* * search stage:delivered action:finished to see last changes that went through pipeline
* * see what projects they are in
* 6 stages execute separate stages
* * Verify
* * Build
* * Acceptance
* * Union 
* * Rehearsal
* * Delivered
* Each application component (the actual app, corresponding component, etc) each have their own "acceptance pipeline" with change/review/approve/deliver
* Each acceptance pipeline feeds into the shared "delivery pipeline" (union, rehearsal, delivered)
* Each change must pass through union and rehearsal in order to be delivered
* * One single Union/Rehearsal/Delivered environment for each project that has to interconnect, not a hard requirement for only 1 Union machine, that's up to # of your systems
* Upcoming feature: explicit dependency management for the pipeline


Delivery acts as a "git remote", or has GitHub integration

Live demos are hard, especially when you use conference wifi.  SORRY FOLKS. VzWireless, don't fail us now...

Delivery CLI tool (aka "delivery-cli") is open-source.  Available on packagecloud.  Ping a chef person to get access to the Mac OS X .pkg installer.

## Questions
* Builds: are there pre-existing build recipes that ship with Delivery? ex Java, Jenkins
* * Using Travis has .travis.yml, tells how you want things to be performed
* * w Delivery, you have a build cookbook where we have a recipe for each phase in the Delivery pipeline
* * when Delivery executes the phase, it'll run chef client on recipe corresponding w the phase
* * Use build recipes however you want to build your app/product 
* * Build cookbook shared among people (common functionality), like this is how you build Ruby, Java, etc, and is shared across projects
* * Currently, the only build cookbook we ship is a cookbook for building other cookbooks called Delivery Truck (open source: https://github.com/chef-cookbooks/delivery-truck)
* * no other cookbooks are shipped w Delivery
* * Build cookbook is the component that's open source (in addition to delivery-cli)

* What else is open source?
* Delivery Cluster (server, build nodes, dashboard, etc.): where running?
* * in data center,  on prem
* * not offered in Hosted Chef

* Does "unit, lint, syntax" each tie back to a recipe in the build cookbook, or is there a single "build" recipe?
* * Each stage (i.e. verify, build, acceptance...), the phases (i.e. lint, syntax, unit) each have their own recipe that is executed by Delivery.

* If syntax check fails, does it fail other tests?
* * Runs all checks in parallel to get faster feedback

* For a cookbook acceptance pipeline, what versions of the cookbook are being used?
* * The version last used in a particular pipeline is recorded, and any other items in the shared Union environment pull in the last-known-good / last-delivered version of that artifact to ensure success in the shared environment (avoiding the situation where you are testing old versions that are older than what was last delivered - true "continuous integration")
* Can the output from "delivered" be the input for another acceptance pipeline?
* * Not a first feature today, though with code, you can do anything. :)  Possible future feature...  Current focus is changes that are best represented as "diffs to existing code" vs. inputting artifacts from other pipelines
* Do you have to iterate meta-data or does Delivery pipeline take care of versioning 
* * no auto-versioning, future feature 
* Where are the artifacts kept once they are built/delivered?
* * No artifact management exists in Delivery today - up to the build cookbook.  Internally at Chef, we publish artifacts to our own internal Artifactory instance via the build cookbook.
* If want to do refactoring or branch, how it that setup?
* * don't setup something separate
* * terminal pipelines: add extra pipelines that have extra acceptance crtieria but don't go to union, so won't ship anywhere but can leverae automation
* * whether using Git Delivery server or Github, you can push a branch to side and do whatever you want and that is outside of Delivery doing workflow for you
* How does this fit in with Chef's established philosophy of open source?
* * Much like how Chef open sources components of Chef client/server but has commercial add-ons, Delivery is similar.  The Delivery server handles the job management, process control, etc. while the inputs to that are open-source (such as the delivery CLI, delivery truck, etc.).
* * Delivery server uses delivery-cli, etc. to do the same tasks.  If the user feels the process/flow matches what they're looking for, but the Delivery server isn't the right fit, delivery-cli can be used as the underpinning of their own "delivery" environment
* * docs.chef.io has additional information about the delivery components
