How to migrate from a chef server with many problems... here's the current world:
+ Hosted Chef 11
+ Version pinning done in roles or not at all
+ One monolithic cookbook repo (hundreds of cookbooks)
+ Many community cookbooks that are downloaded, modified 
 
Approach:
+ Build new chef server bootstrap code to easily stand up on-premises chef server 12
+ Import all repo (cookbooks, data bags, etc.) from hosted chef to new chef server to find any 11->12 upgrade
+ Move nodes as appropriate per team

Migrate cookbook from monolithic repo to github.com private repos
+ Squash git history per cookbook and upload to github private repo per cookbook
+ Keep track of master list of all cookbooks and their locations in a master-cookbook-list Berksfile (this replaces the 'cookbooks' dir in the chef server chef repo)
+ Populate jenkins CI/CD pipeline from that master-cookbook-list
+ Can be scripted
+ All changes then go through pipeline to get pushed to chef server

How to un-pin from roles
+ Move current production versions of cookbooks to cookbook_version list in production environment of new server
+ Delete pinnings from old roles

Migrating to new versions of community cookbooks
+ Download same version of community cookbook and do diff to 
+ Try to go to latest version of the community cookbooks and see what breaks

Migrate role by role
+ Also has additional benefit that when you're done migrating all in-use roles any cookbooks that weren't pulled over can be ignored/deleted

Create data center cookbook that has location-specific attributes e.g. postfix/LDAP
+ Or consider data bags for data-center specific settings

Knife solve # dep-solver plugin to use what's actually in used

Code to write out cookbooks and versions
```
# Let's set some attributes for all the cookbooks (and versions) we used for this chef run
cookbooks = run_context.cookbook_collection
cookbook_vers = {}
cookbooks.keys.each do |cb|
  cookbook_vers[cb.to_s] = cookbooks[cb].version.to_s
end

node.default['cookbooks'] = cookbook_vers
```