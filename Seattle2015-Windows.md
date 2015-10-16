Raveena 11:30 - WINDOWS

Full Windows `package` resource compatability with the OSS cookbook is coming to core Chef this quarter

Adam E spent a fun weekend setting up a chef-client run as a Scheduled Task.  He is committed to providing workarounds for issues people have.

Test Kitchen, Knife, Chef Provisioning - all these need to leverage a shared WinRM transport layer so they don't have different issues.

Transfering large files over WinRM is hard.  Its also probably a bad pattern to store large binary files (packages) in a cookbook.  These should be in a package manager like Artifactory. (Chef Server is only meant to be a store for lightweight json objects / cookbooks, it is *not* a way to store binaries -- actual binary repositories are optimized much better for hosting binary files, including metadata around those files).

Rebooting - not supported through Test Kitchen.  https://github.com/vinyar/chef_win_reboots has good rebooting patterns.

Really, really long chef-client runs on Windows servers because they try and put as many services on each Windows box as possible.  Possible solutions - build an image factory (Packer was suggested) to pre-bake most of the chef-client run.  DSC has good support for managing IIS resources.

Apparently, chef-client runs in Packer are broken right now.

Powershell DSC with windows examples:
    DSC example iis config: https://gist.github.com/echohack/957aa29b493e1b7b8967
    Chef recipe invoking DSC_script: https://gist.github.com/echohack/09c3daf494949a6951bd
    DSC Gotchas (DSC_script): https://gist.github.com/echohack/68ea3a61a5f4042357ae

Chef + Windows Nano = Awesome