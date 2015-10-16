Chef High Availability (HA), Disaster Recovery (DR), and Chef Sync
Thursday, Oct. 15th at 11:00 am

Question:  how are people handling HA & DR with their Chef Servers?   what if you don't know postgres/rabbit/etc?

chef-sync:  a premium add-on to Chef server -  but not widely known or used
https://docs.chef.io/server_replication.html

Stephen Delano:  the DRBD-based HA mode is open source and free for use.   The AWS-HA mode is a premium feature,  there's a new AWS HA mode coming that uses AWS primitives to provide HA. Also reduces the number of backend services to 3:  Postgres (RDS), S3, and Solr (CloudSearch)

HA: Is it more than just checking a box? HA systems add massive complexity which tend to reduce availability, unless they're extremely well thought out (this is rare)

What do you need when your HA system fails? is it DR?

Why would you want to run one chef server/cluster in one DC, while your application runs active in multiple DCs? The typical argument is unified search.

### The pattern:
    * Policy data (cookbooks, etc) should be published via pipeline fan-out to multiple chef servers
    * Service discovery data (node data) should be localized per failure domain
    * This works if your applications are designed to run active in multiple data centers
    
## Monitoring

Use Splunk/LogStash, etc. to monitor logs
The Chef Server runbook: https://docs.chef.io/runbook.html

Hosted Chef:   you don't have control over availability,  many prefer to use on-prem Chef

### chef-sync feature-request:
    * ability to filter types of objects replicated
    * ability to detect and resolve conflicts  (in case of unauthorized/malicious changes in the target org)
    
## DRBD:
    * great for protecting you against hardware failure
    * terrible at protecting you against software failure
    * bad on VMs where there's no cross-over cable
    
What level of availablility is worth investing in?
   * if Chef server isn't part of your control plane, you can probably tolerate an hour (or multiple hours) of outage - because you just can't deploy during that time
   * if Chef IS part of your control plane, you need to significantly invest in resources for specialized tuning and monitoring of the component services