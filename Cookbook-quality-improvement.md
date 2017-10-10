* Chasing standards is hard
* There is a Chef Cookbook Certification Program (CPCUP)
  * Can access via Supermarket by checking a partner box to find them
* Quality standards are hard to enforce
  * Some cookbooks have external resources that can't be tested via integration
  * ChefSpec is faster while integration is a lot slower. It's a quick safety blanket versus the slower build cycle of a bigger integration test suite
* Can you generate ChefSpec Tests?
  * ChefSpec can catch data entry errors easily
* Use kitchen dokken and inspec to test things quickly and effectively
* Testing edge cases with resources feels faster in ChefSpec
* Check out Bento for a build system for building all the various images for testing via test kitchen
* Unit testing Chef is difficult to do with Chef
* What about community cookbook quality?
  * There is a repo for that (tm) https://github.com/chef-cookbooks/cookbook-quality-metrics
  * Cookstyle vs Chefstyle for linting code
  * Why can't Chef have more opinionated policies for cookbook quality?
  * Some cookbooks are complex and opinionated like the users cookbook while ones like tomcat are really complex because it supports a lot of options
  * Can there be a Python Pep16 for Chef? Rubocop with Cookstyle seems to be the closest thing
* Can the supermarket display the quality metrics on the search results? A summary of number passing and failed tests
* Wish foodcritic could run on the rubocop engine
  * rubocop does not have good documentation on how to extend it
* Opinion: Community cookbooks should just be custom resources to make them able to be composed. No recipes.
  * Also they should have a test cookbook that consumes that cookbook
  * Should the ChefDK generate these? What about a community generator?
* Supermarket could add a "I use this" type +1 to a cookbook to endorse it as a metric

See also the [Cookbook Quality Metrics notes from the London Summit](Cookbook-Quality-Metrics).