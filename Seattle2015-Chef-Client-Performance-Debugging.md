Chef Client Performance Debugging - proposed by Mike Fiedler from DataDog

Wednesday Oct 14th 1:30pm in Kirkland room

Thanks Lamont G and Dan D for being in the room :thumbsup:

What's happening in a chef-client during the compile phase when it looks paused or generates no output?
- often these things:
- searches
- node object lookup
- loading data bags

chef-client --profile ruby
(coming in 12.6)

Make flame graphs of resources in the client run?  Yes - that'd be cool be doesn't exist


https://github.com/chef/chef-rfc/blob/master/rfc051-telemetry.md
https://github.com/chef/chef/pull/3818

Remote directory resource fixed (faster) in 12.5.1

chef-client --profile-ruby is post 12.5.1. Uses rubyprof. Deep Ruby profiling. Call graph.

Can you turn RubyProf output into flame graphs?

Ruby profiling during compile phase is needed

Also per-resource profiling during converge phase is needed

Why is Ruby memory using ballooning? This is because you aren't using targeted searches, or partial search.

Idea: Show top 5 slowest searches, resources, memory usage at the end of Chef run

Read Jon Cowie's book ( http://shop.oreilly.com/product/0636920032984.do ) for ways to add hooks to your Chef Client runs and get data about client resources.

Chef Resource Reporter is just our implementation of a handler that batches up stats and sends them to analytics, reporting etc. https://github.com/chef/chef/blob/master/lib/chef/resource_reporter.rb