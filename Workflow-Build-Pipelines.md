# Proposal: Discussion around build pipelines

* Jenkins? Chef Workflow? Other?
* Has anyone migrated from one to another?

# Tools

## Chef Workflow

Handful of people looking at or using (maybe 1 using in production)

Opinionated - this is both good and bad...

 * good -> don't have figure things out from scratch
 * bad -> limited ability to customise behaviour (can skip, but not add)

Positives:

* Union/Rehearsal/Delivered idea is very powerful
* If you want Continuous Delivery for your infracode, you will need something much like that

Negatives:

* No Windows build nodes
* Can't run kitchen suites in parallel
* No unattended installation of build/run nodes
* Documentation is so-so
* Little guidance on how to define union/rehearsal, map your reality into Workflow, etc
* No scheduled builds (everything starts with a change)

## Gitlab CI

Scope:

 * (branch) lint, rspec, kitchen -> merge to master

## Jenkins

Scope:

 * (branch) lint, rspec, kitchen -> push to chef server

Positives:

 * lots of plugins
 * easy parallelisation of tasks (eg, kitchen suites)

Negatives:

 * lots of plugins
 * can be a beast - needs to be maintained
 * no turnkey Chef cookbook pipeline (find examples on blogs or github)

## GoCD https://www.gocd.org
Pipeline all the way to production
Happy with the way this works, but not sure how to close the loop with testing in final stages

## Spinnaker https://www.spinnaker.io
Opinionated, pipeline-oriented system.  Blue/green deploys.
Deploys infrastructure into your cloud environment (eg with terraform templates)
Chef could be used in building the artefact, but would not run after

# Questions

Q: How do cookbooks get promoted into production?
A: Manual updates to environment pins, knife-spork, delivery-truck(?)

Q: Who is or can automatically deliver to production? (continuous delivery)
A: 1 or 2 hands (most people were not confident in their tests, or limited by compliance requirements)
