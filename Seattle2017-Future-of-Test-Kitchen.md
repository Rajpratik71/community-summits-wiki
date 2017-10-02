# Future of Test Kitchen

Public Safety Tip: don't use:

- kitchen-ssh
- kitchen-fog
- kitchen-package
- kitchen-localhost

## Providers

Conceivably, all of these providers ought to be included in the ChefDK so that conflicting dependencies can be caught early.

Providers we know are in use (tier1):

- vagrant
- ec2
- dokken
- vsphere

Providers we don't know how much are used (tier2):

- azurerm
- google
- digital ocean
- docker
- openstack
- proxy
- terraform (?)

## Kitchen Roadmap

### Near:

- auto-upload fixture cookbooks (we're gonna do you a solid)
- [telemetry](https://github.com/chef/chef-rfc/pull/270)
- deprecations
  - legacy SSH
  - mixlib install script (will require changes to kitchen.yml if you want to control the version of chef-client installed)
  - driver_config
- explicitness (e.g. virtualbox is vagrant default)
- kitchen-doctor
- kitchen-shell
- pre_create_command
- new driver `exec` (or something) which is basically `proxy` but exec instead of ssh (replaces `kitchen-localhost` functionality) with a big warning that TK's changing your host

### Far:

- chef -> external
- build bridges to other TK projects
  - kitchen-ansible
  - kitchen-puppet
  - kitchen-salt
- deprecations
  - remove `package` (just use packer)
- more test output formats
  - junit if there will only be one

### Farther:

- [multinode RFC084](https://github.com/chef/chef-rfc/blob/master/rfc084-test-kitchen-multi.md)
- multi-converge/suite (N)
- lifecycle hooks
- maybe re-implement `package` as a verifier if the telemetry data shows it would be used and we've got multi-verifier through lifecycle hooks
- faster and refactored transports

## Ideas

- driver vagrant default explicitly spits out `virtualbox` to make it clear what the default is to inspire user twiddling
- document
  - dark arts around custom Vagrantfiles so we can avoid making kitchen-vagrant even more complicated
  - tell people about the directories that are magical
  - how to test chef vault with fixture data bags and the helpers that fallback

