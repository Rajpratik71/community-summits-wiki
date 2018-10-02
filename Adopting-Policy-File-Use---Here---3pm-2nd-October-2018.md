Policy files

Anthony 
  Policy files were not ready.  Want to switch an use them now.  What happens to an organization when you migrate.


Tyler
  Chef workstation - generate policy file like artifact.  SHA, versions, have some idea of what exactly your are running. Dependencies all figured out.  Run list in artifact, and allow overrides. Not the same as policy files but close.

Lamont
  Replace berksfile locks for testing. Replaces environments and roles.  Policy groups for differences. Can use policy file like a role.  Push the policy files to the server.
Differences from roles  - more manageable.  Cookbooks are shared between policy file using nodes and non PF nodes.

Advantages
  Fewer abstractions, no dependency solver on nodes, know what you are running, no unpinned dependencies.

Slow adoption, Why?
  Released 3 years ago, selling delivery but didn’t support policy files. Need to change the way chef is taught.  Why use berkshelf? Use policy files instead.

Include policies and hoisting should make things better.  See if this might work for unix base.  Might need to loop over all policies, regenerate and push.

Chef workstation - hard to tell what generates policy files and workstation policies.  Working on refactoring chef to have”chef” be the command that is used for everything.  Eliminate some of the overlaps.  chef push, vs knife upload, vs berks upload, simplify things.