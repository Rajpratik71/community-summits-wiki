Matt has been using PowerShell and DSC to successfully create physical clusters but has had a problem validating hardware drivers, maybe you could use inspec to validate the configuration first? 

Challenges with blue/green deployment and data migrations.

@snoker is working on a test kitchen solution of 3 vm's (1 DC and a 2 node cluster)
link [repo](https://bit.ly/2GFwPM8)

We talked about password management, secrets management with deploying SQL.  Some people had to use pre-staged accounts to get round 

the [ad-join](https://supermarket.chef.io/cookbooks/ad-join) but you would need to tidy up the task scheduler to use it on 2016
The other option is to use dsc_resource manage the reboot.

Patching SQL Clusters? - [Cluster Aware Updating](https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating/?view=win10-ps) the DSC 

https://github.com/schubergphilis/blu