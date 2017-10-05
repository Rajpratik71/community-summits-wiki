# Policyfile Inheritance (RFC)
This is an update to the original "[Multiple Policyfiles (RFC75)](https://github.com/chef/chef-rfc/blob/master/rfc075-multi-policy.md)" 
1. Adds directive to Policyfile with `include_policy` 
1. De-duplication of dependencies at `chef update`
1. A fused lockfile is computed from remote (git) and local policyfiles
1. Nuance: Every time child is `chef update` the parent is updated

## Problems with RFC075
- This does **not** work on Windows platform (Ruby does not provide #fork)
- Consecutive policyfile runs from the `policy_name` attribute (#Array)
- Serially, independent, no resource protection between chef-client cycles

## Action Items
1. Additional syntactic sugar to the Policyfile DSL (update attributes, parent attributes)
1. `include_policy` source being the Chef Server (specify the `policy_group`)
1. RFC for globally turning off the `ignore_failure true`. 

