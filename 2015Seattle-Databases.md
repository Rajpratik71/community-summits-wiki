2015-10-15, 10am

Folks on mix of db technologies
* MySQL
* PostgreSQL
* SQL Server
* Oracle
* etc.

Good number on AWS

Sombody asks about having Chef converge a temporary state for database upgrade

Somebody treats database changes as part of an application and Chef just cares about converging the application

Can have Chef query schema version, and then conditionally run some upgrade tools

Chef can more generally help with database administration with the host on which it runs (cron jobs, backups, application)
* Leave the inside of the database to the DBA

Anybody worked on automating Oracle install?
* Somebody heard that there's a cookbook to install Oracle RAC

Can be a control/ownership issue with DBAs that want to control everything on the db machine
* Variant on immature devops org
* More typical with "old-school" DBAs
* Need to convince them to make changes through Chef

Kernel changes may need reboots, some do not, but can adversely affect a running db

Talk about compliance, auditing, change-control

Find some common ground

In one shop, Chef just bootstraps the db machine, DBA installs and configures it, and then use Chef to search node to apply config to app nodes

MySQL/PostgreSQL, use the community cookbooks?
* One person: No, they have too many dependencies, takes too long
* Question poser: No, we want Percona MySQL so we can't use cookbook

Orchestration can be a problem where certain nodes (their schema)  need to be upgraded in a specific order

Somebody says they used Chef to install and seed test data into databases, also failover and upgrade

Some use VIPs to abstract the db from the app servers
* Usually just build a new box

Chef isn't a great fit for managing a failover where temporary state is involved
* Some use Chef to pull down scripts, not to run them, but there for admins to use under the right scenario

For orchestration, try using a service instead of scripts
* Like Barrel Roll, Run Deck, Jenkins
* Somebody says they're a huge fan of Chef and Rundeck
* Rundeck is ssh-based script runner

Application still needs to be architected to support sophisticated upgrade scenarios
