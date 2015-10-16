In Leschi Room.

There is now an initiative inside of Chef called 'ease of use' to help reduce the pain of using chef.  This team really wants more details from the community of where there is pain.

Problems:

* a lot of hidden assumptions about Ruby knowledge (threefour types of hashes)
 * different command line utilities (8 or so) 
* casual users, using chef now and then, are being lost because of how quickly the system is evolving.

Catalog of tools w/o having to look at chef spec.

Request: want an atlas
    wants an atlas/glossary of terms.

The Atlas needs to address the “where do I start?” for a new user.

There is now a catalog within Chef (company) for what they consider a product and what they don’t consider a product.  This will be shared out.  Help people understand if a tool or library is maintained, by whom, and such. 

Chris D wrote a blog post on replacing a shell script with an apply file, was beneficial to some new-user documentation

Chef training is being overhauled. All training material is online and public on github _as power point files_

Chef docs are now versioned - but still lots of landmines for people not aware of the changes in versions in chef.

it would be nice if recently added features had a callout as to what version they were introduced (sensitive parameter in template)
foodcritic takes a --chef-version option to show compatibility with older versions of chef-client (who knew?)

If you don’t give a chef version flag it will default to some hardwired version that may not be the latest version - and most likely not the version included with chefdk.

Some of the test metric problems are being solved in the secret labs of Chef.  

Omnibus is the project that Chef started to help manage ruby versions (squirreled away in a nice self contained area in /opt).

Chefdk is for somebody who doesn’t want to build ruby or worry about ruby to use Chef.

Fletcher wrote chef-dk-updater, lamontG turned that into app-bundle-updater, call for bringing that into chefDK to help with out of cycle gem updates (consuming later version of kitchen than is included, for example). There should be a tool like:
    chef gem update testkitchen 

# cookbook guidelines

What are the current recommended patterns for cookbooks?  Following that is currently a nightmare.

How do you get new users into writing chef cookbooks in a way they do not burn out in complexity?
 
Don't jump into complexity too quickly, cause you'll drown. Stop talking about Best Practices or introducing complex universal cookbooks and instead talk about solutions to problems.
Prolific cookbook writers vary about how much they talk about their workflow. Jamie is the best at that.  Also, some people object to the phrase Best Practices.


Chef leaders would do well to publish their workflows. 
Perhaps focus on “good practices” instead of “best practices"

_Best practices work well for things that are simple.  As they become complicated you need good practices.  When they are complex you need a good flexible team familiar with good and best practices._

TIL:  you don’t need to define your versions/dependancies in both berkshelf and the metadata file. *really?*  (yeah, the metadata keyword in Berksfile tells berks to look into metadata.rb for dependencies, you'd only redeclare them in Berksfile if you wanted to specify alternate sources (git locations, filesystem locations) for individual cookbooks)

Question about yaml support where json is used,  there is an RFC and 2 years ago a patch was written that was approved and might be merged in recently (pending funding). Some folks love yaml for readability, others note that new users have more trouble editing yaml than json.

YAML is very difficult for new users. This is why core will stay with JSON.

Just to get testing to work you need to know: Ruby, YAML, JSON, Chef, and …  
Consistency of languages/tools across the ecosystem would be great. Kitchen needs  yaml to run, all roles/databags being tested have to be in json.

Joe talked about internal tooling around git commit check that does pre-flight checks on syntax

# enterprise pain points around proxies/locked down corporate networks
Proxies, almost all tools support consistent configuration of proxies, busser under kitchen does it differently. 


"when are you guys moving hosted chef?" "already did, you didn't notice, we're that good"

On the chef side they’ve been decoupling components of chef allowing them to things like break apart the HA stuff.  There is a giant epic track in the Chef roadmap.  Chef requests people using Hosted Chef to be filing support tickets.

How do you check the health of a Hosted (Private?) Chef?  This is currently an issue.   Secret labs of Chef is working on this right now.  There is a bunch of commercial pressure on OpsCode to get this resolved in a good way soon.

corporate locked down environment hard to get to external package repos. Joe will write a blog post about his mod_rewrite/yum global conf mirror proxy in a "no internet access/no compiler" setup.
Noah has a new/better way of dealing with replaceable backends that he hopes will gain greater community cookbook adoption.

Documentation is sometimes ‘straight out wrong’ and the examples do not work.  

Chef looking into setting up a pipeline to "test the docs”.  There are alot of smoke and mirrors that help generate the docs that can cause multiple pages to have very similiar (or the same) content.

*The docs are on GitHub -  use the issue tracker when you see problems* 

Perhaps add 'up' or 'down' vote to the docs - issue is how do the doc maintainers know why the doc is 'down'.

Docs team getting better feedback from learn.chef than from docs.chef because of the user feedback mechanism available on learn.chef.  Perhaps consider trying to integrate a similiar system into docs.chef.
