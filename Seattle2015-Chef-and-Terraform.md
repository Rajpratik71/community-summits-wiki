# Chef and Terraform 
## Chef Provisioning and Terraform

Chef has come along and changed things for our sys-admins to build up new boxes - simplying building, rebuilding, and changing.  Terraforming is taking it to the next level.
Still have state that isn't defined - the infrastructure state.  If somebody hits delete on a box - it is gone - and you are left trying to remember (or looking at docs that you wrote.. right) for what that box was (ram, cpu, setup).  Terraform lets you define and capture that information.

Clicking to create a new copy your infrastructure in AWS could be hundred of clicks and hours of time.. terraform lets you define all that in code.  

### lets talk about that
Unlike Chef (remote server) Terraform runs from your desktop and ensures the state in AWS meets your definition.

AWS has a limit to tags (~20) and tags are 'kinda clunky'

_Terraform is a different methodology than Cloud Formation_   (how?)

Terraform is a metalayer across different cloud providers.

   terraform apply # spin up those resources

Similiar tool to *chef provisioning* 
* both to help provisioning infrastructure
* chef provisioning driven by cookbook and then it converges your infrastructure to align with the cookbooks
* terraform you have to describe your whole infrastructure in your file
* chef provisioning didn't exist when terraform was started
* both get the job done
* there are some gaps that Chef Provisioning does and Terraform does not (and vice-versa)

*How do we drop chef down a layer?*

Is there plan in the future, possibly, for terraform to consume chef provisioner files?

storage and networking blur the line in provisioning

*How does this tie into test kitchen?*

Example: Mysql master/slave - very hard to write a test for that.

You can write some rspec that runs locally that grabs the IP and tries to hit website, then murders the database, then smashes website to see if it is still working - if it is still working then everything is good.

Kitchen.yaml - define clusters apply to vSphere - then does sanity check of if the nodes spun up with expected storage, ram, cpus.

*Is there a way of introspecting what will be built?*

Terraform has something?  Chef provisioning (not yet?)

[ThirdWave Insights](http://www.thirdwaveinsights.com/) has tooling around visualization with Provisioning
https://www.youtube.com/watch?v=hoXf0Uo5bCo

*When using chef provisioning node (perhaps your local laptop) how do you keep things all in sync with dev and production and not create a huge mess?*

This is similar to how it used to be painful to keep chef server and your github repos in sync - but berkshelf and CI came together to help with that.  
Terraform pulling a push to git for CI almost there but not yet there.  Kind of like how chef was 3 years ago.  Still need to work on the tools and right workflows.

*Chef orchestration (formerally metal) and Chef provisioning - are they the same thing?*

Chef metal became Chef Orchestration which is now Chef Provisioning.  _Keep up folks - this is perfectly clear._

Chef provisioining looks like a Chef converge but they are not the same and it is a different beast. That can be a bit daunting for a new person trying to wrap their head around it.  The barrier to entry for even a basic 5 nodes on AWS is hard.  

## Chef Provisioning needs a quick start guide for AWS.

"and chef sucks for not having that" - chef employee 

docs.chef.io and AWS README are not even consistent.

Chef and Terraform
Terraform allows codifying the infrastructure - stores information that they used to configure in the console.
They use tags on the infrastructure to drive behavior in chef.  User Data also supplies the initial configuration that the first chef client run uses.

Chef Provisioning on VMWare

Chef Provisioning and multi node testing

Chef Provisioning or Terraform to deploy Chef Servers: Which is the better option and why? We are looking to deploy Chef Servers closer to our customers both geographically and a Chef Server built to their specs.

Do community members want Chef to support Chef integration and workflows with Terraform?

Gap: spinning up a multi-node environment and performing integration testing afterward - either testing that the provisioning succeeded (right number of CPUs, RAM, etc.) and/or that the application actually functions (i.e. MySQL cluster, kill the master, does the app still work?).  No defined way to do this, some light patterns discussed, but no agreement on the best way of doing this.  Still seems new to most people.

Terraform vs. Chef Provisioning: different models of thinking / approaching the actual provisioning.  Group did not identify one "deal-breaker" or "feature" that pushes someone to one tool vs. the other

"I hate Chef Provisioning - it sucks, and it's difficult to use."  0-to-value w/ Terraform was 15 minutes.  

How do we continue this conversation more regularly?  A number of room attendees wish to discuss more and don't want to wait until next year.  "gitter" is proposed as a good way to discuss more about Chef Provisioning.

The lack of 'quick start' guide for Chef Provisioning has stopped many people from even getting started with it.  Terraform is the opposite - it is a great getting started guide that takes people from nothing to a provisioned machine in less than 5 minutes.