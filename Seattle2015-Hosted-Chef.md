Session 10/15/2015 at Chef Summit

Hosted Chef migrated from Rackspace to AWS one week ago
We are using the new external PostgreSQL feature of Chef Server to run the back end on RDS

Q: We've been wondering if we're crazy to run business critical stuff on Hosted Chef
A: Up until last week...maybe.  But our confidence and yours should increase dramatically now that we are on AWS.

History of Hosted...
In ye olden times of Opscode, Chef as a SaaS was the monetization play, thus the birth of Hosted Chef
Over time a lot of "special sauce" was whipped up to make it work, which meant Hosted drifted from our core code base (not functionally but operationally)
Hosted Chef is now "a really big Chef Server" that runs in AWS, using the same code base that our customers run on prem

Q: Any chance you might look at Aurora?
A: No, because Chef relies on some PostgreSQL specific features and Aurora does not support it

Q: Multi-tenancy, how does that work on Hosted?
A: Same as on-prem in terms of org management

Q: Any chance of not using PostgreSQL with Chef Server?
A: Nope, because of our dependency on some of the platform-specific features

Q: How many orgs can you support on Hosted?
A: Orgs are basically unlimited

Fun facts!
There are about 15 FE servers in Hosted today across three AZs in AWS
In total we support around 200k active nodes with Hosted Chef (active means used in the last 30 days)
Environment lives in US East

Over the next year Chef will be open sourcing all of the code we use to stand up and manage Hosted Chef
Q: Is that anything like the Chef reference architecture cookbook?
A: Not exactly...  The reference architecture lays out all the components that are used in Chef's internal CI infrastructure: Chef Server, Analytics, Supermarket and all the little bits and pieces.  Specifically out of scope is HA support because this is not part of the business need in our CI scenario.  More info here if desired: https://e.chef.io/p/chef-reference

Q: What's the security model for Hosted?  How do you prevent getting hacked?
A: We take security very seriously.  Your data bags are safe with us...we recommend using encrypted data bags for anything secret (see Chef Vault).  Over the next year Chef will be working through SOC 2 for Hosted.  

Q: Do you do any data de-duplication?
A: No, not across organizations.  This is built in Chef functionality within an org.

Q: Do you do any data sharding?
A: Nope.  We had a thing like that in the distant past and life was unpleasant.

Q: Are you working on supplying AMIs for Chef Server?
A: They exist today...enjoy yourself!

Q: Does the AMI have a time bomb?
A: No, all good for up to 25 nodes.  You only pay for the AWS resources.

Q: Is there a free Hosted offering?
A: Yes, up to 5 nodes.

Q: Is there an AMI for Windows?
A: Chef Server only runs on some distributions of Linux.  Client has Windows support (and lots of other "exotic" platforms).

Q: Can you run Chef Server on Amazon Linux?
A: Danger Will Robinson!  Not advised.  Amazon Linux is "weird".  Amazon Linux is a "tier 2" supported platform for Chef Client.

Q: How do we get started if we want to check out Hosted?
A: Go to manage.chef.io and register.

Q: How's the documentation?
A: Same workflow and tools as Chef Server -- no special docs for Chef Hosted.  Very few steps are excluded from Hosted (such as org creation).

Q: If I was on the fence between going the AMI route and going with Hosted, what could help me make that decision?
A: We might be biased...start with Hosted.  

Q: Safe harbor ruling -- any impacts on Hosted?
A: No, we don't anticipate any impact there, but we will keep up to date on this.

Q: Any longer term plans you can share about Hosted?
A: Just catching our breath after the migration.  Want to make sure that is rock solid and successful, and that our patterns for Hosted follow our customers' on-prem patterns.  It was a 6-month initiative to rearchitect and migrate to AWS.  We have a lot of enhancements in the backlog and now we get to start planning those?

Q: Are you happy with AWS?
A: Totally happy.

Q: Is there a guide about ports etc. to use Hosted?
A: We do have a list of IP addresses -- let us handle RR DNS, LB, etc.  We will give you more details if you need it but we start by keeping things simple.

Q: Do you have an operational status page?
A: Yes, it is at status.chef.io

Q: How do you present Hosted as an option / tell the story / convince management?
A: It's not for everyone.  If you have large infrastructure, strigent security concerns, etc., it's more appropriate to run on-prem.  That's fine with us.  We want to support the range of customer needs and we don't advocate one over the other.  A good use case is for customers who are doing cloud migration across the board and want to bring Chef along with them.

Q: Is storage constrained/capped in Hosted?
A: Not at this time.  Please be reasonable and nice.

Q: What telemetry exists that shows what is going on in Hosted?
A: Today it's Chef Reporting -- next year we hope to bring Chef Analytics to hosted.  Analytics supports taking data to Splunk.  There is also a plug-in for Chef/Splunk in OSS land.