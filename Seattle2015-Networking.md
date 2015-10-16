Carl and John proposed session

Carl is trying to get feedback from the community

John wants to talk about vendor-neutral support to abstract interface configuration in chef.

Big issues: silo, culture in networking

Carl is to blame for Openstack Neutron

Carl is working on adding chef support to a large networking company's switches. The company starts with C and ends with isco.

Running chef on a switch requires configuring the switch which is the whole point of putting chef on the switch.

It might be time to start pushing for a shift in how we thin kabout networking. VLANs and L2 are dead, long live VLANs. IPv6 is easier, because automating serial consoles is hard.

Brian wants malleable infrastructure -- he wants his switch dynamically configurable. Carl wants to know his use case.

Lowest-common denominator doesn't work great for most use cases.

Brian's solution is to double-encapsulate. 9000 customers, Q in Q takes him a long way, but not everything.

Brian is using Cisco and Juniper primarily (mostly Cisco), both Catalyst and Nexus. Uses a template file to bootstrap -- Brian wants TFTPboot.

In Carl's experience, getting any automation on older gear is really F***ing hard. Brian is fine with abandoning older gear.

Brian has vswitch, openvswitch, custom protocol, vlan, vxlan, magic. He wants infrastructure code to say what is in the rack, but the switch needs to be configured for what areas it controls.

Brian wants to tell the switch it is part of dev, and it should know what to do with that. 

Matt wants to know if there are any tools people like: Answer: Chef!

Jason provides some rpms as part of the template, which puts the code he needs into the initial boot process.

Two use cases from $OTHER_PERSON: Uses Nexus switches at top of rack, up to 10G switches. Uses TFTP for provisioning. Needs to change single port VLAN, wants to remove human factor from typing commands to the switch. 2nd case: Nagios monitoring network, wants to know parents in the network. Switch knows MACs, hypervisor knows MAC. Everyone said LLDP -- Ohai plugin for LLDP -- install LLDP agent and turn it on for switches.

Brian has sent SNMP to device to manage it. Only Brian speaks SNMP at his place (ouch!). He wants something better than SNMP to tell a device what it is.

John is trying to put everything in Atlas.

DevOps and NetOps sometime conflict -- In NetOps dude -> switch -> rancid -> source, in DevOps dude -> source -> deployment magic -> prod

Phil's network guys really wanted automation from day one, until they made their own switches. Once you have > 1000 switches that they need to change things.

Infra as Code conflicts with Network guys in $OTHER_PERSONs company.

Carl says awesomeness is inversely proportional to CCIE coolaid.

Carl: DevOps group hug with Networking guys will help an awful lot

95% of the time is spent on boring issues, automating will swap this to 5%!

Brian wants help breaking the automation is terrifying. Carl suggests building a virtual lab to show how things maybe won't break to build comfort. Phil wants to know if the problem is outages or hugging servers. Outages are easy to argue about, but hugging servers is much harder. Brian is the architect for Devops, other guy is Network architect. Brian wants them to work together well. Brian argues that his last 3000 changes haven't broken anything, but the last 9 changes to the network have broken things. But Management doesn't really care.

John wants to add that network engineers are burned by black box automation that breaks things, which encourages a cultural perception against automation.

Carl wants you to know it gets better if you use legacy network gear. Getting off your 6500 Catalysts is a good idea.

Carl wants to talk about Networking in the Cloud where you don't even know what a VLAN is.

$GUY_WITH_HAT uses AWS and AWS cloud formation, but also uses Chef. He wants to know where to draw the line in terms of networking. JJ wants to know OpsWorks or Chef. $GUY_WITH_HAT is using Chef. Carl's followup is VPC or EC2? They are migrating to VPC, but aren't there yet. At Automaticon HW released new version of Sparkle Formation to make things not suck. Ask Chris (wearing the Heavy Water shirt) for more details.

Carl wants to know $GUY_WITH_HATs specific network problems: Security, but mostly keeping things from being put together by hand. Others suggest Terraform over Cloud Formation because it is much less fragile than Cloud Formation. Carl says there is also some info with the analytics toolkit that can help -- you can build tests based on some ohai attributes -- what ports are running, what security groups the machine is in, etc. Carl reminds us he is not trying to sell analytics. You don't need to pay for audit mode.

Another call for not talking about hardware -- no one really responds. John asks if anyone is using anything specifically for security automation. Carl is using CM to bring in IDS things and tests that don't break things with Metasploit -- dump everything into logstash and figure it all out later. Carl thinks there is a lot of tooling for security, but it is hard to use -- it is completely different terminology, some vendor specific, and requires a lot of work just to run ping. Jason mentions that security tools also have performance penalties to discuss.

Carl wants to know if anyone is from 1998 -- because they haven't heard of ipv6 yet.

ARIN finally ran out of IP addresses, for real this time. Mostly.

5 people have deployed ipv6 in any capacity.

Carl thinks ipv6 will make a big change because the internet of the 80s and 90s is back. EVERYTHING is public and crazy protocols abound. NAT firewalls don't really work for v6, because everyone gets a real ip, and you have to do firewalling. He likens it to a firewall in your car -- the internet is ALWAYS on fire, and you need to poke holes to let legitimate things through. NO MORE NAT firewalls. In Carl's opinion that brings hardware closer to cloud, because cloud doesn't worry about VLANs or ACLs or other magic. We're back to just IP. Carl wants to get to that model for everything, and not just cloud.

Carl mentions we need new levels of management to handle firewalls, vpn endpoints, routes, etc. Group policies -- but not the giant networking company version. An abstraction of ACLs. All the devs get access to the dev environment , etc.

Network guys don't trust us because we do the network equivalent of chmod 777 -- allow everything everywhere.

Traditional developers are terrible at networking, but we're moving to an era where devs should start caring about networking. ACLs are a complex thing. Cloud Security Groups are basically just group policies with less terror.

Where does an IDS live now? Carl suggests monitoring and security are still super important -- you still need to make sure your policies are enforced. He suggests putting these things at the choke points -- the router that connects you to the internet, for exmaple. Inside your network? Switches have gotten better -- you can run that stuff on certain switches now. It's scary, but possible.  Distributed port mirroring, s-flow sampling, etc.

The challenge and opportunity around that is terrifying for enterprises, because they have no idea where is what -- we need manageable units. We need to solve differing permissions with the same logical end points -- what if Bob and Mary share a tablet, but need different permissions? This is a discoverability problem.

Don't tie Identity to IP addresses. VPNs, however, do exactly this. More intelligent proxies that have a better idea of what a person is helps break this tie, because there is more to an identity than an IP. This makes a management problem of how to manage these identities. Alex Perry from Google gave a fantastic presentation on how they manage these a few years ago. They added a richer language to express the needs of their network and what they let on.

Carl has a problem with how everyone is enforcing this with a VPN. Basically everything has AES acceleration now, which makes VPN less painful, but we need to divorce from 2 old security isues: devs are on the dev network. NO! You're a developer, your access should be controlled by kerberos certs, sso, mfa, etc. everything can talk to everything, and we need to move access control elsewhere, instead of relying on old-style vlans. This is much harder to deploy, but doable.

VLANs also help prevent DoS. How do yo ucontrol that without VLANs? You stil have network access control devices in place, which are basically routers. This still gives you the segregation because you can tell routers to drop traffic. Switches can handle traffic better than they could before. We have better things than the Catalyst 6500 nowadays.