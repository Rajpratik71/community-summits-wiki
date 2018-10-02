# Chef Workstation

We combined these because Test Kitchen falls under the scope of the Workstation team. Workstation is an extension of ChefDK that also contains an ad-hoc tool and a tray application that will handle auto-updates.

Workstation is supported on RHEL, Ubuntu (and similar linux systems), MacOS and Windows.

The primary problem workstation is solving is that ChefDK needs to have an expanded charter to handle all workstation tasks users want to solve. ChefDK is a grab bag of tools without good direction for starting users. For example, the many tools in the ChefDK do not all recognize certificates installed on a system in the same way (if at all). Workstation is intended to be more opinionated about how to solve specific problems with Chef. It aims to make getting started with Chef easier.

ChefDK equally weighted the problem of 'getting started as a Chef user' and 'getting started as a Chef contributor'. Workstation will put much more priority on the Chef user over the Chef contributor. 

## Pain points

1. In Test Kitchen, getting started on a Windows workstation. It requires a bunch of manual steps to get it working.
1. Tech debt. We have some old tools that are hard to fix or extend (EG, Foodcritic) that we need to decide what we do. Fix the tech debt? Make something new? Remove the functionality?
1. Administrator control over developer workstations. EG, developer should not have push or admin controls while administrators should. Workstation should facilitate this. Maybe a workstation config bundle or installer that is unique to the permissions of the user who is logged into automate who is downloading it.
1. I need to know what all the tools inside the ChefDK are doing before I can use them effectively.
1. It would be nice to be able to specify a version of the linter to lock a cookbook to. It sucks to run the linter on my workstation and have everything pass, then push a commit and see it fail in CI because it has a different version of rubocop installed.
1. I want the latest DK all the time (note: this is the goal of the update notification in Chef Workstation).
1. We don't update until it's out for at least 30 days (Regardless what software it is). I want to be able to specify when to update based on how long the software has been out.

## Potential next steps

1. The tools in the ChefDK do not feel like they came from the same company. We want to fix this and make them more homogenous.
    1. Make the integration between the tools more seamless. EG, should not need to log into Automate from multiple different tools.
1. The ad-hoc use case (`chef-run`).
1. Tech debt in the ChefDK.
    1. Reducing complexity and tool spread in the ChefDK.

## Notes

* The version of Chef Client included in the ChefDK *usually* doesn't affect the version that is managed on your fleet. You should typically always be on the latest version of ChefDK even if your fleet is running an older version of Chef than what is included in the ChefDK.

# Test Kitchen

Request for more resources contributed towards this - TK is a very valuable tool. We have talked for years about releasing the next major version but it is not visible what it is happening.

The Workstation team is responsible for Test Kitchen now, but we do not have great news on this front. It needs more resources. The community sees that many existing tools are not getting resources put towards them but they need it. They are still being used.

We have a lot of community tech debt. Fostering a community takes commitment from the maintainers (Chef Software) that hasn't been there in a while. Fostering community takes time away from developing features or fixing bugs, but it is important for future velocity.

# Contributing

Question: should Chef Workstation help more potential developers or more Chef users?
Answer: Contributing to Chef products should be like contributing to other Ruby projects. We don't need a special developer toolkit. That said - contributing is hard. It takes experience with the code base, or good documentation (that can fall out of date). This is a problem every project struggles with, and we struggle especially hard. We would like to make it easier to get developers spun up.