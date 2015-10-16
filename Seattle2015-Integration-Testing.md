Note taking party time for Note Integration. Fancy! Stylish! Readable! Yay! - doge

# Integration Testing

* what is testing: unit, integration, and the tool sets: chefspec, test-kitchen, audit mode. 

Test Kitchen & ServerSpec vs Audit Mode.

## How do you test mulitple machines that are dependant on each other?

 - spin up multiple machines with private network between them in Test Kitchen
 - run TK through Jenkins instance if you need more resources for multiple nodes
 
 Individual kitchen driver files in github repo
 https://github.com/test-kitchen/test-kitchen
 
You are currently going to be reading the test kitchen code base or reading blogs to get an idea of how to do this type of testing.

(this discussion is difficult to capture) <-- I agree

Should each cookbook have its own chef-specs and server-specs?  How do you avoid repeating yourself?  

Do unit tests in their respective cookbooks.  Simplify integration tests as much as possible to test the whole path through your application

Test the minimum thing that the cookbook does.

chefdk gives you the chef tools along with testing tools and generators, allowing you to have the ``chef generate app`` that gives you the test files and kitchen.ci files.

Discussion on stubbing out the needed databags:  If it is hard, then you should stub it or abstract it. 

stubbing one helper method that looks for databags (instead of _??__ each of the databags)

ex.  Library method looks for encrypted databag, then databag, then falls back on node attributes which you can easily set in your kitchen.yaml file

## What is audit-mode?
 
audit-mode in chef client (benefit : the same audit mode test will run in dev and live)
three phases now: compile, converge, (new) audit mode

https://github.com/chef-cookbooks/audit-cis

Allows consistent tests in local (devel) and the live environments.  It is a form of ServerSpec (with more keywords and formatting). "It's cool, check it out"

There is a new audit-cis cookbook written for this audit phase of chef.  This will allow you to prove to your auditors you are passing the CIS audit.

"It's just a recipe" + needs an audit mode flag enabled (add to run list)

## How do you know what is a valuable test, vs. a robotic test?

"I expect chef-run not to raise an error"  #1 test for every recipe.  Ensures you don't have any typos before cookbook upload and finds all dependencies and identifies if you are missing one
- you do not need to wait for cookbook upload and chef-client run to see a quick/easy failure caused by a simple oversight

What would you check after ssh'ing into a server after deployment?  Take that thing and test for it using serverspec

Tests aren't necessarily for YOU, NOW.  They are for the poor shmuck 6 months later who will come and work on it and may easily break your logic.   - unit tests for ALL branching logic and guards

Good way to judge what tests might be the minimum: Ask yourself: At 2AM, I am pushing out a new version of this thing, what would I go poke at to confirm it worked?  Or if 6 months from now we have a new person what should they be looking at to confirm things are working.

"The best test is the one you write."

Good practice to write a test per resource to prevent accidental removal or version changes

## multi-node testing - use chef provisioning? (following JJ's openstack cookbook using rake - but feels like it should be better integrated in kitchen)

Manual testing - but it wouldn't be far for serverspec.  Sounds like an orchestration tool?

Blog Post coming.... stay tuned

## Has anyone used Liebnitz? 

Referenced in a book that Steven Nelson Smith wrote.  But looks stale.  

Updated a year ago.

## General question about Test Kitchen: Multiple convergances to run before server spec.  How to do automatically? Can do manually.

Why? Users need to be created first.  Or to ensure recipes are idempotent. Or if making changes to client.rb... 

Serverspec can invoke chef client, too.

In most cases, calling ohai plugin to reload should work (unless like adding users to AD... not user to box).

## Going from one version to another.  When there's cleanup that needs to be done - testing the states... (audit mode)  Both states should pass (old and new)

Can't always just do an action delete in next version of cookbook, might need to stop services, remove configuration.  Integration tests needed to test previous version followed by new version in two seperate runs

That's one of the reasons why "union" and "rehearsal" states in Chef Delivery exists - to help catch those types of things

Use case: version x creates a resource.  version y doesn't need that resource.  It would be cool to have the new version know that there was a previous version.

Tests should change between version.  So - need to trust Chef's idempotency

## Kitchen for windows? (show of hands) = approx 7 or so people 

In CI? = no hands

## Monolithic approach
