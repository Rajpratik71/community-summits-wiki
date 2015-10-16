# testing ohai plugins

# Can we get information without shellout?
* interfaces are not consistent across platforms
* what is the overhead of shellout, could mixlib-shellout keep a shell open?
* shellout on Windows is particularly heavy

# Should ohai data get saved early in a Chef run?
* runs used to save early, but caused problems with partial node objects on failed runs
* could we have a node.save that took a whitelist or just ohai data?

# deploying custom ohai plugins
* chef delivers the ohai plugin which means we don't get the output of the plugin in the first run, do it in bootstrap?
* how you decide which plugins get pushed to what nodes on bootstrap?
* could we have an early ohai run, somehow determine what custom plugins need to be loaded and then load those plugins before rest of the run
* is there a way to have plugins run based on the node run list?

# cross-node ohai queries.
* when deploying nodes in parallel, how do you make decisions based on another nodes  data that hasn't been saved yet?
* this is more of an orchestration problem

# ohai plugins as a chef server object alongside cookbooks, first class artifact
* supermarket differentiating between bare plugins and plugins in cookbooks
* cookbooks coule depend on a plugin if it was a first class object
* could slow down the converge having another trip to the server
* could have a ohai plugin run after cookbook sync but before cookbooks run
* cookbook metadata specifying required attributes.

# virtualization platform plugin is broken on some platforms
* Windows.  xen, virtualbox, vsphere (wade)
* FreeBSD?
* listing guests that are running on a host