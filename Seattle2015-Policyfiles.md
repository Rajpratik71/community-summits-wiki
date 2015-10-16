# Session 1: Policy Files
Policy files 101
- problem it solves:
- eliminates need for Berkshelf
- roles are unversioned:
- "doesn't actually address that!"
- managing cookbook versions
- transient dependency versioning
- chef server dependency resolver produces unexpected solutions sometimes:
    - the process is invisible to the user
    - policyfiles aim to make it explicit
- goal is to automatically pin cookbooks with their use
- would need to rewrite roles as policyfiles
- policyfile in Ruby, get a .lock file
- versioned via hashes of constituent cookbooks/recipes
- policy files tend to map to different phases (aka "environments")
- e.g.: put 1% of prod nodes in prod-canary, measure, evaluate; then roll forward or back off

Chef-zero/chef-solo anything over Berksfile?
- can provide runlist

Heavy users of roles may not care

How about with environments?
- (use wraper cookbooks instead of roles)
- policy "groups"?

Chef environments
- cookbook pinning
- inherent with policyfiles
- every time you update the policyfile, it gets a new version

Granularity of policyfiles
- by environment, data-center, etc.?
- contract of roles providing attributes to cookbooks
- use data bags to provide an intersection of concerns
- co-version attributes with cookbooks, put them in a policyfile

Precedence?
- policy files replaces environment and roles, so polcyfiles attribute precendence similarly replaces it

Named runlist replacement for override runlist
- e.g.: add a service to a machine

Things can break if cookbooks depend on environment attributes

Chef Provisioning, in progress to give it policyfile capability
- ChefDK can put some 
- Chef Client 12.5, upcoming Chef Server, policyfile json can exist on node

Some folks having problems using Chef Provisioning

What's the plan with the runlist?
- will deprecate?
- no plan (yet) to deprecate other ways of using Chef

With proliferation of ways to do things with Chef (e.g.: policyfiles, environment + roles), folks can get themselves into a difficult place
- try to build cookbooks that expose resources

Policyfiles + Chef Solo?
- RFC to do something with Solo(?)
- some difficulty using policyfiles with Chef Solo(?)
- a little tricky, avoid overlapping
- plans for prioritization of conflicts?
- policyfiles require a line for a cookbook, even if it's not in the solution

Using Roles & Environment, can I shim in a different resolver?
- Are policyfiles going to deprecate anything?
- No plan right now to remove any other stuff -- would be way too disruptive ("a dick move")

If you have a number of policyfiles, and you need to update a cookbook version, do you have to edit all your policyfiles?
- somebody wrote something to generate policyfiles
- seems to drive the need for some layer to better manage policyfiles

Makes sense to check in policyfile lock file at first
- with more sophisticated setup, might have tooling manage lock file

Chef will add 'composition' to policyfiles
- can support something like what a base role would do
- whatever attributes to share across policyfiles, just update one file

Naming recommendations for policyfiles (to facilitate search)
- machine name + environment

How to search what nodes have a cookbook in its runlist?
- chef-client will populate runlist based on policyfiles

# Policy Files

Dan D 
   
Some Berkshelf things work well.  Dependency solvers are good.  Chef servers don't know what Berksfile are though.    

Compare policies with chef-solo.  Basic advantage vendored cookbooks together.


Migration from roles, environments to policy files.  Convert all roles to policy files.  Sort of big migration.
     
Migration from wrapper cookbooks, environments, no roles.  Policies have versions and revisions map them to deployments. Talks about implementation methods, split out small group of nodes to implement some of the servers.  
    
How do we override by data center.  Could have policy group by data center?   Data bags to supply attributes is possible.  If you want attributes with the code you can put the attribute values in the code.

May need to build hierarchy into the policy files.
    

Attribute precedence - policy files replaces roles.
    

Any way to add role equivalent quickly to a server - named run list might work.  They are a replacement for override runlists.

What are environments in this set up, right now it's a hard error.  Searches need to be updated, but these decisions are open to change.

One purpose is to get rid of environment pinning.  

    
If you have an existing node changed to policy mode, the runlist converts to essentially comments.

Recommended way to provision a node (cloud init, chef provisioning).

    

Plans for runlist - no plan to deprecate runlists, roles, nodes in the near future.

Best and common practices are hard to drive out.  Going to recommend policy files first. 

Polciy files chef-solo willl be replaced by local mode. Couldn't follow the discussion.

    

Chris Roberts - use different resolver.  Doesn't want policy files.

Dan the resolver can be replaced.
    
Christine - Do I need to update multiple policies to make slightly global change.   Response - not clear.  Inform application owners of the need for updates.  Policy files manage artifacts, they are not the artifacts themselves. Pipelines may need to own the lock files. Planning to add some sort of compostion, so policy files can include some sorts of secrets.
    

What problems are you solving?
+ Roles are not versioned. May or may not have solved this.
+ Workflow rfc.  
+ Get the same cookbook versions and solutions.
+ Dependency solver rage.  Produces unexpected solutions.Possible cookbook combination will run together for the first time in production.
+ Aiming for safer implementation.  Limit ability to shoot self in your foot.


Nathan - how do you use search?  Similar to existing methods.  Chef server 12.3, node objects will have policy name and group. 
     
Multiple folks - confused discussions.