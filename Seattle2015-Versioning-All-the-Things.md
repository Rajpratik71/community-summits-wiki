# How to version the unversioned
## Role and Environment Cookbook pattern
Seperate the code from the data, give them their own pipelines and use git veriosn tags to align the two at deployment

Don't version the environment file, CREATE IT each time.  Aka environment files don't exist in source control.

Keep the applicatoin code in the same repo as the cookbook.  The application version is the smyver version as the cookbook
Master Level Cookbook drives cookbook dependencies and also has the code.
## Policy files 
 - a way of describing a known state and creating an artifact - treat it as a single item
 - ignores version numbers in metadata.rb
 - single artifact with cookbook versions at time of creation are pushed up to Chef Server using a unique id
 - policy files use a seperate API endpoint
 
 https://github.com/chef/chef-dk/blob/master/POLICYFILE_README.md
 
 ex.  Dev/ QA/ PROD policy groups - attach to nodes and guarantee your nodes pull what is in policy.lock
 
 https://www.chef.io/blog/2015/08/18/policyfiles-a-guided-tour/     - Great blog post by Dan Deleo
 
 Upcoming Feature Enhancement - policy file layering
 
 Policy Files supercede integration with existing roles and envrionment pinnings
 
 `chef export policy`

Can set policy in client.rb on node, or via knife node edit => Policy group, policy #

Is there a knife node subcommand for editing policy files???

- Create multiple policy groups for a staged rollout to different environments
- None of the existing functionality should be depricated (anytime soon?)

How to view what policy file is on a node?  Knife? Currently knife node show doesn't show policies/policy groups (just tested with chefdk 0.9.0)
(Ignore run list on node, its defined in the policy)

OHAI plugin to solve problem below:
    Machine A depends on recipe B v1
    Use knife search to identify any nodes still on v1, once v1 not used, it's dead   - instead create ohai plugin with cookbook dependencies
    
    

Policy files won't be 1.0 until docs and training are ready
 - guidelines for migration path from roles to policy files will be made available