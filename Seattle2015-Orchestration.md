Brian at Datapipe wants to talk about Orchestration versus CM. CM is like cleaning a single house, Orchestration is about cleaning an entire block.

Single CCR for the orchestration flows.

Chef provisioning has some capacity to do this, perhaps not fully baked today. Hashi Terraform seems more compelling.

Can we define orchestration? Is it about complicated deploys? Use case: Cloudera + 11 nodes. Used Ansible to provision, otherwise would need multiple CCRs.

First node available becomes master, others running chef-client in a loop until they can discover the k/v pair that identifies master. Using Chef Search functionality as a lock. Consul/etcd are perhaps better suited.

Distributed systems deployments with just Chef, this worked, however without the requirement of a single CCR. Only needs to be done when the cluster comes up for the first time, beyond that it's all Autonomous Actors scaling up and down.

Problem of chef-client sitting around for hours waiting to discover a master.

Chef provisioning allows one to describe the pattern of multiple CCRs within a single recipe. 

Need to agree on SLAs with customers.

"We don't need order as often as we think we do". This allows for the multi-CCR eventual convergency. Implicit trust.

If going to Zookeeper, it also needs to be set up. Need to invest in health checking.

Multiple CCRs - give developers the ability to take coffee breaks.

Consul and etcd seem to be the hot stuff over zookeeper.

As a community we have not discussed/agreed on a good master elector tool.

# Orchestration Session - 20151014-1330

Topic Proposer's current environment: jenkins used as a build tool, which sends artifact to UrbanCode Deploy, which runs Chef Recipes to do the actual heavy-lifting

Topic Proposer wishes to discuss how to simplify the deployment process, while maintaining a GUI.

Complexities: 
+ Tough to onboard a new employee due to the variety of tools used
    
Chef Delivery is proposed as a possible solution:
+ Defined delivery pipeline with automated testing
+ Code review gate waits for someone to approve the change
+ After approved, it goes through multiple test phases (Union, Rehearsal, Delivered)
    
What is "orchestration"? Not a single pipeline, tends to be a multi-step process involving disparate components.

How orchestration is done by participants:
- "orchestration recipe" that relies on chef provisioning:
  + halt chef client, go node-by-node to do whatever work is necessary, turn chef client back on.
- custom resource that conditionally includes a recipe which blocks.
  + uses Serf under the covers to determine whether a node should block or not
- use tags to determine whether a run_list item should be included or not
  + tag includes the recipe to run, allows chef client to continue to run normally but include additional recipe when needed
  - orchestration APIs: CFN, Eucalyptus, etc.
    
Orchestration Issue: need to test a multi-node cluster, but timing of what nodes come up in what order, how long they wait before moving on, etc. is important.  It's been discussed in the past about writing a test kitchen driver.  Some participants use DSC resources, some use Rake - no real clean solution for this. What if the Chef Server could be used as the metadata store containing state about the each of the appropriate nodes, whether they're up or not, chef done or not, etc. to help orchestration these multi-node orchestrated deployments?

If Chef were to write orchestration primitives, should those primitives be machine-to-machine type communication, or should the primitives be focused on a centralized controller handling the orchestration responsibilities?  Room seems to agree that the centralized controller is the right / safest option, but edge cases will dictate the need for both. +1

"Can't do CD properly with the Chef Server cluster itself" - participant notes that upgrading Postgres in the chef server requires downtime, found it ironic that Chef advocates for continuous deployment but our upgrade processes are not seamless

# Proposed by: Brian

Should Chef be an orchestrator?
  A desire to do this in one Chef run
  Some work is being done with Chef Provisioning
  Hashicorp Terraform as an alternative model

Easy use case: Cloudera Hadoop with 11 Nodes
  Ansible: Bring up node x before y, establish connections.
  Able to create k,v store. Use the k,v store as a state storing semaphore system
  Con: Introduces some communication between nodes, though now the nodes are no longer autonomous
  Reported Case by deploying Riaak using the same method. Best way is using etcd

Seemingly no angst agaist using mutiple tools. Best tool for the job?
  Monitor as gating factor. Once a node is flagged to be a monitor. Monitoring system as flagging as the needed system as up.
  Done in 2 chef runs.
  Required a bit of planning

Lots of distributed systems don't have config apis. Having them makes it easier for Chef to operate against it.

Using cookbook blocks, this can cause hours of delay. Possible to get around this with push jobs.

You also need to have good SLAs with your users.
+ Would love knife up x...magic!
+ You as the operator dictact to chef what you.it want.
  + ie This vlan truncates here
  + VM waits for its network till..it finds it.
  + So lots of dependencies.
  + Not immediate consistency....eventual consistency as things come up.

Or the etcd model
  + Canary nodes
  + Separated what boxes are doing
  + This requires quite a bit of scale, and knowing what you're doing
  + This also has a bit of a cultural shift (managing expectations)

Doing things "in order" vs "out of order".
  + Out of order requires some robustness, but will lead to eventual consistency, and you don't need to worry about races.

Back to the semaphore, k,v model.
  + Other option is zookeeper-watch, but you're using a distributed system to make a distributed system.
  + Zookeeper is great if everyone is behaving well
  + Also exists an etcd cookbook.

Don't think of the web server needs to discover the load balanacer....
  + The load balancer needs to talk to the web server
  + These things are allowed to talk to the other things...essentially the pull model.

Other needs?
+ Needs to sequence nodes.
  + Again, push jobs as a solution
  + Another technique, short splay during provisioning phase. Once "done", increase it.
  + Set an attr saying it's ready/done.
  + Tagging things with attrs is a great way to know something is ready.
    + So node does thing, add attr to that node
  + Danger of lots of tag, attr cruft hanging around nodes.

+ Using attrs to keep state of various applications
  + Not great to have dozens of apps, and have all these attrs hanging around. This is with 20k nodes.
  + Possible solution:
    + namespacing the attrs
    + whitelist attrs. Best practice to do some whitelisting ohai to improve performance. 
  + When provisioning...a broken chef run can leave things in a half state which may cause issues with idempotency.

  + Anyone trying to do complex state with node saves...etc?
    + With fine grained needs, something that runs every 30m by default may not be the best solution.
    + A chef server you really depend on for state, better be really highly available. So this is why things like zookeeper. Some seem to run chef like zk.

  + Another solution: Caneria cookbook (reference below)

  + Back to the community:
    + These sorts of solutions should be published. Yes it's embarassing but it's better than nothing and it's an idea to be built on.
  + All these things change with scale:
    + Some people try to solve their scale problems with "big company" scale solutions. These often aren't published, and the whole story isn't told, or it's completely overkill for you.
    + Many scale solutions are somewhat custom.

  + Newer generation k/v systems are much easier than the old ones.
    + ie: Zookeeper is a PITA to deploy.
    + Consul ()HashiCorp) and etcd are much easier

    + One story of etcd, stability and split brain issues, but also feature rich.

  + What's chef push?
    + Basically knife ssh...doesn't scale
    + Replacement using ØMQ.
    + Whitelist of commands to run, so you can't run anything. It's just queued up ssh
    + Uses your client key so you can do role based access as well.
    + Jobs are logged to the chef server, instead of just console spill with ssh
    + You could just do chef this way, just push "on demand" (yikes! don't do this all the time in prod!)
    + Of course won't work with hosted chef.
    + This came out one month after puppet mcollective was released.

References:
+ https://github.com/chef/chef-provisioning
+ https://www.chef.io/blog/2014/11/12/chef-provisioning-infrastructure-as-code/
+ https://docs.chef.io/provisioning.html
+ https://github.com/ranjib/chef-etcd
+ http://onddo.github.io/chef-handler-zookeeper/
+ https://docs.chef.io/knife_tag.html
+ https://docs.chef.io/ohai.html
+ https://github.com/ryancragun/canaria-cookbook
+ https://github.com/coreos/etcd
+ https://www.consul.io/
+ https://docs.chef.io/push_jobs.html