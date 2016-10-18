* How to upgrade from DRDB to HA
  * Support ticket?

* Knife-backup seems to format the node data wrong

* Setup a new Chef server:
  * re bootstrap each node one by one to the new chef server
    * very time consuming
    * if node.set is ever used then the node data on the server and the node data for the new boostrapped node is different

* Complete back and rebuild
  * Build a new chef server
  * File backup + db backup
  * Restore to new server
    * cutover DNS
    * Need details on how to do this process

* Mixed client versions in your environment (11 and 12)
  * aggressive pinning of versions with environment cookbook model
    * CI systems to test new cookbooks that come in

* omnibus_updater
* Pulls from public site, which isn't an option
* windows upgrades don't work after 12.5+
  * windows service removal in upgrade process

* Upgrade RFC

* How do you upgrade if you have multiple "customers" on your server
  * Do you split out orgs as part of the upgrade? Is it an opportune time
