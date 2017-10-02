-- We have policies to check wifi, optional packages. We only manage laptops that are in the Chef team.

- Is everyone using Macs in production? for build/test?

-- For IOS product builds, it's good to use OSX. 

- The OS10 cookbook wasn't really maintained. We're excited to revamp MacOS support at Chef. 

-- Getting Mac OS as a core resource in Chef would be good. We should have that. We have (sous chef mac OS cookbook) user defaults, doc preferences, and finder. The apple reccommended way is to leverage the API...but apple doesn't document that API in a consumable a way. :(

- One of the principles of the Chef is that it would do the expected action. 

-- But the question is are writing a default provider or preferences provider?

- Let's be opinionated.  The reason why we use default over anything is because it's been the most stable.

-- The default handling for dictionaries is horrendous. I should be able to use the API that loads the dictionary and I use what I need. I wouldn't want to write a defaults provider, I would want to write a preferences provider that leverages the API. A preference is not a key:value pair. I want the resource to look like a "systems preferences".

- There are a lot of keys that you wouldn't know for Apple - how would you know about this?

-- Apple wants you to go straight NPM.

- Chef has a concept of a resource that has multiple providers. The default provider would use Apple's preference API.

-- A personal goal I have, a Chef run when it runs, all these CLI kickoffs creates so much noise for security team. If we could provide a binding to the API, so this can't be handled quietly - that would be nice!

- Is everyone using the launch_d resource? What do you think?

-- A coworker got an OSX_profile PR in there. Would you find prefs helpful?

- So what about Windows?

-- A lot of the work we're trying to do is that everything as coverage in windows/linux/mac

- Windows has a registry key. 

-- There's some resources that are cross-platform that have OS specific properties, I like that better than having OS specific properties.

- Service command on OSX is different than Windows, on Windows it's just a service.

-- What are you all thinking for OS10?

- I value DEB because I could just provide them a mac. Be able to ship a unit from apple store without having to intervene and do anything to it.

-- What management platform using?

- We'll use MDM OSS or write our own. We need to make sure our devs have the same tools, environment set up.

-- How long lived are those devices that you are using to managed with Chef? If the use reboots the machine, it will clear/remove the configuration set in recovery mode. VMware puts the version ID in the bundle ID, so everything version has a seperate bundle. Apple wants the management of it outside of the OS.

- I know hosted Chef does certs? does it certs?

-- the Chef Client validates certs like SSL by default.

- The custom resource DSL is what you should be doing.
 