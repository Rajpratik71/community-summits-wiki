# Chef Workstation & Test Kitchen

We combined these because Test Kitchen falls under the scope of the Workstation team. Workstation is an extension of ChefDK that also contains an ad-hoc tool and a tray application that will handle auto-updates.

Workstation is supported on RHEL, Ubuntu (and similar linux systems), MacOS and Windows.

The primary problem workstation is solving is that ChefDK needs to have an expanded charter to handle all workstation tasks users want to solve. ChefDK is a grab bag of tools without good direction for starting users. For example, the many tools in the ChefDK do not all recognize certificates installed on a system in the same way (if at all). Workstation is intended to be more opinionated about how to solve specific problems with Chef. It aims to make getting started with Chef easier.

ChefDK equally weighted the problem of 'getting started as a Chef user' and 'getting started as a Chef contributor'. Workstation will put much more priority on the Chef user over the Chef contributor. 

# Potential next steps

1. The tools in the ChefDK do not feel like they came from the same company. We want to fix this and make them more homogenous.
    1. Make the integration between the tools more seamless. EG, should not need to log into Automate from multiple different tools.
1. The ad-hoc use case (`chef-run`).
1. Tech debt in the ChefDK.
    1. Reducing complexity and tool spread in the ChefDK.

# Pain points

1. In Test Kitchen, getting started on a Windows workstation. It requires a bunch of manual steps to get it working.
1. Tech debt. We have some old tools that are hard to fix or extend (EG, Foodcritic) that we need to decide what we do. Fix the tech debt? Make something new? Remove the functionality?
1. Administrator control over developer workstations. EG, developer should not have push or admin controls while administrators should. Workstation should facilitate this. Maybe a workstation config bundle or installer that is unique to the permissions of the user who is logged into automate who is downloading it.
1. I need to know what all the tools inside the ChefDK are doing before I can use them effectively.