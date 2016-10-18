## Questions that came up - 

* How does this fit with Chef?  Who configures IIS?
  * Maybe Chef does global IIS config and habitat pkgs do websites, app pools?
  * Maybe IIS (and other windows features) could be treated as a habitat package - using the superisor as a standard configuration interface.
* What PowerShell versions should be suppported? or required?
  * Would be great to have DSC resoures accessible as a way to configure targets.
  * Forcing a minimum version of 3/4/5 could keep habitat out of tightly controlled environments
  * building our own powershell increases package size, but provides consistency
 * How will credentials / authentication work?
   * how do I run habitat supervisor as a domain account?
   * how do I have habitat run my service/app as another account?
   * how do I control access to the supervisor's apis?
 
## At the end of the session I asked, "If Habitat worked on Windows exactly the way you personally picture it, what would delight you the most?"
 
 * Handles windows auth securely and integrated
 * Service discovery works and supports things like finding DCs and SQL Server
 * Integrated seamlessly with Windows Clustering
 * Easy upgrade process with options on how upgrades proceed
 * Integration with Chef - we like our tools to work together easily
 * Support IIS and IIS extensions like Application Request Routing (ARR)
 * There should be a DSC resource to install/configure the supervisor
 * PowerShell cmdlets for all the tasks - we don't care about hab.exe, we want standard powershell cmdlets.