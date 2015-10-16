Another Note Taking Partay! Woot woot! 
😃 
2015-10-15 @2pm in Issaquah Room

# Emerging Anti Patterns in Chef

Facilitator: Naomi

Intro:
    Some time ago it was proposed to create an "Unlearn Chef" talk

"Yeah...you probably shouldn't be doing this"


## Good practices:
+ Abandon Attributes for Libraries (aka stop using attributes.... so much)
+ "It's ok to hard-code your values" but not for community cookbooks.
+ Design for what you need to day - don't design for "in the future, we might need ... "

Don't do "X" actually means Don't do so much of "X"


__Anti-Pattern__: Conditionals that use node attributes creating a lot of code branches
+ This is untestable

__Anti-Pattern__: trying to customize all the things using attributes
+ Attributes are global variables so using them often does not allow you to use them in a reduced scope
+ Using too many is a code smell
+ Old pattern: an attribute for every single configurable thing.  
+ New pattern: Model the configuration you need and then... teach chef to create the configurations for you
+ Node attributes are leaky... passwords are problematic because they're insecure.  
+ Sprawl with attributes: Too many attributes... indicator that your cookbook does too many things.  

__Anti-Pattern__: How cookbooks handle passwords
+ Committed in clear-text to source control
+ Noah K has a blog on the different options (https://coderanger.net/chef-secrets/)
+ Joshua Timberman did a blog on Chef Vault (http://jtimberman.housepub.org/blog/2013/09/10/managing-secrets-with-chef-vault/)
(but Chef Vault is incompatible w/ Autoscaling, so if you're in AWS, use private S3 buckets and IAM)
The bad idea list of __Storing secrets__:
    __Encrypted databags__ - Bad
    + YouReally bad are using only one key to give access to a lot of other secret information. 
    + Plus this single key is distributed to everynode to get access.
    + does not support key rotation
    __Databags__ - Really bad
    __node attributes__ - Really, really, really bad
    + error prone
    __Source control__ - Terrible

__Tool__: Chef-vault
    + Manages the secrets in databags
    + uses client keys to allow access to the vault
    + If you use auto scaling you cannot know the client key before so you cannot grant access
    + Good for static scales though
    
Lots of other options like, hashicorp's hashivault, and .... ???

__Anti-Pattern__: Cloud autoscaling
+ If the cloud is scaling its creating a lot of dead nodes.
+ Must clean up later 
+ Causes bloat in your backup too.  
+ Therefore need to add something like a shutdown script to delete. (but you won't want to restart a machine then)
+ ephemeral aws nodes dissappear - maybe use sns to notify cleanup process
+ Can write a listener to AWS Autoscaling during scale-down events from SNS
+ Can also say, anything that hasn't converged in a set amount a days (like 3 or 7 if you're converging every 15 minutes) just delete

HACK DAY IDEA: what was this??? Joe mentioned it. (removnig auto scale nodes automatically?)
what about the zap cookbook I just heard about?

__Anti-Pattern__: Recipes
+ Need to make shorter recipes
+ Use providers to vary per plat
Internal vs Community
+ it's okay to write recipes if the thing you need is in it.  
+ keep it simple
+ if you pay the cost of actually get into chef spec (or pure ruby), the rspec returns fast (instead of having to take a walk for results)
+ keep recipes declarative
+ no God functions! It hides logic
+ Using action :nothing and notifying later is a 
-w/ recipes with many resource calls (for example: action:nothing, w/ notify later on), it's difficult to follow due to the branching logic.
+ keep things as simple as possible for non-ruby developers.  So if they need to just change something like a path, it would be easier.
+ beware with your use of notifications.

__Anti-Pattern__: Numerous Notifications
+ Some are ok, but a lot is a code smell
+ Everything action :nothing and notify is a extremely hard to follow
+ Are kind of like GOTO statements
+ what do we do instead?
  + Use libraries and helpers
  + Keep the recipe declarative try to move logic elsewhere
+ why are notifies so prevelant and not subscribes? This is due to it chef compiling a subscribe to a notify anyway.
+ Erik Hollensbe chef resource run queue (http://erik.hollensbe.org/2013/03/16/the-chef-resource-run-queue/)

__Anti-Pattern__: Don't use numbers for modes
  mode 0755 should be mode "0755"
  Must turn it to a string.
  Food Critic will warn you.

__Anti-Pattern (pro-pattern)__: Cookbook Quality
+ We want to gather metrics about cookbooks 
Tools: Rubocop and foodcritic
+ Rubocop is opinionated.
+ Chef Style Guideline
+ Make sure to commit your code before running it so you can see diff
+ Write your own food critic rules/tests to implement the style you have agreed upon

__Anti-Pattern__: Policyfiles
+ too young to know all the wrong ways?
+ designed with CD approach in mind.

__Anti-Pattern__: Knife cookbook upload
+ always use w/ --freeze
+ you can put chef guard in front of your proxy server
+ Chef Push (uses new policyfiles system)
+ Berkshelf (uses freezing by default)
+ Humans should not run this (do it using CI)
+ Contention from multiple players

__Anti-Pattern__: HUMANS
+ fire everyone and replace them with cookbooks :D

__Anti-Pattern__: Going cheap
+ New teams try to go cheap by going for 3 chef-servers for 5 people
+ Should get a VM per person
+ Use test kitchen

__Anti-Pattern__: For new people to Chef, are there any?
+ Seriously though... You can't follow all of these right away. Newbies need to use the tools at hand and grow 

__Anti-Pattern__: Wrapper Cookbooks
A decision was made "any community cookbook, we're going to wrap", and now it's a mess.
+ Use the community cookbook as is - and pin the version (a "quality pin")
+ Wrap when you need to change something
+ One repo per cookbook is OK

__Anti-Pattern__: repos per cookbook, what's the anti-pattern?
+ Put the cookbook in the application repo ok?  Yes
+ Monolithic repo OK?  Yes. If managed well. Policy files can help manage the versions

Delivery Truck - in the Chef Cookbook Store
Chef Delivery Sugar


CHAT 
(yes i know there is a chat to the right #YOLO)
This is LARGEST etherpad I've come across this summit Woot woot!

Welcome to the partay!!! :D
If only we had gifs...GIF PARTY <--- totally)
I have done all of these anit-patterns. Some are still in place. I have a busy weekend ahead of me.