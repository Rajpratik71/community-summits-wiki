* learn.chef.io module - https://learn.chef.io/modules/keep-your-cookbooks-up-to-date/#/

* omnitruck mirroring for airgapped environments
  * use the chef server to run an omnitruck api

* knife plugin to show chef server and chef client versions
  * https://github.com/kkenny/knife-inventory/blob/master/inventory.rb - does not show chef-server version but is good for client

* requirement for `new_resource.<method>` probably hardest behaviour change for 13 -> 14

* rubocop rule name changes are painful

* resource cloning is bloody hard to describe. https://docs.chef.io/deprecations_resource_cloning.html

* what happens with cookbooks that are no longer maintained?
  * quality metrics to make it clearer when you shouldn't pick a cookbook
  * sous-chefs to help maintain and own unmaintained cookbooks

