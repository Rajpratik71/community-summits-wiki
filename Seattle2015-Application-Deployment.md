Application Deploy

The "deploy resource"
- does anyone use it
- should anyone use it (consensus of No)
- better than it ever has been
- bound to the Capistrano model which may not work for humans

Poll of git vs packages

Deployment methodologies
- rsync for application, chef for config mgmt
- code deploy (Amazon)
-- control of canaries
-- lots of primitives for controling the roll out

Push Jobs
- how it works
- use cases

Managing secrets in apps
- Citadel
-- solves bootstrapping issue
- chef-vault doesn't work with autoscaling
- HashiCorp vault
-- punts on getting token/appids to machines securely in the first place
- Azure Key Vault
-- not using with Chef yet

Orchestration
-problems with long lived sessions
- stop accepting new traffic, setup new env accepting traffic, and the issues with gating

Database migration
- scripts outside the system
- take it outside of Chef
- http://www.slideshare.net/PostgresOpen/selena-decklesane-schema-management-with-alembic-and-sqlalchemy
- resque workers that report status of migration back
- RunDeck is great for these orchestration tasks
-- downside: no way to execute a task and waterfall it   another task
-- can be done by replacing their executor
-- nice Chef integration

Windows Application Deploys
- using custom LWRPs for ASP.net

Blue/green environment style deploys
- Gilt Group splitter
- Asgard

Running chef-client on a schedule vs using a CI pipeline
- use CI system to drive a canary system

Artifact Repos
- artifactory

BitTorrrent deploys - anybody using them?
