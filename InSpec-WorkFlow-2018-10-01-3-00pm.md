SPonsor: Jon from Starbucks

"How can I have an InSpec Workflow that lets me work both locally and have the same code work in a Compliance environment?"

Heath has a Packer-Docker setup, does not use profiles, just runs `inspec exec *_spec.rb`

Three ways are common:
 * `inspec exec -t ssh://some-host`
 * from compliance
 * from test kitchen

"When I run locally, I manually change values - in this case it is the URL a webserver."

Desire is to verify that an nginx webserver is running (both locally working) and that the network path is open through the firewall.

Galen: Consider testing the firewall rules.
Clinton: Use inspec attributes to 
Jerry: If you want the same profile to test both locally and remote: you could use an http resource (which will run on the remote machine) and you could use a local Ruby call (like net/http's GET) to execute a request from the local (inspec workstation) machine
Galen: An issue with that is that under Compliance, it's just the audit coobook running, so "remote machine" == "inspec workstation" - you won't have that external check.  You might consider having a separate run in which the smoke testing is performed.
Jon: I think I need to look into attributes with `inspec exec`. We just used audit-cookbook because we needed access to the chef server node data.

Where should tests live?
Do tests live in the cookbook?  Yes, the ones that are for the cookbook.
What about the smoke tests or functional user tests?  That should probably be another set of profiles, or maybe not even InSpec.

Other topics:

Feature request for A2: in delivery review for a cookbook, it would be great to easily link to a download of the latest.





