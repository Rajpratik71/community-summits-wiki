# Exotic Environments & OS's

Kick off by Matt Ray - Partner Integration.

Looking for where the bad things are and good things are.  Platform Porting.

Partner Integration - makes things happen on weird platforms.

heavily uses omnibus - this allows for building of the tools (ruby apps like chef) on weird platforms or platforms with elderly (old) versions of packages that won't work well with Chef.

Omnibus supports all sorts of weird things (AIX or RHEL 4).

How do you build an Omnibus package?

Minimum viable build environment to get Omnibus to up and going is *gcc* and *git*.

*OmniBus toolchain* - given a gcc it can build the series of bits needed for OmniBus.

In the current ecosystem - if you write tools in non-ruby languages - it is a pain.  How could we make that better?

For example: right now you have to parse ruby to understand what is in metadata.rb.

Is there anybody else building non-ruby tools that are working with Chef?

Yes - this would be why a focus on using JSON as the inter-change language between tools.  Possible RFC topic.

Topic: Chef talking to things not Chef.

How do you get all the right build package on each system?

The Chef Secret Labs is looking to release some magic sauce.  Secret sauce: *Angry Chef* and *Angry Omnibus* - Angry things build the normal happy things.

OmniBus build essentials is to be depricated in favor of Omnibus Toolchain.

How does this help me?

Brings you closer to the warm hugs of teir 2 support.

PowerPC and Arm Debian chef client support.

Is there a test platform for T1 or T2?  No - not yet.

ChefCo is wanting to expand what is included in the CI for chef builds to allow the community maintainers easier access to build status.  Goal: Make the ChefCo CI pipeline accessable to external maintainers.

TODO: Need to document what is needed to be done by a community member or external hardware hoster to tie into that CI infrastructure.

Goal: Upgrade from 'here is an RPM' to 'here is an image for this particular cloud platform'.

Consider: Allow Supermarket to allow sharing of these type of things (bento boxes, omnibus builds) -- warning - danger zone of lessons learned - do this carefully and cleanly (namespaced).

Old versions of Windows are now considered 'exotic' like RHEL 4 is now - however now 32bit windows and other older things without recent PowerShell are ... not in a healthy chef support state.

What is coming down the pipeline?

* The Power builds currently stalled out by IBM responsivness, bugs, and limited capacity at Chef (man power limitations).
* Cisco ports - nxos (chef on certain cisco switches)  and a TBD project (super secret!)

To get started - if you have ruby 2 and a working git you should be able to check out omnibus-chef, bundle it, and then build it
... LOTS OF INTEREST IN GETTING THIS PROCESS BETTER DOCUMENTED ...

Bonus point for build on limited system: If you are disk and ram constrained you will want to allocate the disk towards RAM and NFS mount the disk.

Example challange: Chef on a WRT54G you could possibly use proxy layer with chef client running elsewhere.

SSH isn't everywhere - look into transport and the options that are available there - could really help the Internet of Things topic.

Order of things:
    
    * omnibus-chef # if it works Yay you are done enjoy your chef.. if not keep going down
    * omnibus-software #
    * omnibus 
    * ohai # likely needed if you are needing a new omnibus you'll need a custom ohai
    * chef # gotten down here? You on cisco?  You'll likely will need patches to bring your new package format

PR's accepted - but if you are in T2 you won't be inside of the CI

# Internet of Things

Chef provisioning was first stab at doing chef on other boxes that may not be running chef.

There is some more Chef Secret Labs *stuff is coming* that could help with this.. to be annouced yet... not yet opensourced

ohai proxy - to be announced



