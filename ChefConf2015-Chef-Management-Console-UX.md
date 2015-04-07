Performance

Feature Needs
Want to see graphs when they first log in.
 - Errors
 - Stats on Node clusters / Failures. What went wrong, where and when.
 - Be able to see Master / Slave Relationship
 - Maybe viz as a system diagram
 - potential to intergrate with home grown dashboards.
 
- Attribute Searches on nodes
- Being able to share nodes or cookbooks between orgs. 
- Visualization and comparision of attributes between nodes. 
- Query Syntax should be more complex - think Splunk
 
Usability
Policy Tab
- Why do I have to go to Policy to find out what is going on with a Node RunList.
- No good Mental Map to get anywhere - does not even reflect Knife Commands.
- Could not 

Integration
 - potential to intergrate with home grown dashboards.


Could not figure out how to delete a cookbook from the Manage UI.

Split between users: who uses Manage?  Strong ops people typically use Chef, but often the people who use Manage are not the strong ops people but are different people.

Would like to be able to manipulate perms for clients and not just users in Manage (such as using chef to manage laptops). Manage seems to support just users not client. 
Can do this in knife acl, but not in Manage.

Requests for Manage:
Using Chef 12 for HA and Replication. Would be neat to visualize this in the UI.
See which load balancer is master/slave, what the status of things is.
A visualization of this, but also be able to get the json of things so could build your own - in chef server, like the status endpoint.

Want a tool to give visibility to the rest of the organization. Each person has done their own implementation, but each is different and not a great answer from Chef.

How do you report the state of things to people who just want to know status and aren't the Chef users?

The chef-manage-issues repo exists and can be used to find info on manage and to file issues. This is a public repo.

Manage issue as a premium feature probably isn't the best answer. Having a simple subset that is free is probably good.
Have a basic thing that let people know when to panic or not panic.

Having Manage work as a way to lower the barrier to entry would be really compelling.

Find what you are looking for and make it easy - Search/Sorting/Filtering

Wishlist terratory: pipe searches like splunk
An attributes visualizer - to be able to see which attribute lives where and do comparisions across notes.
More complex query syntax
REST-API so you can export to graphite/splunk/etc

One Feature you must have:
+ Dashboard - instant visualization
    
+ Manage search box can execture Solr searches
  + But Manage gives no way to make this clear or accessible. There are no hints on how to do this.

Pain Point:
  + LDAP integation with AD.
    + Populating all the users so don't have to invite each person they login for the first time.
    + Would like to say: All the people in this OU are in the users group and manage through AD.
    + 2 features: support AD groups
    + When new users get added to the group, make sure they get the AD group permissions
    + Let's say fired a user - want them to not have access to everything right now. Want this disable in AD and have it just work and be picked up in Chef.
    + Not being able to configure chef from manage.  Ex: setting up ldap from the user interface

This is a good way to see attributes with Chef browser (search your nodes) https://github.com/3ofcoins/chef-browser

[View original notes in etherpad](https://e.chef.io/p/W4mDvYnsx8)