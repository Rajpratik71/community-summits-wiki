# Contributing to open source

Topics:

+ Balancing OS contribution when working for $company
+ Advice/guidance to start contributing

## Balancing

Nick - Balancing don't want to give away game changing stuff, due to competitive advantage.  What's the balance?  What to keep secret and balance?

Techies want to talk about it, but business.

Made something better?  Contribute back so don't have to maintain separate fork.  Company doesn't have to keep everything open source, can pick and choose.  Take it to other powers?

Nordstrom got permission to contribute cookbooks and chef stuff.  Legal may need to be involved.

Questions exist about why a company would do this?  Eco system argument, there are books.

Another benefit - recruiting tool. Strong folks might require to be able to contribute and present.

Jennifer - Open sourcing helps reduce technical debt.  When people share, more folks contribute and help make stuff better.

Folks have been fired for open sourcing something - get permission and think throught the license choice.  GPL needed to be confirmed.

Other side to technical debt, commit to support in some sense.  Coding in the open, the government can't accept the licenses.  You do need to understand the licenses.  Everyone's corporate licenses are afraid of GPL licenses.  Black Duck is code to scan repo's. Don't just open it up, have a license.


Doug - recommend Apache 2 License for Nordstrom stuff.  Brand protections that MIT and BSD don't offer.

## Getting Started

### Resources

+ Openhatch - project to match users with problems to be fixed
+ [Mozilla](https://developer.mozilla.org/en-US/docs/Introduction) - nice
  contributor, expert to tell you what you can contribute to
+ Chef projects - labelled Easy  Can add tests.
+ [Your First PR](https://twitter.com/yourfirstpr): Twitter account "showcasing
  great starter issues on GitHub."
+ [Digital Ocean's Hacktoberfest](https://hacktoberfest.digitalocean.com/): get
  a nice t-shirt when you submit 4 PRs to open source projects at GitHub in the
  month of October. They have a list of "featured projects" seeking help.
+ [Contributor Covenent](http://contributor-covenant.org/) - a project
  encouraging community codes of conduct. There is a list of projects there that
  have adopted the covenant to pledge to be welcoming communities.
+ (pending: resources with guidance for writing super-useful bug reports and
  pull requests, "what to expect when you're contributing")

### Types of Contributions

#### Informational/Support

+ as a user of any experience with a project, providing quality problem reports
  when things don't go as expected
+ as a user of almost any skill-level, spending time in a project's
  communications channel(s)—e.g. IRC, mailing lists—and providing help to other
  users having problems you may know how to solve (or at least help troubleshoot
  to improve the quality of a problem report)
+ as a user of moderate+ skill, improving the quality of the documentation
+ get to know a project's community and culture before becoming too invested,
  some are welcoming and some are emotionally brutal

#### Bug Fixes or New Features to Existing projects

+ as a someone new to the project/ecosystem/language, submitting fixes for
  issues the project has identified as easy for new folks
+ as skill and knowledge of a project's workings and roadmap increases,
  submitting fixes for gnarlier bugs or adding new capabilities
+ **WARNING**: know your employer's policy on open source code contributions.
  If you're submitting bug fixes on company time, does the company own the
  copywrite? Forgiveness later can get hairy.

#### Open Sourcing a Code Base of Your Own

Put your code out there! You solved a problem other people might be having, too.
Recommend you do so knowing some of the experiences of others when they have
started projects. This is especially true for companies.

Are you signing up to support something for life?
+ The ideal would be to find a successor when the time comes that you do not
  want to provide support for a project.
+ A community sprouting up out the project can help spread support effort, but
  can also be the _source_ of support requests. If a project takes off, it can
  take up a lot of your time. You should _care_ about this problem you are
  solving.
+ Be aware of guilt. It feels bad when you are faced with issues you don't have
  time to do anything about.
+ Not _super_ awesome to just dump code.  You can read it, but having support
  and a community is better. Checking something compiles and generally works is
  sort of a minimum.

Some examples of projects where support/succession got fuzzy:
+ chef-vault: Came out of Nordstrom and was added as part of the Chef DK
  toolset. The community supports it, but who makes decisions about roadmap?
  Responsibility feeling is real.
+ Berkshelf - Came out of Riot Games, is a part of the core Chef toolset. Folks
  left Riot. Who sets berks roadmap now?

Some basics if you opt to create a public code repository:
+ [Read up on open source licensing](https://tldrlegal.com/verified) and put a
  license on your code.
+ Manage expectations of others who discover your project in a README or
  CONTRIBUTING document. Will you be supporting it or is this YOLO YMMV code? Do
  you have a vision for the future that could go into the README or a ROADMAP
  doc? Will you decline—thankfully!—pull requests that conflict with the vision?
+ In GitHub, turn off pull requests for your repo if you won't take them and
  say that in the README.

## Contributor License Agreements

Why they exist?  CLA a layer on top of license, giving extra permissions.  Like the right to distribute without attribution.  Chef does not do copywrite assignment.  Some CLAs give up  the copywrite.  Patents can be a really big deal. Research and talk to lawyers.  Check your employee handbook.

Actions
+ Add references to legal advice around licensing.
+ Add links to the contributing
+ New to open source, advice for how to start