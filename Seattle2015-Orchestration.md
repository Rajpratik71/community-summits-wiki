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
    Tough to onboard a new employee due to the variety of tools used
    
Chef Delivery is proposed as a possible solution:
    Defined delivery pipeline with automated testing
    Code review gate waits for someone to approve the change
    After approved, it goes through multiple test phases (Union, Rehearsal, Delivered)
    
What is "orchestration"? Not a single pipeline, tends to be a multi-step process involving disparate components.

How orchestration is done by participants:
    - "orchestration recipe" that relies on chef provisioning:
        halt chef client, go node-by-node to do whatever work is necessary, turn chef client back on.
    - custom resource that conditionally includes a recipe which blocks.
      uses Serf under the covers to determine whether a node should block or not
    - use tags to determine whether a run_list item should be included or not
      tag includes the recipe to run, allows chef client to continue to run normally but include additional recipe when needed
    - orchestration APIs: CFN, Eucalyptus, etc.
    
Orchestration Issue: need to test a multi-node cluster, but timing of what nodes come up in what order, how long they wait before moving on, etc. is important.  It's been discussed in the past about writing a test kitchen driver.  Some participants use DSC resources, some use Rake - no real clean solution for this. What if the Chef Server could be used as the metadata store containing state about the each of the appropriate nodes, whether they're up or not, chef done or not, etc. to help orchestration these multi-node orchestrated deployments?

If Chef were to write orchestration primitives, should those primitives be machine-to-machine type communication, or should the primitives be focused on a centralized controller handling the orchestration responsibilities?  Room seems to agree that the centralized controller is the right / safest option, but edge cases will dictate the need for both. +1

"Can't do CD properly with the Chef Server cluster itself" - participant notes that upgrading Postgres in the chef server requires downtime, found it ironic that Chef advocates for continuous deployment but our upgrade processes are not seamless