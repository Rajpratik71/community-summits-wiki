# Post-mortem Report

### Post-mortem Facilitator: Jay Mundrawala

1. Failure Happens. Mistakes Happen. This is a blameless Post Mortem.
2. We assume everyone participating in the project wants to do a good job.
3. We will not focus on the past events as they pertain to "could've", "should've", etc.
4. All follow up action items must be actionable and have a participating individuals commitment to implement, design, or otherwise achieve them.

## Description

Chef 12.2.0 introduced a bug which rendered Chef Client unusable for anybody using Chef in cases where the HOME environment variable was not being set, such as through their init system.

## Timeline (PDT)

* 2015-02-26 19:00 Chef Client 12.2.0. released
* 2015-02-26 20:00 [Issue 3153](https://github.com/chef/chef/issues/3153) reported on Github
* 2015-02-26 21:00 Fix for Issue 3153 posted in [PR 3153](https://github.com/chef/chef/pull/3154)
* 2015-02-27 Fix for Issue 3153 is merged
* 2015-02-27 09:27 Build is started for 12.2.1
* 2015-02-27 11:04 Build fails because of network connectivity issues
* 2015-02-27 11:10 Build restarted
* 2015-02-27 12:23 Build fails because the failed nodes from previous build were in a bad state
* 2015-02-27 12:39 Workspaces wiped for bad nodes. One node refuses to allow us to delete workspace
* 2015-02-27 1:50 Start rebuilding broken node
* 2015-02-27 4:50 @coderanger asks for an official message about the issue
* 2015-02-27 5:04 new builder is up, new build kicked off
* 2015-02-27 5:10 We see build will fail because the new builder is not fully bootstrapped with all needed software
* 2015-02-27 5:13 Chef Inc started internal incident because of bad release, everyone is working to nuke the release
* 2015-02-27 5:20 Status site and Release blog post updated
* 2015-02-27 5:20 Chef client yanked from omnitruck and package cloud
* 2015-02-27 5:34 Chef client yanked from rubygems
* 2015-02-27 5:48 New build node ready to build chef client
* 2015-02-27 5:51 Incident over
* 2015-02-30 Chef 12.2.1 Released

## Contributing Factor(s)

* Tests did not cover this way of running Chef
* Build environment was having issues
* No internal procedure for yanking bad releases

## Stabilization Steps

* Chef Client 12.2.0 was yanked
* Bugfix release 12.2.1

## Impact

* Any users using Chef Client without a `$HOME` variable would be unable to start chef-client

## Corrective Actions
* Chef Client will have automated integartion tests that run similar to the way people run Chef * kartik
* Release Process RFC * jdm
* If a fix has not been released within X hours, define a process to move forward (trigger incident) * btm
* Process for yanking a bad release (RFC)
* Communication process for blocker level process
  * twitter
  * mailing list
  * IRC
  * blog
  * Public Information Officer

# Maintenance Process

Lots of talk, but start with RFC 0
github.com/chef/chef-rfcs

Even more notes available elsewhere!
+ http://dragoon.io/2015/04/07/chefconf-2015-community-summit-retro/