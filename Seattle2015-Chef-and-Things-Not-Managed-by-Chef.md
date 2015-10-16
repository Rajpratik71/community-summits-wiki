Couple things we want to talk about
1. Controlling things that you can not put Chef Client on.
2. When Chef is not the canonical source of truth

An example of this. Chef on Windows. Integrate with AD using Chef Vault authentication.

domain-join cookbook.

Mostly writing LWRPs that wrap MS tools to do the job. 

When the tool is a command line tool, parsing their output sometimes sucks.


When a thing can not have Chef Client, we have been using an intermediary node. Devices register with an intermediary node. 

Similar to a provisioner node that is not provisioning.

This is great for consistency. Everything is in Chef.

Works very well for things that have APIs.


It is not easy when there are no APIs. For e.g. switches that can only be talked through special ports.

How does one do it with Chef? 

Adapters? They have special ports that can convert the special port to SSH. 

Security Appliances? / GUI - SSH


Is there a Ruby expect? Yes: pty gem. 


When using the intermediary node, Chef Client is used with more than one identity so that you can see each device separately on Chef.

Where is the mapping between devices and intermediary nodes?

One way to do it is with ohai plugins.  Ohai is a gem that comes with Chef Client that can collect all the metadata information about your nodes / devices.


Learn Chef is a great place to start.


I have a bunch of nodes. They need to get something from authoritative source. I don't want to have all the nodes have the credentials to talk to the authoritative source. CMDBs, IPAM

Have an intermediary that collects the information and puts it into a data bag.

You might not want to make the secure information queryable with proper security.


Have multiple instances of Chef running on one node as proxy: See the above intermediary node concept.


It makes sense if there are a small number of nodes but if you are directly managing a lot of devices Chef might not be the right tool. 


Databases?

Trying to manage schema through Chef is not good since it is not idempotent.

As a database person, make the system look correct but other stuff should be the responsibility of a different tool. 


How about things that want to talk to Chef Server? 

One use case is to want to push state into Chef to keep it a cannonical source of truth. 

I have a bare metal provisioning tool in phyton. I want to create a client in Chef and use that client as the identity of the machine I provision. 

S3 => Use the aws cookbook. Chef Provisioning.