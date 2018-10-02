Around ChefConf 2017 a number of discussions occurred about the intersection of Habitat and Chef. For example, a Chef cookbook for managing Habitat. One pattern that developed was creating a Chef Policyfile for a particular application or purpose, such as server hardening, and bundling that in a Habitat package with the Chef Client package. The cookbooks contained in this package are then run with `chef-client -z` independent of the need for a Chef Server. When changes to the cookbooks are needed, a new Habitat package is generated, released to a bldr channel, and consumed by the Habitat update strategy. This package can still report to a Chef Automate server using a data collector token directly rather than through a Chef Server.

These Habitat packages are simple to build using the [scaffolding-chef](https://github.com/habitat-sh/core-plans/tree/master/scaffolding-chef) Habitat scaffolding.

If you had existing heavy use of data bags or search, it is theoretically possible to run Chef Client in this model using a Chef Server rather than Chef in Zero/Solo mode, but it isn't known that anyone is using that pattern today.

Currently the Chef run happens as part of the Habitat run hook at an interval as part of the scaffolding. The possibility of using cron to run Chef rather than consume the resources to keep the client binary in memory. It was also acknowledged that many container images don't have cron today however.

Primary benefits of the Habichef model is simplifying the system on the target system by removing a Chef Server. There isn't a dependency on the Chef Server being online, which increases stability. Updates can be deployed in seconds or minutes using the push model of Habitat, as opposed to the splay based pull model of Chef where it is likely to take 30+ minutes between runs.

On the other hand, some users will have to understand both Habitat and Chef to use this pattern.

It is not recommended to use Chef to provision Habitat on your systems, and then run Habichef on top of Habitat. Habitat should be installed by your existing provisioning system, such as using the [habitat provisioner](https://www.terraform.io/docs/provisioners/habitat.html) to Terraform. It was discussed if there was a Cobbler plugin for Habitat that existed or not, but not determined.

Habitat packages exist on less platforms than Chef, for example there ARM packages, which can limit the environments this solution can be used in.