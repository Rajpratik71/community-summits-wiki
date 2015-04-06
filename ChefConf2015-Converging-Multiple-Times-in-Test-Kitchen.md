Converging multiple times in Test Kitchen

Some use cases:
    Restarting a Windows machine - you need to run chef-client multiple times
    Modeling deployment strategies
    Converging Chef multiple times and ensuring the second converge does not update any resources
    Running audit-mode and validating an existing infrastructure isn't going to break

Can write a custom TK driver to handle some of these scenarios (especially unique ones, like Windows machines restarting or running chef-client multiple times)

TK can be ran with a cmd-line arg specifying a .kitchen.yml - If you use the same machine and test names you can setup a multiple-phase test as multiple .kitchen.yml files

Output from TK kind of sucks for CI - you need to grep stdout for some status message
  A Chef handler could send output from chef directly to TK
  Or it could output a specifically formatted file
  A new plugin type which supported targeted output checking (check TK output vs check convergence output)
    This isn't necessarily a verifier (which sends tests to a machine and tests them) but it does perform verification
    The output isn't necessarily going to be from Chef - you could use a puppet driver for convergence

There are no docs for writing drivers/provisioners/verifiers
  Adding yarddoc to the API would help - seperate public and private API methods
  Existing drivers all look different, there isn't one example to extend or follow
  A `how to write a driver` example
  Setup an MVP driver, provisioner, verifier
  update the driver generator - it is seriously out of date
    This should give a valid spec_helper.rb or some examples that show what you need to mock to test your driver/provisioner/verifier
    A good MVP could also illustrate this

Add a maintainers strategy - for all the obvious reasons

Publish office hours and make them public - good time for public to ask questions and push their PRs/Issues to the top of the stack

Test Kitchen is awesome!

https://github.com/mwrock/kitchen-nodes
https://github.com/GoatOS/goatos

View original notes in [etherpad](https://e.chef.io/p/testkitchen)