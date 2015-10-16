# Cookbooks

## Attendees

* Robb Kidd
* Chris Webber

Responders - Noah, Tim, Sean, Mark A, other folks got stomped.

## Discussion

Build cookbook in delivery land.  There are different types of cookbooks.  Cookbooks don't need recipes for instance.  When do we build names for the types of cookbooks.
The names are made up by the different companies, this forum may also be a good place for creating names. Individual companies define things in different ways.  Metadata may be a good place to classify, cookbook names may work.

Code is usage case, not code pattern.  Defined by how stuff is used.  Cookbook team - hoping to come up with examples, blog, no common opinion.  Training and teaching chef is using different names.  
Opposite opinion - prescriptive is not really the goal.  Jess would like to have names, make it easier to talk at about these.  
Noah - naming the pattern isn't good idea, give examples of the problems and solution patterns will work.  The problems seem to be very common and consistent.  Quality community cookbooks are needed.
Chef doesn't document solutions to problems.  Might be a good idea.  

Is mysql cookbook - may be a good example.  Could we open source all of the chef code.    

Community cookbooks vs open source cookbooks.  Different animals.  Chef is an open source company, but can't support everything.  We forget that there are people using the code and causing problems for them.  Need an example company with cookbooks.  Community cookbooks are example of how to write cookbooks, not to be read, just used.  How do things get used in the wild.

When we have concrete things we can talk about naming patterns.  

Community cookbooks - hard to justify supporting on multiple platforms.  Hard to abstract out the details.  

Development of cookbooks?
    Start beautiful,
    Changes, add functions
    Turn off,
    Software natural state is a hairball.
    Re-usablity is sort of important.

    Open source vs community cookbooks - example of something that might work.    

    Use an abstraction model to boost productivity.  Chef and ops world needs to get there.    

    Jess - Why can't we build small cookbooks that act like software, composable, api and usable.  The existing cookbooks could be written as reusable.
    Need doc on writing a highly reusable cookbook.

How are other communities doing sharing and good code.    Gang of 4 book (?) has patterns for development.

Things need to work in a simple fashion.  Progress from simple to complex.  Ruby has examples of how to build from simple to complex.  Metrics tools, Rubocop and Foodcritic.  Could rate cookbooks by complexity.  

Cookbook quality metrics - hard to identify if cookbook is quality or not an RFC exists.  How to add bio hazard to some cookbooks. Looking for ideas of what is quality.  chef-cookbooks.org to contribute suggestions.  Keeps on changing, makes it hard for enterprises.  Ready for quality measurements.  Some orgs need prescriptive patterns. Lego movie?  Blah, Blah,   not sure of the point.

Multiple patterns are nice.

Brandon - Very handy in the beginning, very useful to have something telling you what to do.  
Doug - Expect a level of quality from community CB and from app team developing stuff.

Quality metrics - should show what to improve.

## Supermarket cookbook guidelines

Not discussed - move to tomorrow??

   Name
   Maintainer
   Email
   Open source license
   Test coverage



Action item
  Clinton - volunteered to write a sample company set of cookbooks.
  Chef - contribute quality items
