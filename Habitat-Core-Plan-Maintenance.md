 * Ian kicks off the conversation
 * Thom: prior Debian maintainer, easy for things to become stale because people disappear despite best intentions. Everything should have N+1 maintainers, it should be easy for people to become a maintainer, and it should be easy for people to stop being a maintainer
 * Adam J: the one standard we should set is: "the plan should install and run the service in a bare-minimum way." Need to do something else? Write your own plan in your own origin that depends on the core plan. That pattern should be easy.
 * Thom: The contract is "I will provide binaries on disk that do the right work."
 * Adam J: one notch further: "if it's an executable, it should successfully run in a bare minimum configuration."
 * Adam L: "Do we have docs on that pattern?" Ian: "No, it could be better."
 * Paul M: We need to properly document the expectation of what a core plan is.
 * Thom recently added more 
 * Nathen: "Should all core plans have a README? Do any core plans have a README?" Ian: "Some do." Definitely an area in which we can be better.
 * We shall call them "configuration plans" - there was a fun conversation on naming things, which like death and taxes, continues to be a staple of life.
 * Is this a pattern that we should adopt in Chef? Bare-minimum cookbooks that install the bin and accept a proper config?... and that's it?
 * The packages that use "debconf" are known to have a poor experience. Reiterates the thought that packages / cookbooks that provide the bare minimum working installation are a better experience.
 * Hack Day: document the "your core package, my config" pattern
 * Lots of great conversation of what the "source cookbook" (sc) might look like, how to prototype it... can we distill the installation/running of services to a single resource that takes package name, maybe a version, the config files and contents to write out... Might be a great Hack Day project.
