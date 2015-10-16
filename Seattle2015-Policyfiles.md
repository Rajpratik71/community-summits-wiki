Session 1: Policy Files

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