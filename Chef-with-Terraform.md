# Chef with Terraform

A large number of the group uses Terraform.
Love Terraform, but it has many limitations because it's a DSL (Domain Specific Language), and not a real programming langauge. Need an understanding of the innards of Terraform to manipulate loops and conditionals properly.
Terraform doesn't easily create infrastructure that talks to each other -- nodes that are aware of each other -- out of the box. Needs to hand off to a provisioning tool such as Chef. That handoff to Chef is often painful, complicated, and requires a Chef Server.

Some people don't like using multiple tools. Would it be nice to be able to write infrastructure just in Chef? But it's often overkill, Terraform is simpler. There is a big learning curve to writing infrastructure within Chef.

Wish you could version infrastructure like Chef. -- Is there a need for a Chef-like tool for infrastructure? Like Terraform but wish it could be a language such as Ruby.

Chef provisioning is a hard sell because it goes beyond just configuration management. So now you're not just using Cloud Foundation to do your work anymore, you're using Chef to be your swiss army knife. Chef is great for configuration management, but over complicated for infrastructure provisioning.

Terraform and Chef only each solve half of the problem, and you have to use 2 tools to solve the problem. However, many prefer using the right tool for the job over a swiss-army knife approach, even if that means using another tool.

Do your engineers need to learn Terraform? No- around the room. Most prefer to keep infrastructure related code out of the hands of application engineers. DevOps/SRE's responsible for infrastructure. Some in the room use a CI tool such as Jenkins or templatize infrastructure (Terraform) using Chef.

An outstanding issue is that orphan nodes are common within Chef. It doesn't usually know when a node gets deleted. Cleanup can be hard. Someone wrote a listener that listens for deletion events and then removes the node(s) from the Chef server.

Taking on the effort to make a ruby-language infrastructure tool would be a huge challenge, especially with as fast as the cloud infrastructures progress. There would need to be significant community support to develop and maintain such a tool. e.g.: In Terraform there are 60-some providers, AWS has over 90 resources, and Azure over 70. Both not even natively supporting all resources available. May be unreasonable to assume creating a new infrastructure tool would make sense unless it drastically solved a different problem by enabling easier communication between nodes and prep-scripts following provisioning.