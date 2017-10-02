11:30AM, Stowell

A similar session a few years ago didn't seem to go anywhere. There was some talk of the F5 cookbook, but it's sat idle for quite some time. Curiosity about whether the desired workflow would be similar to that one (an api-call from a management node), or different workflows.

Note from Tim: there's a new cookbook, and F5 is collaborating. New chef-vault workflow. 

Distinction between things that cannot run the agent easily (e.g. an F5), vs machines that should be managable via supported platforms, but for which there are not resources available for easy management.

Example of the latter from Facebook: Part of open source network infrastructure project that can be maintained by chef. Achievable because the platform is linux based, and sidestepped the issue of platform support that might be present in other types of setups.

On SaaS platforms that wouldn't be able to run the agent, resources can make outbound calls. Concern is over whether that breaks the intended model since now a management node is what's actually making the calls, so there's a disconnect between where chef's running and the item being managed. Also means it's more difficult to represent devices as their own objects, or maintain history if, for example, a management node is replaced by a new server.

Talk of whether there would be value in a proxy node configuration, where a logical node can be defined, and take advantage of some of the node-internals (e.g. assigning environments to logical nodes managed by a tools box or similar). There's been some talk in the past of implementing similar, but there's a larger conversation over whether it breaks the chef model when you go down that route. 

Regardless of implementation, what gains are there from having managed devices distinct entities?

Automate visiblity -- while you can reference devices' "node objects" of sorts in a subhash of their management node, you lose some of the granularity of insights that automate brings.

Does the inability of running chef on some network gear affect selection? Do you avoid buying certain gear based on that? 

Legacy issues -- not all organizations will have the ability to replace, how does chef manage things in environments where there may be large deployments of incompatible devices (e.g. Cisco IOS devices). Generally these devices are still manually managed. 

How are new issues identified validated? If a particular configuration is found to contain an esoteric vulnerability, how easily can an environments' configurations be audited?

Last mile issues can stifle automation consistency. If I can manage my servers effectively with chef, but a subset of services or functions lag behind, does that create bottlenecks for implementing the systems that *can* be easily automated.

"Rancid is not configuration management for switches" :-D

Parallels brought up to GUI-based workflows in windows. Shortcomings of existing tools there and in networking is that there's not a focus on approvals, promotion or change validations. 

How are validation processes automated?

ex: changes documented in change management, requestor and implementor typically different, combination of eyes and monitoring validates. Things tend to be bundled into change windows, and can increase troubleshooting burden.

Handling silos in large organizations:
"siloing happens", but regular review of practices allows teams to determine where separation of privileges has caused a problem or blockage, and determine whether a broader group should have access to more easily adapt to similar issues in future.

Contrast to public sector work -- lots of meetings, control boards, processes. Increased a sense of stability, but in practice just enforced a lack of change and evolution. 

Conversation around culture and speed. Is the slower pace encountered in areas like government inherently bad, or just the appropriate culture for that space? 

Broken processes vs. over-optimizing slow processes.
Ex: Cisco environment with 10 switches. Change frequency was slow, without much effort required, at which point automation doesn't add much to the equation. Could have made the process faster, but given how infrequently changes needed to be applied, and that the environment ended up being replaced, automation efforts would have been likely to add more development time than the gains they provide.

Long lifespan of network devices adds to the difficulty of solving. Lots of ancient IOS and similar devices in the wild, and even if modern networking gear is more easily automatible, large swaths of users won't be able to benefit. Counterpoint, if time is spent on those types of devices, is it at the cost of supporting better future patterns. Rancid + Chef is far from perfect, but might suffice as more organizations move to modernized networking stacks.

ex.: when dealing with a cli-driven network config, does chef just provide the wrong kind of abstraction? Less of a conceptual hurdle going from raw ios to rancid, than if you need to learn a new workflow to wrap around that with templating, and potentially doesn't fit in the traditional idempotent/convergent chef model. 

catch 22: if vendors have newer platforms that more easily support automation, even if larger groups of users have older platforms in production, there's not incentive for them to patch older systems instead of upselling on newer systems. 

How frequently do network configs change, and what types of changes? What would an ideal way to manage look like?
Often daily, things like Firewall rules are most frequent. 

What is the universal abstraction between devices? Is there a way to not have to care about cisco, f5, juniper, et al?

If instead of a straight DSL, if there was raw config, inventory and templating, would that be enough for the 80% case?

