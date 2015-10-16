Log:
[Nell Shamrell](https://twitter.com/nellshamrell) introduced
Seth Thomas ([@cheeseplus](https://twitter.com/cheeseplus)) started the conversation
# Thoughts?
# Questions?
1. Suggestions 
2. Question: What delineates recipes vs. cookbooks?  Where is the divide?
  1. Answer: it depends.  Do not put logic in attributes, recipes should be minimum viable thing
  2. One opinion: service is a cookbook, aspect of a service is a recipe
  3. if setting at attribute hurts, should make a resource. If it does not hurt, it is probably fine.
  4. cookbooks are units of release in Chef world, aka an artifact
3. What is best process of starting development process with Chef?  Where is this journey taking us and what is the next step to do testing, learn resources, etc.?
  1. Answer: all cookbooks are 0.y.z until I have integration and chefspec, then it becomes 1.0.0
  2. Start with serverspec - rspec library, lets you write tests for what ports are listening, services running, etc.
http://serverspec.org/
  3. Technical limiitations vs. political limitations - start with something you can blow up completely and that has clear business value to sell Chef to business
  4. Figure out where you are starting in organization, do SIMPLEST thing that will ADD VALUE.  Testing - find what you are comfortable with, add a check for last thing that went wrong
  5. Specifics - start with test kitchen, if it's not there you need it there, base level.  Then server spec.  Then ChefSpec.  Integration testing - more obvious value upfront
  6. Start at middle, not at the beginning 
  7. - BATS - uses bash rather than rspec
     https://github.com/sstephenson/bats
4. what is best way to get into Chef, what coding language should I learn to use with Chef
  1. Chef uses Ruby, but don't need to know all of it immediately - people start by taking bash/powershell scripts and put it into Chef, then slowly refactor into Chef resouces, etc.  More ruby you know, easier to get into Chef internals.
  2. Nordstrom - teaching Powershell users to use DSC, good to focus on at first
  3. Chef Docs - "Just Enough Ruby for Chef"
  https://docs.chef.io/ruby.html
5. Core standards for how we write cookbooks, recipes, etc.  At what point is that a good idea?  At the beginning or as we're learning?  When do we dictate best practices.
  1. Be cautious of internal standards, use community standards, code reviews - everyone who attends code review meeting learns, create a culture of continuous learning
  2. Source on community standards?  
  3. Two sets of standards - i.e. community cookbooks, might not be for cookbooks that you write internally
  4. Make sure to treat Chef code as actual code, not as scripts
  5. Have example cookbooks, a gold standard you can look/reflect on
6. Success story - how do you get Enterprise to let control go and put back in hands of devs
  1. Core team within large company 
7. If you do not have Chef infrastructure, what is best way to deploy Chef infrastructure?  What is best way to deploy Chef code if you do not have Chef Server?
  1. Lots of ways to do this - what makes most sense for your environment, don't change entire world all at once, find smallest piece you can and expand on it, find path of least resistance
  2. Chef Delivery
8. Best practices for redesigning/hacking your way out of tech debt with homegrown cookbooks mess?
  1. Make sure that cookbooks describe a thing, test all of them