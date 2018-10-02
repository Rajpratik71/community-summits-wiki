SPonsor: Jon from Starbucks

"How can I have an InSpec Workflow that lets me work both locally and have the same code work in a Compliance environment?"

Heath has a Packer-Docker setup, does not use profiles, just runs `inspec exec *_spec.rb`

Three ways are common:
 * `inspec exec -t ssh://some-host`
 * from compliance
 * from test kitchen

"When I run locally, I manually change values - in this case it is the URL a webserver"