## Ruby Cookbook: the Sheddening

Goal:  provide a ruby cookbook to subsume the existing (multiple) ones.

Intended audience:  users with specialized ruby needs not supported by the distro package.

Support the following installation methods, in no particular order:
+ custom ppa (e.g. brightbox)
+ ruby-install
+ compile from source and install
+ package from internal repo
+ omnibus rubies (already consumed via poise-ruby)
+ rvm
+ rbenv

Supported ruby versions:  ruby 1.9.3+

Supported platforms:  Tier 1 (except OS X, where `package ‘ruby’` does the right thing) and Tier 2.

Chef-rvm cookbook goals
- Leverage lots of mixlib shellout to wrap rvm for managing rubies
- Looking at ripping code out from the ansible playbook for rvm (official rvm blessed) and making an LWRP cookbook

Notes:
+ Internal to Chef, we have at least 4 ruby cookbooks in use.
+ Use ruby-VERSIONSTRING naming, as in ruby-build.

- The example from the omnibus cookbook that could be the basis for a 'source' provider:
    https://github.com/opscode-cookbooks/omnibus/blob/master/libraries/ruby_install.rb

### Summary
    - Chef rvm will be rewritten
    - Noah will most likely be plublishing a abstraction for rubies soon
    - Chef is interested in ripping out their ruby-installer stuff from omnibus to create a "thing" (possibly THE ruby cookbook)