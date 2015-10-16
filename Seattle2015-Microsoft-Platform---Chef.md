# Developing with Chef on the Microsoft Platform

Problem with using exiisting openssh solutions (instead of a MS solution) is that a) does not integrate with windows auth, and b) companies don't like third-party (not part of the core OS/vendor offering)

Would like better documentation on configuration of WinRM for chef bootstrapping.
Note: The knife-windows 1.1.0 release has better support for SSL bootstrapping and config:
    https://github.com/chef/knife-windows/blob/v1.0.0/DOC_CHANGES.md#new-subcommands-to-automate-winrm-ssl-listener-configuration
    https://github.com/chef/knife-windows/blob/v1.0.0/DOC_CHANGES.md#new-winrm_ssl_verify_mode-option
    

Barrier to entry is that getting a vagrant box for local testing (Kitchen, etc) is challenging. 

The path-helper in chef helps with writing Windows cookbooks

What are the minimum set of tools on the Windows platform
- ChefDK
- Programmer's text editor
- ConEmu
- git
- vagrant
- local hypervisor (optional)
- (some method of spinning up a VM for kitchen testing)
- whichever kitchen drivers are needed for your particular solution

Think about taking the Chef preflight scripts used by the sales engineering team and making it a chefdk command ("environment verify" or something)

Big gap in pester is there are no matchers for a lot of "server" related stuff. Would be nice to have matchers like this.

Question about Visual Studio support for chef code, etc. 




Example cookbook that gives you the Windows tools except for vagrant:
    . { iwr https://raw.githubusercontent.com/adamedx/winbox/0.1.79/files/default/install.ps1 } | iex;install-workstation
https://github.com/adamedx/winbox

ChefDK bootstrap script/repo from Nordstrom to get a windows workstation set up
https://github.com/Nordstrom/chefdk_bootstrap
