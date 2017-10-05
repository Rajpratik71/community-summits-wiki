# Policyfile Inheritance (RFC)
1. Adds directive to Policyfile with `include_policy` 
1. De-duplication of dependencies at `chef update`
1. A fused lockfile is computed from remote and local policyfiles

## RFC75 - Multiple Policy Runs
- This does **not** work on Windows platform (Ruby does not provide #fork)
- Consecutive policyfile runs from the `policy_name` attribute (#Array)
- Serially, independent, no resource protection between chef-client cycles
