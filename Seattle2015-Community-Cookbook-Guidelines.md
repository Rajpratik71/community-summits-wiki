There are no guidelines for contributing to community cookbooks. Peple are complaining in some cases about quality of cookbooks in the community, but there are no clear guidelines or standards set by Chef. 

There is a community initiative called cookbook quality metrics 
On the chef cookbooks github repository that has been proposed by Nathen Harvey and the community Engineering team.
The cookbook team is fairly new, but there are more people assigned to helping to maintain community cookbooks. 
There are 13 quality metrics that start to define the quality of community cookbooks. 
The long term plan is to pull that into Supermarket and automate these metrics. 
Some metrics include:
    publish to supermarket, version, support for platofrms, rubocop, foodcritic, etc. 
Should be fairly easy to bake some of these metrics into foodcritic. 
Writing and/or guaging quality of cookbooks is a skillset that contributors develop - how to understand, and use community cookbooks effectively. i.e. wrapper cookbooks. 
As people are new to Chef, they aren't familiar with cookbook
Rating system could potentially discourage people from contributing

Do we have any guidelines or rules for how to contribute. Do you write a new cookbook? Or do you send a pull request?
There is also a bad taste left 

would like to see semantic versioning
Sometimes a pull request gets accepted and the version doesn't get bumped, which is difficult when using in an internal pipeline

Supermarket forces a semantic version bump, but there is a way to override

Right now, community engineering team is collecting data to come up with a metric system

Matt Ray from Partner Engineering - What is a good cookbook? 
Reference community guidelines - https://github.com/chef-cookbooks/community_cookbook_documentation
+ a README
+ Rubocop
+ Foodcritic
+ ChefSpec
+ Using Test Kitchen is much easier that ChefSpec sometimes. 
+ Using an attributes file
+ Document Dependencies - other cookbook dependencies and Chef version dependencies. 
+ Windows Support
+ Use Resources instead of Executes


Suggestion: Test for idempotency? Re-run Chef-client and parse the output 

To attribute or not to attribute? Nebulous


Post converge server spec that actually tells you if it works.

When speaking with vendors, partner team says to vendors that they will take pull requests from community members for additions and feeatures.

Code Climate is in progress


Rubocop -a use - iterate through changes, pull request
But only fixes cosmetic issues. Doesn't necessarily 

"When you get people to think about these things they may accidentally write a good cookbook. "

Is there any way for us to enforce a README? This is a governance issue. 

There is a plugin called knife cookbook doc that helps you document your cookbook as you write it: https://github.com/realityforge/knife-cookbook-doc 


Do people think ChefSpec is useful? It's nebulous until users realize the value in unit testing. 
Operations people will likely have an easier time with test kitchen because of the way that they are used to testing. 
Chef Spec will tell you if the code will compile. 

Instead of testing across many platforms using test ktichen, test over 1 platform and use ChefSpec and Fauxhi to make that process faster

Community Engineering: In the cookbook readme, the SCOPE of the cookbook. What it does  and what it does not do. 

"Chef Spec was difficult to learn because it was indirect - instead learned RSpec first. 
Use BetterSpecs.org asa guideline for RSpec

Use a commented out description of the test is helpful so that the next person does not have to figure out what the "expect" line is testing for. 

"I've seen developers just use straight ruby code in cookbooks"