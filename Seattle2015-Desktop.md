# Desktop / Workstation Management

Facilitated by DJ echohack

For hack day: https://github.com/echohack/chef_desktop

Workstation management with Chef is an area that needs to be improved.  Lots of organizations recognizing they've got a handle on their server infrastructure but are needing help wrangling workstations.

What tools people use?

* Boxen - puppet under the hood - for macbooks
* Chef Pantry - jtimberman
* ChefDK_Bootstrap Cookbook - Nordstrom (installs atom, vagrant, and virtualbox): https://supermarket.chef.io/cookbooks/chefdk_bootstrap
* Winbox (Chef Windows Dev Workstation setup) 
* BoxStarter http://boxstarter.org
* A Mac OS X Chef bootstrap (https://gist.github.com/fnichol/1100372) & workstation cookbook (https://github.com/ut-cookbooks/ut_base & https://github.com/ut-cookbooks/ut_workstation) - fnichol
* Battleschool https://github.com/spencergibb/battleschool
* Kitchenplan https://github.com/kitchenplan/kitchenplan

Example that bootstraps the software listed at https://gist.github.com/mwrock/8278331

http://boxstarter.org/package/url?https://gist.githubusercontent.com/mwrock/8278331/raw/e491685abaeb3f7326af5306fd2f07da1bcd7c51/Boxstarter

Facebook managing chef: contact info: mikedodge04@fb.com (Mike Dodge), pcox@fb.com (Pat Cox)

## Scoping attempt:

Lets say you are IT at an org - and you want to manage desktops.
Or you are developer and want to manage your Chef development workstation.

Need help understanding to integrate Chef into the enterprise IT organization's existing 'blessed' path for managed desktops/applications.

New to chef user: when you come in as a developer you are faced with a lot of tools to install and setup.  If you lose that workstation getting it all set backup again can take a long time.  Goal: Setup your dev station in less than 10 minutes, not 10 hours.

At one organization: Two camps of devs were found 
* give me the image that lets me get up and running now
*  a dev should be able to setup their own dev space.

At .net shop w/ devs on macs - they provide vagrant box w/ chef role already setup.  so a combo of boxen for mac - and then everybody has their own spot for customized area.  The windows environment is very prescribed and people get what is officially supported - this works well.

Q: Is that a locked down or open approach? 
A: Everybody is an admin on their own box

Devs with very custom and tricky setup.

Q: Anybody using Chef to setup dev workstation?
A: Nordstrom's Chef Bootstrap - seems to work well - acts as single chef solo run.

dotnet dev:  setting up new dev workstation - can have multiple reboots and updates - and keeps going and going - so wrote a tool to help ease the pain of that - looking for a chef tool similiar.

Potential HackDay Topic: Review the current solutions out there - see what are good ideas & bad ideas - and then try to come up with an awesome tool around chef to do that 

Q: How would this work? Like where would the binary software stored?
A: Usually stored as resource on the web.  Like chef base would use the package mangament system, like cholcolaty on windows, will go out and grab it from a known/trusted location (if you've done the dance to trust the sources).  If you have a custom thing for your org you'll have to setup the hosting location and point your receipe at that location yourself.

Typically packages come from three places : web, internal articfact factory, or local storage (usb drive)

## bootstrapping to get to that point - how do you get there?

Q; How do you get boxen doing it's first run?
A: Boxen has a curl command that you pull down and it sets up (your thing)  -- a curl/bash bootstrap script

Nordstrom has a bash script that takes 20 minutes to get a chef developer workstation setup.  You can wrap the script and override parts, such as pointing at public or private supermarket.

boxstar.org/wackpackage  -windows only example: give it URL to a raw gist, it installs chocolately.

Bootstrapper - one line in console - just gets it done.  In Windows you don't have curl -- so use powershell.

People are using chef and boxstarter at home to keep their home systems sane (got those crazy kids downloading all the crazy stuff - handy to be able to reinstall quickly).

A: Anybody in room that was IT helpdesk?

Facebook - has 14K managed mac, along with some windows and linux desktop.  They are using Chef internally to manage those workstations by encouraging the mac users to adopt the chef appraoch.
(Mike Dodge).  The provisioning is dealt with separately, but for configuration management it is all Chef.
contact info: mikedodge04@fb.com (Mike Dodge), pcox@fb.com (Pat Cox)

Q: Using chef directly or something like boxen?
A: Yes - using chef directly

Individual engineers at facebook don't have to write chef code - they might if they want super custom stuff - for most normal stuff they work with IT to manage that.  

Q: Can they turn it off?
A: Probably, but likely not because they'd have ot turn off network access. They are using the chef server logging to ensure clients are checking in and use that to work with the users to debug why their workstation isn't checking in.

Q: Compliance discussion -- how to get client to run against different chef servers (one for compliance) - a control/audit seperation.
A: For compliance run - if you can control how chef get sstarted, you can pass options to override the config it looks at.

If you dealing with Windows - where is Chef providing pain or gaps?

Compliance - sometimes doesn't make sense because it is being driving by rules not related to making your IT life easy. Creating situations where IT support do not have visibility into how applications get deployed into some environment.  In heavily regulated industries it is very easy for people to say "no".

Make the cost of meetings visible.

For those in these heavily regulated areas:
* Audit ability is really strong - ablity to do this remotely saves time & money
* Possibly can diagnosed and fixed remotely

Important to separate out the different problems that meets the regulations - build a CI that meets the needs of the regulations, perhaps have a manager in compliance be the official button pusher for causing code to go from dev to prod.

External auditors are coming in without any knowledge of DevOps making it difficult to explain why you are compliant with the processes and workflows.

A group where the Devs are using Chef but the Ops are not - using audit may help the Devs get more consistent platform from Ops.

Q: Are you doing DevOps Days - lunch-n-learn?
A: (nope)
* Show them "Compliance at Velocity" and make them scream for "GIVE ME MORE CHEF!"
* Show them peers at other locations, such as Jim Bob's Bank, that are using Chef
* Not a technical challange - social and business challange - understand the layers and politics within your organization

# Links to cool stuff!  Resources around Desktop Management (not just chef stuff) - we'll use these resources at hack day

Example that boostraps the software listed at https://gist.github.com/mwrock/8278331

http://boxstarter.org/package/url?https://gist.githubusercontent.com/mwrock/8278331/raw/e491685abaeb3f7326af5306fd2f07da1bcd7c51/Boxstarter

