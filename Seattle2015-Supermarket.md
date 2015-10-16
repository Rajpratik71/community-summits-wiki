All Things Supermarket

If you already run private chef server, why would someone run private supermarket?
- Because of paranoia, limited external access to resources 
- might not have permission to run chef server
- many internal organizations
- one internal supermarket to share cookbooks across internal organizations
- better interface for browsing for solutions

Mirroring supermarket cookbooks
+ not a feature of supermarket today, current option is minimart
+ vetting cookbooks in the public supermarket? - See the COOKBOOKS! session in Medina after lunch!
+ want a mirroring mechanism to bring in "approved" cookbooks from Supermarket? Yes, depending on "approved."
+ some folks showed interest in caching/proxy feature in private supermarket to designated upstream universes

Namespacing Desires:
+ Idea: cookbooks live under a user/org namespace, maybe award some cookcooks to "approved"
+ Copy the DNS model - look in your local domain before recursing to find a thing
+ (source priority: order of sources in Berkshelf matters)
+ quality metrics may alleviate the problems attempted with namespacing
+ some need namespacing to be able to fork cookbooks that aren't getting fixed; wants a namespace to have a dedicated universe

Abandoned/Orphaned Cookbooks
+ lack a formal policy on dealing with abandoned cookbooks
+ renewal process to re-commit to maintaining a cookbook

CI Automation User
+ Need a user that owns cookbooks that are produced by a CI pipeline
+ Current solution, a user in Chef Server that is used by the CI pipeline for publishing new versions

Issues with Choosing Private Supermarket
+ authentication
+ mirroring from anything that has a universe

How do I remove a cookbook or specific version(s) of a cookbook?
+ might need a whole session around this
+ issues are open to deal with this
+ credential data spills - yank no matter how implemented is not sufficient for your safety; your creds are out there, change them
+ version yanking, where artifact at that version is no longer resolvable, but supermarket "reserves" that version to prevent re-upload: you MUST increment to upload a new version
+ maybe implement yanking with a feature flag at first

Publishing Cookbooks:
+ knife cookbook share
+ stove:
  + treats supermarket as pure artifact server, e.g. does not include tests - makes it difficult to evaluate quality

Action Items:
+ RFC on community adoption of abandoned cookbooks
+ Supermarket linkage on the Chef downloads site