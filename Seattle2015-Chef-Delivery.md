What is Chef Delivery?
-Runs tests
-Visibility into code review
-Allows testing in union/rehearsal environments
-End product can be a variety of things: cookbooks, application packages, infrastructure environments

Is it for applications or just Chef code?
-it depends! Can be configured for either or both

Can it stand up infrastructure?
-You bet: provisioning, terraform, and shelling to knife to work with vrealize as examples

Tell me more about Union!
-generally, allows you to test both a project and its dependencies
-tests against a set of nodes which you can select via version pinning
-currently, Delivery provides one Union environment; in the future there will be dependency chains defining Union.

How can we be selective about what goes into Union?
-When something goes into Union, it's upstream dependencies are locked

How do we get visibility into Delivery?
-Bitchin' UI that shows progression thru Delivery steps

How do you add a new dev to the system?
-They add a feature branch and perform local testing
-To submit change, cmd line delivery tool submits change to Delivery
-Delivery will perform verification tests, and notifies team that change is awaiting review

What about Stash integration?
-We're working on it this year

What's Github integration look like?
-to integrate w/ Delivery you create pull request; Delivery robot updates you on status of change moving thru delivery