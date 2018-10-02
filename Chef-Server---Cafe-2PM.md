Chef Server

Question: is Chef 12 HA worth the hassle.  Consider DR vs HA, if you can’t tolerate small outages maybe use HA.  If you have good backups DR might be a better way to recover.  User pointed out HA has caused more apparent outages than it seems to have fixed. Usual causes are slow I/O and slow network.  ETCD is particular about good response.

Plans - Informal, no schedule general guidelines.  Trying to do away with SOLR and RabbitQ. Postgresql 10 is the works.  Some discussion of postgresql features, including postgres logical replication.  Chef Server should come out in a habitat package eventually.  Common authorization between chef server, chef manage, chef client are still somewhat difficult.

Chef Manage

Don’t want it on anything internet faced.  Not interested in a lot of new features.  Want to push the features to automate 2.

Cust - happy with moving to A2. Glorified reporting + manage features would be good.  
How to users use chef manage?   CLI and use manage to see what’s really there.  Rare to touch node data.

Good things on automate - figure out why things stopped converging, visualize reasons.  Good if A2 was real reporter on nodes.
A2 - server and info collecter and use inspec.

Customer - moving inspec controls to central place.  What Chef to manage that, A2 maybe.  Want to be able to manage nodes from A2, easy to pull information
use it for asset management.  Want to be able to test the fully converged environment.  Test built server with a control. Get inspec out of the cookbooks. Make chef server install like the A2 install.

Policy files now have inherited policies. Good stuff.

Working on IP V6 clean up.  V4 loopback gets turned off by default on RHEL.  Causes all sorts of problems.

User login.  How do you assign stuff in chef server to users that login to Automate?