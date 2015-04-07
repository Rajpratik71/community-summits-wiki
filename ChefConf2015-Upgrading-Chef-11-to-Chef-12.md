## Upgrade Chef 11 to 12 - Help!

Upgrading Server is easier than upgrading client

### Clients 

Major breaking change that causes issues -> SSL validated by default

Chef has a built in self signed cert. This cert is only generated and owned by the Chef server. If you use this, fairly simple to port to existing clients using knife ssh/knife winrm then use knife ssh fetch. Each node pulls down cert from Chef server. Goes in trusted certs dir. 
Chef 12 adds trusted_directory. Self signed certs should go in here.  All the tooling does this automagically if the cert is here.

^ This works well if this is your model.

Get in trouble if cert isn't self signed in a non-standalone situation. For example, if you use your own cert authority and the cert on the chef server is signed by the certificate authority. There is no easy way to get this cert, because you have to get this from a location that isn't the chef server.
Hack: use knife ssh/knife winrm to script putting the cert in the trusted_cert dir. However, this is a one once operation.

Another way: have a base cookbook that puts this in place.
In base cookbook/role: explicity turn off SSL (turned off SSL implicity in Chef 11, but Chef 12 turns this on). So turn this off explicity. Can use chef client cookbook for this. Two settings: ssl_verify and another one. Set to verify_none and false. Do this before upgrade so upgrade doesn't turn this on before the cert is in place.
Catch-22: can't turn on SSL until cert is in place for Chef 12.

Cert: if using self-signed cert, the server cert is your root cert. If using a CA, then need the cert from the CA authority.
Cryptology is hard. Do research, find an expert for help.

If cert is already on the nodes, then in a good situation.

Another option: enable on 11 first then upgrade - but this apparently doesn't work, because verifying the CA on Chef 11 is broken and has an issue that is fixed in 12.
There is a github issue explaining this and how to work around:  https://github.com/chef/chef/issues/1653 (possibly?)

Omnibus Updater: downloads chef client you want to upgrade to. So to work, it will fail the first chef run, then run the next run successfully with the new client. Had to do this to work.

Windows: harder to do. Supermarket omnibus updater windows is broken, don't use it. There is a fork that works.

Docs: there is an ssl cert location variable that can be set to look in another location. This might be useful for use on the first time.

Might be good to have a good recommended upgrate path.

Don't use 12.0, use 12.1, since 12.2 just came out.
+ If you are using the windows cookbook prepare for dependency hell. Need at least 1.36.0 for compat with Chef 12, recommend 1.36.6. 
  + There are changes in 12 around the windows package resource. Be aware of this and pay attention to any use of windows package.
    + Maybe. Core resources at some point got moved into Chef Core but not clear when.
      + There is a dance around using the windows cookbook and resources, as windows cookbook defines resources that move into core at some point and conflicts can arise when this happens.
      + Be sure you pin to an exact version of the windows cookbook.
      + As you upgrade, see what your usage of the windows cookbook is and evaluate if at some point you can remove it because enough resources are added in core Chef.

Chef gem - another big gotcha.
  + Downloads gem during compile phase of cookbook run. Doesn't do it lazily. Can cause lots of race conditions based on which gems get downloaded when. 
    + Might be nicer if this is done in context of the run.
      + Chef 12 has a feature to enable this by explicity setting an attribute.
      + Can test this out with test kitchen. Setting this solves a lot of race condition issues.

## Chef Server

Make sure you're on Open Source 11.1 or high or Enterprise 11.2 or higher before upgrading to Chef Server 12, or automated tools won't work.

Even better if you get to latest Chef 11 server, that way closest to 12 before jumping to 12.

Upgrade documention is on the docs site - it's really good if doing a stand alone upgrade. 

Note: add link to docs here.

Test out in a sandbox environment.

If using LDAP over AD, then make sure you are using 12.0.5 or higher that contain fixes for AD bug that locks out users if using LDAP to talk to AD.

Going from Chef 10 to Chef 12 is tricky (Not in place upgrades, have to bring up new Chef 12, export/import). Chef 11 / 12 clean up a lot of data integrity issues that existed in 10 that have to cleaned up before getting to 11/12.
Validations should be caught on upload, but can be painful, especially if have large data sets.

Chef 12 server opensources all of RBAC. If not using the Management console, have to use the ctl commands that are added. 
Appears to be a bug where you can't accept an invite from the Management console on the command line. (minor case to be aware of).

Chef 12 server uses chef_server.rb from private_chef.rb. If you used enterprise, chef_server.rb is a symlink to private_chef.rb.

The way you install plugins changes. Old way: use omnibus packages. Can now use the ctl command to install. This doesn't work if need to air gap things. Can do this with install command, but the syntax is weird, because you can only specify the directory it is in, so look it up. 
Upgrade documentation says to use the install command, but you can still use the old way of install .

## Notes:
### Background
Many Chef customers have asked us for advice in upgrading their Chef clients to 12. ...

### Deploying Chef Client 12SSL Verification Differences
Chef 11 and prior releases did not verify the validity of the SSL cert on the API service it communicated with (typically your internal Chef server or api.chef.io).  Back in October, 2014 we announced that that SSL Certificate Validation settings were going to change, although warnings have been there since Chef 11.12.0:

* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
SSL validation of HTTPS requests is disabled. HTTPS connections are still
encrypted, but chef is not able to detect forged replies or man in the middle
attacks.

To fix this issue add an entry like this to your configuration file:

```Ruby
  # Verify all HTTPS connections (recommended)
  ssl_verify_mode :verify_peer

  # OR, Verify only connections to chef-server
  verify_api_cert true
```

To check your SSL configuration, or troubleshoot errors, you can use the
`knife ssl check` command like so:

```
  knife ssl check -c /tmp/vagrant-chef-1/solo.rb
```

* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *

Many customers have discovered upon upgrading to Chef 12 that they receive the following error:
ERROR: SSL Validation failure connecting to host: chef-server.example.com ...
ERROR: OpenSSL::SSL::SSLError: SSL_connect returned=1 errno=0 state=SSLv3 ...

This SSL Validation error typically occurs because of these reasons:
The SSL Certificate of your Chef server is self-signed, or signed by a Certificate Authority that Chef isn’t configured to trust
The Common Name (CN) field of the SSL certificate does not match the hostname being connected to.
The Certificate has expired, or the date is outside of the validate ranges listed on the certificate

### Before the upgrade
Before migrating to Chef 12, it’s recommended to implement the following:
1. If you have a base role or base cookbook for your organization, update the chef-client cookbook dependency to 4.2.4 or higher in your metadata.rb.
  1. Automatically set verify_api_cert to false and ssl_verify_mode to :verify_none in your client.rb on all nodes. You can do this like so:

#### Ready Bake Code 
(somewhere in your organization’s base cookbook)
```Ruby
node.set[‘chef_client’][‘config’][‘verify_api_cert’] = false
node.set[‘chef_client’][‘config’][‘ssl_verify_mode’] = :verify_none
include_recipe 'chef-client::config'
include_recipe 'chef-client::service'
```

This ensures that you explicitly have set your organization’s current policy of how you plan to validate the certificate. This matches chef-client 11’s current behavior.
1. If you decide to increase security, you can later on set verify_api_cert to true and ssl_verify_mode to :verify_peer. If not, at least you have explicitly set these values and other cookbook dependencies will not break your converges by accidently or implicitly setting these attributes.
2. If you use the Windows cookbook and are using a version older than 1.36.0, you’ll want to update to 1.36.0 or greater in order to provide chef-client 12 compatibility.
3. Of particular note is the change to windows_package. Depending on your usage, your cookbooks may be able to remove windows cookbook dependencies after the chef-client 12 upgrade. You’ll want to review this documentation: https://docs.chef.io/resource_windows_package.html
4. Updating this cookbook can be problematic because it’s likely to touch and influence many of your internal cookbooks. You’ll want to set aside some extra time for testing downstream dependency updates.

Chef 12 users have several options of increasing security:
1. Update your client.rb verify_api_cert setting to false and ssl_verify_mode setting to :verify_none - NOTE:  although this does reduce the security of your Chef 12 client configuration, it maintains parity with Chef 11’s security. 
2. **Using self-signed certs**:   Ensure that your Chef server’s certificate CN name is correct and the certificate is not expired.  Use knife ssl fetch to store this certificate in all of your Chef client’s trust store.
3. **Using certificates signed by your internal CA**:  Place your CA certificate in the /etc/chef/trusted_certs directory on your nodes. On Windows you’ll want to place this in the C:\chef\trusted_certs directory.
4. **Using certificates signed by a public CA**:  These certificates should be trusted automatically by Chef clients, because Chef includes the Mozilla Root CA bundle by default.
If you decide to increase security by trusting a certificate using one of the above methods, you’ll want to make this certificate available for bootstrap operations. Newer versions of knife bootstrap will automatically copy the user’s .chef/trusted_certs directory to the node’s chef/trusted_certs directory. For self-signed certs, the user can simply do knife ssl fetch, for other methods you will have to manually acquire the CA certificate and place it in your ~/.chef/trusted_certs directory.

Instead of putting the CA certificate manually in the /etc/chef/trusted_certs or C:\Chef\trusted_certs directory on nodes, you can put this in your base cookbook and deploy it that way. I’m using an attribute here so I can drive different CA certs in different environments.

### Ready Bake Code
#### Linux: Validate and install CA certificate
```Ruby
directory '/etc/chef/trusted_certs' do
  recursive true
  action :create
end
cookbook_file node['example_base']['ca_cert'] do
  path "/etc/chef/trusted_certs/#{node['example_base']['ca_cert']}"
  action :create
end
```
     
#### Windows: Validate and install CA certificate
```Ruby
directory 'C:/chef/trusted_certs' do
recursive true
    action :create
end
cookbook_file node['vertafore_base']['ca_cert'] do
    path "C:/chef/trusted_certs/#{node['vertafore_base']['ca_cert']}"
    action :create
end
```

There’s an interesting problem here however, in that CHEF-4647 (https://tickets.opscode.com/browse/CHEF-4647) prevents Linux machines in particular from automatically placing the CA certificate on nodes running Chef 11. This issue is fixed in Chef 12 (https://github.com/chef/chef/issues/1653). In other words: You need Chef 12 client before you can roll out the CA certificate automatically using this method. Using the omnibus_updater method below of automatically updating chef-client won’t work either, since it restarts at the end of the run…

My fix here is to roll out chef-client 12 to all nodes with these settings:

### Ready Bake Code
```Ruby
node.set['chef_client']['config']['verify_api_cert'] = false # Set explicitly to true after Chef 12 upgrade
node.set['chef_client']['config']['ssl_verify_mode'] = ':verify_none' # set explicitly to :verify_peer after Chef 12 upgrade
```

Then after this is rolled out, then rollout the CA certificate and turn on the above settings.

### Methods for automatically upgrading the Chef client across your fleet
Linux
The omnibus-updater cookbook can automatically upgrade the Chef package (referred to as the Omnibus).  This may result in some complications if you run chef-client as a daemon because it’s tricky to restart the chef-client daemon during a chef-client run.   However this can be worked around with an ‘at’ job or manual restart of the chef-client daemon.

Your Chef package may also be upgraded using ‘knife ssh’ or  any pre-existing internal tooling.

It’s recommended to work this into your organization’s base cookbook or base role so you don’t have to apply it to every node’s run_list.

### Ready Bake Code
```Ruby
node.set['omnibus_updater']['restart_chef_service'] = true
node.set['omnibus_updater']['version'] = '12.1.1'
include_recipe 'omnibus_updater::default'
```

### Troubleshooting Common FailuresIncorrect verify_api_cert setting
If you have a number of nodes that were incorrectly updated to validate the api cert (in other words, the client.rb on the machine has verify_api_cert true set incorrectly), or if you have a number of nodes failing the intended ssl verify, then these nodes will be stuck in the started state.

There isn’t a drop down menu in Chef Manage to filter by the “started” status, but you can modify the http request to display them as so: 

https://chef.example.com/organizations/example/runs?endTime=1425588291&startTime=1425501891&status=started
Chef Server API Compatibility
The Chef Server API is a REST interface which is decoupled from Chef client development, and supports all currently supported versions of the Chef client (10, 11 and 12).  Our customers have experienced no issues mixing and matching 11 clients with 12 servers, and 12 clients with 11 servers.

## Cookbook Changes
(statement about how most cookbooks work just fine without modification)

### Testing Recommendations
(vagrant/test-kitchen)
If your cookbooks compile right in Vagrant/TK, they’ll be fine.  Don’t expect any behavior changes during runtime,  aside from the aforementioned SSL differences. 

In order to test upgrade and backwards compatibility scenarios you can add an attribute to your .kitchen.yml to force a particular version of chef-client to install.

### Ready Bake Code:
.kitchen.yml
```
---
driver:
  name: vagrant

provisioner:
  name: chef_zero
  require_chef_omnibus: 11.18.6
```

### Under-the-hood Chef changes that may affect your libraries
If you’re writing providers as libraries in Ruby (sometimes called HWRPs) that call Chef DSL resources, you need to add an  `include Chef::DSL::Recipe` if you see NoMethodError when calling them. 
Provider mapping changes:   you should now use the `provides :resource` method instead of doing Chef-11 style provider mappings


[Read original notes in etherpad](https://e.chef.io/p/UpgradingChef)