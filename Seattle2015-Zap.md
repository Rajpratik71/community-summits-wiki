Zap

What is zap? 

Github URL for the cookbook: https://github.com/nvwls/zap

Problem - F5 LB, cron job for "503 report", no longer needed, deleted from recipe. How come we're still receiving the "503 reports"? Chef needs action delete, then come back in a week or so and delete from cookbook

Zap Pattern:
    cookbook that inplements a heavy weight resource providier
    
    ie.
```
zap_crontab "root"
  #chef name: "503 report"
```

  will go through and delete stuff there are no longer referenced

if you have 20 files in a directory, zap only needs to be set for the directory to cleanup the 20 files

How to control directory cleanup?

```
zap_directory 'var/www/' do 
  recursive true
```
  ^^^ will delete subdirs

to add file to resource tree
```
file 'file' do
  action :nothing
```

Works well for handsoff environment, specifying that chef controls files, dirs, etc 

has filters

common use case: delete directory, add to chef control via file action :nothing, cleanup users that are removed

lwrp, resources? no events for resource tree add, otherwise could use event handler. Chef doesn't have a good way of walking all the resources

how do you handle guards? 

Suggestion: save files, as a list and next run compare the current list to planned list

some use cases that it doesn't work with: partial runs, if you run a subset of your runlist

no one ever ssh's into servers right? 

zap functionality - chef controls the entire directory instead of the file (like how Windows Group Policy works)

supports why-run mode

do we add zap functionality to core chef? make it extensible to new resources/subresources
ie. 

```
directory '/var/www' do
  ...
  zap true
end
```

windows scheduled task resource on backlog to add to core