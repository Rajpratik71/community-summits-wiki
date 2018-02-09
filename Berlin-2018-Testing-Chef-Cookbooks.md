* Ops folks found writing unit tests hard but settled on test-kitchen as being close to their experience
* Switching from serverspec to InSpec

* overview of testing tools

* Unit Tests are problematic, since many people value code coverage and end up writing ChefSpec that tests Chef itself rather than the recipes.
  * some people use unit tests to avoid writing docs

* clustered test-kitchen testing
 - hard since you need an orchestrator
 - kitchen-dokken

* Discussion of kitchen-dokken - what it is and how it works

* Running own supermarket?
  * mention of [minimart](https://github.com/electric-it/minimart)
  * vetting of community cookbooks

* Best practices need alignment

* Many people look at chef-cookbooks and sous-chefs to see how to write good cookbooks.

* Might be good to talk about "Desired State" as a mindset for cookbook authoring?

* People find it hard to reason about what their cookbooks are doing and how to improve them

* Test Kitchen multi converge - 
  * `multiple_converge` and `enforce_idempotency` - https://docs.chef.io/config_yml_kitchen.html
  * be nice to run first converge with one version of cookbook and then second with newer one

* Federated chef servers for reducing blast radius of changes.