Zac Stevens "so... workflow".
- It wasn't mentioned during the product demos this morning. What's happening with it?
- We currently use Jenkins
- The real blocker in Delivery is Test Kitchen. Parallel execution is what we need. Can you do that in Delivery?
- tomrg: the short answer is no, Delivery doesn’t do that

Q. Can we install runners unattended?
A. Probably? I don’t remember. Effectively a runner install is 90% installing the ChefDK, 10% registration with the Automate server. So I'm sure it could be automated.

Q. Julian asks, are you using Blue Ocean Jenkins or Jenkinsfile?
A. (Zac) yes - declarative Jenkinsfile

Q. Can I remove Delivery since I don't use it?
A. Not in 1.x, but Automate 2.0 is going to be more modular so we'll be able to sell you mix-and-matched pieces tailored to use cases.

Q. I need some audit logging -- does Automate have that?
A. (Some discussion ensued about requirements for different types of logging and how we think about the problem at Chef.)

Documentation - zts
— Workflow section / Automate section in docs - the docs are functional but don’t really help you

Someone else asked a question about performance issues in Chef Server. He has a few thousand nodes converging every hour or half hour and system load on a c3.4xl is like 5.0 or above.

A. (Jon Cowie) --

* You may need to tune internal settings particularly PostgreSQL buffer pool
* If you have a lot of cookbook versions, you should use knife-tidy to clean things up to give a perf boost
* Policyfile to do precompile / pre-resolution can also help -- this way you don't need the depsolver workers on the server
* You can also watch for the next Chef Server release that’ll give you an external _stats API to monitor statistics and give you hints on what to tune.
* More info: https://docs.chef.io/server_tuning.html

Q. How is Chef Server different than Chef Automate?
A. Chef Server and Chef Automate are different components — you can regard Automate as a consumer of data from Chef Server / it’s the commercial uplift to Chef Server. There’s no backup/restore needed.