# Policyfile Inheritance (RFC)
This is an update to the original "[Multiple Policyfiles (RFC75)](https://github.com/chef/chef-rfc/blob/master/rfc075-multi-policy.md)" 
1. Adds directive to Policyfile with `include_policy` 
1. De-duplication of dependencies at `chef update`
1. A fused lockfile is computed from remote (git) and local policyfiles
1. Nuance: Every time child is `chef update` the parent is updated

## RFC75 - Multiple Policy Runs
- This does **not** work on Windows platform (Ruby does not provide #fork)
- Consecutive policyfile runs from the `policy_name` attribute (#Array)
- Serially, independent, no resource protection between chef-client cycles
