## What are metrics of good cookbooks?
* That the runs are fully idempotent
  * all bash/executes/powershells are guarded
  * maybe use multiple kitchen runs to verify
* Documentation is solid (see below)
* Having custom resources is great sign

## Cookbook Documentation Could be improved
* README has a section for Attributes, Libraries, Resources, & finally recipes
* Suggesting a Documentation strike team or docs day for SousChefs
* [chefdoc.info](http://chefdoc.info/) was brought up
    * YARD for chef cookbooks could be a bigger part of ensuring good docs.
* [Knife Cookbook Doc gem](http://realityforge.org/knife-cookbook-doc/)

## Metrics that show low quality/that caused huge headaches to community members
* Calling `node[]` or `node.` inside template hides logic that should be set with `variables(`
* too much logic in templates is a bad sign of hard to read behavior
* A large amount of metadata dependencies is a bad smell for a cookbook that can cause problems
* multiple dependency version pins in community cookbooks also cause HUGE headaches with depsolver issues which are hard to troubleshoot
* community cookbooks that use attribute precedence other than normal cause problems with wrappers and hide other problems with logic.

## Other suggestions
* Make the cookbook quality tool a lib that can be run outside of supermarket for testing before uploading.
* Cookbook quality should be considered a weighted thing on search.
* We'd like a way to share and easily use community foodcritic rules. Maybe something like what InSpec now has.

See also the [Cookbook quality improvement notes from the Seattle Summit](Cookbook-quality-improvement).