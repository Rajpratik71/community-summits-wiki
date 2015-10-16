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