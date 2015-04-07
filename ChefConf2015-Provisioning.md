Chef Provision(ing) session

## What do you want to change or add?

### Cluster testing
+ idea: bring up cluster, test if it works, and if so, pass it along through dev/test/prod
+ can have jenkins server run cluster cookbook, run tests, run rspec
+ priority: devs or ops, making cookbooks that can deploy the application quickly (particularly for an update) with a framework for tests that's just enough to hit webserver (or whatever necessary).  Can extend to have more complex tests, such as running a heartbeat 100+ times against a 2-node cluster, and killing one node halfway and making sure you still get the heartbeat back every time (ie: no requests get dropped in failure condition)
+ achievable goal: build one repository with one application that does nothing but loads "hello world" from a database, and have rspec tests for simple and load tests.  can use chef-provision to start/stop
+ need minimal feedback loop time when testing code changes. 

## What kind of things can we do?
+ chef-provisioning-aws
  + What it can do
    + somewhat redundant with cloudformation, except that it's code instead of json.  but it has less functionality than cf.
    + rule: don't destroy things you didn't just create
    + rule: can reboot server it just started if it didn't provision correctly.  usually helps.
  + What we want it to do
+ chef-provisioning-fog
+ chef-provisioning-vagrant
+ chef-metal-ssh

## Stages
1. Allocating
  1. Getting the id and storing in db
  2. Populating the run-list
2. Ready
  1. Ready to have chef run on it.
  2. Machine as to be "up" and warm, ssh must be available and accepting connections
3. Setup
  1. Chef is installed on machine
  2. key is installed
  3. if provisioning stopped here, and chef cron'd, everything would eventually converge
4. Converge
  1. chef-client is run
  2. need to get here if you need the IP (and other ohai data)
  3. can even get here with an empty run list (or minimum run-list)

Where should orchestration for scaling down happen?  Want a policy for load balancers to remove machines after no activity, and something external to the load balancer to manage resource.

Can have single provisioning node, has recipe that knows every other piece of the cluster and can bring up other nodes.  But something needs to watch it to make sure that system always exist.  Can have other nodes in the cluster re-provision the provisioner if it goes down.  yodawg.

If you want to use a central chef server to store the nodes, you can run chef-client -c .chef/knife.rb recipe.rb etc... 

https://github.com/ryotarai/infrataster

https://github.com/chef/chef-provisioning-central
A central place for chef-provisioning example projects!

Attendees:
    Ross Dickey  rdickeyvii@gmail.com  @rdickeyvii

[View original notes in etherpad](https://e.chef.io/p/provision)