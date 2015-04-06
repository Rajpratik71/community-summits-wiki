Common Woes
- May not be a "right" way that is also transferrable for newcomers


Attributes in templates
- Makes it difficult to follow where things are coming from
- Data "jumps" over the resource and seems to override (using attributes)
- If recipe relies on using attributes, you are locking in users to your methods
- Provider should be providing all of your template parameters (don't hardcode anything)
- Template content attribute (https://github.com/poise/poise/blob/master/README.md#template-content)


LWRP Model
- One provider for each component seems to not be used much anymore ever though it might be one of the better approaches
- Resources are the fundmental components (focussing on these enable max reusability)
- If you want to create examples, you can shove them under the test/integration or test/fixtures so that the cookbook isn't uploaded
- GREAT EXAMPLES mysql(https://github.com/chef-cookbooks/mysql) and httpd cookbooks (https://github.com/chef-cookbooks/httpd)
- Can then wrap all things into a nice cookbook like this https://github.com/someara/wordpress-uberdemo



Attributes
- Attributes dependancies are great at setting default values for resources/providers
- Attributes originally designed to be "tunable knobs" 


Global wins
- Write more resources/providers, less recipes


Alternative approaches for LWRP (deep in the rabbit hole)
- Write gems and "convert" them to cookbooks with HALITE https://github.com/coderanger/halite
- Example from poise (https://github.com/poise/application_git), (https://github.com/poise/application_ruby)
- Can subclass core chef to add more features
- Can use poise(https://github.com/poise/poise) to provide additional functionality to your LWRP


View original notes on [etherpad](https://e.chef.io/p/cookbook_patterns)