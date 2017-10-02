-- I shell out to curl, and then try to parse that versus regex, because the HTTP call doesn't work on remote machines. 

- I'm sorry, it should work on local and remote. 2 resources with this issue SSL/HTTP. We don't alter the state of the machine to run InSpec. The way to fix this is to wrap curl, it hasn't been fixed besides time. We should fix this during hack day.

-- How about windows...

- Let's start here, we'll make it optimal for 2.0. If host has no curl, make the end user responsible to installing curl. We want the UX to be the same for local and remote. Platform RFC will be able to flag a resource for platform support. We skip resource for lack of OS support.

- Let's push a remote http 1.0, make sure it works. What we need to expose: status code, headers as a hash and the content. We can expand to HTTPS, with disabled SSL cert.

ADAM LEFF HAS VOLUNTEERED TO FIX HTTP RESOURCE DURING HACK DAY.

-- A ChefDK generator to spit out resource/profiles would be nice and easier. The documentation for a custom resource for a cookbook is not good. We need better docs, for example yml file for InSpec, I was confused what the minimal amount of info needed.

- The resolve check for the InSpec plugin is "is there a inspec.yml file". The yml triggers all the checks for libraries, controls..syntax..etc.

-- The debug error handling goes into RSpec currently. Huge pain, but we don't have the time to fix this.

(Adam Leff is refactoring the CLI formatter and the JSON formatter, to allow expect syntax.)

- Conversion guide? for example: should_be(compliance auditors) == expect(Integration testers) syntax. 

-- I like serverspec format in the docs, remove all the matchers crap in the resource page. 

HANNAH WILL TAKE THIS ON IN DOCS FOR HACK DAY

-- We need better kitchen-inspec docs, both in both places.


