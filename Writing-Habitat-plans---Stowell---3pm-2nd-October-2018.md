# Plans
.ps1 and .sh
Might have Lifecycle hooks e.g.
- health - think about curl a webpage
- init 
- config directory may have files, handlebars {{ }} 

## Plan definition file - plan.sh and plan.ps1
  Metadata: Naming, License, maintainer etc.
  Build phases officially "callbacks" 
  
**Action:** Check those phases are in the correct order in the docs:
**Action:** Document when to use do_prepare vs do_build, do_before and do_after

Discussion:
  * do_before can be used for things like dynamic build versioning
  * Use underscore as a function name prefix and it's probably just locally scoped rather than official phases
  * Can we have a plan.ps1 and plan.sh (multi-package) - maybe in the future
  * Why hab - is this is Yet Another Package Format? Hab packages can all be installed side by side
  * Hab vs Chocolatey - there are similarities (user namespace, etc.) - Chocolatey is more vendor driven (runs scripts afterwards but not known build phases etc.)
  * Hab packages use pre-built packages as dependencies 
  * Handing things to the ops team, Hab provides a point of 