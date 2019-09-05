# Multi-topic time slot to talk about all things Chef Client

1. Most likely after London summit, we'll fork Chef to work on breaking changes for Chef 15 
Potential items: 
- Look at a list of items to deprecate 
- 10 year long list of the things we can build 
- What resources do we build next? 

1. Would love feedback for Target mode (An RFC that's open a while back) 

1. What's taking so long for the Windows cookbooks? There are a lot of Windows resources. We went through a lot of them for Chef 14; Windows task took a long time. We wouldn't expect to see an Apache resource in core Chef right now, so maybe IIS doesn't make sense for now. What should be there are like AD

1. Is there a native Windows time zone resource? There is.
1. We want Chef to be very good at covering your operating system - it needs to be tested for most of the environments. 

1. Upgrading Chef client. The yearly releases have been great; it seems that some users are stuck on the older version; how do we move the community forward? 
* We are trying to minimize breaking changes for Chef 15 
* For me it's the community cookbooks; I don't want to go edit the cookbooks... 
* Check out sous-chefs 
* One of the huge problems we've had upgrading to Chef 13 from 12 is the huge list of breaking changes. 
* We are still in Chef 13; quite difficult finding change log (each commit) for the older versions; not a problem if you use Chef 14.
* There are now deprecation warnings
* Our manager is very unhappy about the time it takes for us to just do upgrades; (We can maybe try to back port deprecation notices to previous version(ie. 13)). Note: this is a leapfrog scenario (user currently on Chef 12).

* There are no intentional breaking changes going from (ie. 14.0 -> 14.5); if upgrading from 13 to 14, you do need to review what the breaking changes. 
* We are not suggesting users to use why-run anymore
* Ask: why isn't there an auto-correct for my cookbook? Very much, we'd want to do. This requires a lot of work. 
* Foodcritic has been carrying on a lot of tech-debt over the years; 
* Cookstyle is an opinionated Rubocop 

1. You can set the version of Chef that you test again with test-kitchen (current version + future version) 

1. We use Chef-solo a lot; regular Chef on bare-metal as well 

1. Chef target mode
* I don't have a specific use case; I just know we have a network engineering team to use Ansible for managing network devices 
* Don't want two tools to do one task 
