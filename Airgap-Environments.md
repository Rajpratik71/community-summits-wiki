Share pain points and success strategies

* How do you configure 100 or 10000 chef managed nodes to use an internal gem repository?

Q: If the Chef server could serve up the Chef-Client - would that be helpful in air gapped environments?
*** This is not currently supported by Chef Server ***
Chef nodes would get the chef client from the chef server it's checking into. Some people have used the `required cookbook` feature to use Chef as an artifact server beyond cookbooks. 

Chef client updater cookbook can update chef-client from a configured endpoint (i.e., patching server - yum). 

In some environments, most things are closed off but artifact repositories are able to communicate 

Q: What are the common things that blow up in Air gapped?
* Software/systems make expectations that other systems must exist in order to work. 
* some systems require you to log into systems to configure how things can access other systems.
* Artifact distribution
    * Rubygems
        * Keeping Rubygems in sync (too massive) full mirror is 500GB
        * Able to use Artifactory to cache gems on demand as they are requested by systems
        * Geminabox can work as a proxy caching server
            * Can avoid worrying about licensing
            * Rob Kidd is working on a habitat plan/package for this
        * Artificatory
            * Scales well
    * Common pattern to bringing in artifacts involves using a repository server that can cache artifacts from the internet, done in a lower environment. Then you jump these artifacts across the air gap through some mechanism to keep your higher level environments with the same artifacts. 
* Getting approval to use widely adopted tools
    * Getting Artifactory requires security, approval, procurement
* Worried about upgrading Chef 12 to 13

Some of these challenges lead people to packaging dependencies (i.e., gems) into their cookbooks. Not ideal.

Try to build packages that have all of their dependencies baked into them. 

Reminder: Last year we were having trouble with chef_gem, with the fix to modify the Gem.sources collection. This is still a good solution for that use case. Yay!

New Gem issue:
When gems are defined in `metadata.rb` the chef client tries to download and install any defined gems before chef actually runs on the node, which is when the CA Certs and necessary configuration is laid down 
* Introduced by RFC 60
* Needs to exist for loading gems prior to the `libraries` being loaded
* Can Chef-client be configured to trust specific servers at the beginning of the run?
* Maybe the Chef server can offer up the CA Cert chain for the environment?
* Can this be implemented in the bootstrap process?
    * This is implemented in ChefDK with knife tools. 
    * Not everyone uses bootstrap. 
* Workarounds would involve baking this CA Cert configuration into your images or kickstart scripts
* Omnibus sets the SSL_CA_FILE (or whatever it's called) environment variable so it's always pointing to the CA Roots packaged by Omnibus. 
* Another option - rebuild chef client omnibus client
    * Be warned - there be dragons. 

Q: Where is there opposition to using Omnibus?
* The learning curve is very steep, especially when teaching new devs to use it.
* When customers choose to repackage chef with omnibus it eliminates visibility into the build from Chef's perspective. Harder to support.
* Some vendors need to be walled off from where chef typically gets installed to, requiring the need to control that installation location and customizing omnibus. 
* Maybe we can find a better way to simplify the installation, exposing those configuration points? Can we make the experience better for the customers?
