-- Learn chef start is great, but there's no real world examples.

- Onboarding new people...is hard. People won't do the modules in learn Chef.

-- I have to learn Ruby, no experience in Ruby. Show me a way to bring them all together, let me do something end to end. End-to-end like capstone.

- The modules have type-o's and misconfiguration. Overall quality, type-o's.

-- Need an atlas to ecosystem, -relationship of components.

- how to think of Chef's role conceptually.

-- Hashicorp doc style is awesome.

- Take down anything that is before Chef 12 please.

-- Show me patterns and how they relate to each other. Why would I use this pattern vs why wouldn't I use this pattern?

- First piece of info I'm looking for...what is Chef? Chef server? Chef Solo?

-- Canonical Chef - knife-solo/knife-zero

- Debugging a failed chef client run...how to?

-- How do I download a cookbook? Give us deprecations warning, and telling people how to do this (use berkshelf)- would be nice.

- One of the hardest thing to bootstrap...is the Chef server, would be great to just get a button to get a bash/python script that it spits out and you can bootstrap.

-- Dynamically generated run lists vs roles...the highlevel choose your own adventure style patterns would be nice..

- We have 3 different entry points in the CLI (knife, Chef, berkshelf)...why don't we just put everything in Chef, to make it easier for everyone. It would clear up so much confusion. I would love berks to go away..

-- Why don't we just delete the chef tool as it does so little.

- I did a phone screen with a bunch of 2-5yr experience Chef folks and they couldn't describe the difference between compile vs converge. We probably need more conceptual docs.

-- The docs are lacking real world use case. It shows you how-to but why you would want to do this is missing.

- We need to be clear on what data passes through the handler... there's not a lot of context.

-- Is there any basic Ruby that helps us get started? Especially, for folks who have no prior Ruby experience. We need to teach just enough idioms (make sure they are not helpful or dangerous).

- Recipe in templates..where did this come from..keeping track of that in your boilerplate is challenging.

-- How do we solve doing too much in one cookbook..The correct level is default.

- How to create a wrapper cookbook..needs documentation. 

-- We should probably tell people about knife.rb vs config.rb.