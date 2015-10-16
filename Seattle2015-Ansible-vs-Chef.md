Greenwood, 2:30pm Wednesday
Ansible and Chef Improvements

+ Competitors are Salt, Fabric, Puppet (on a downward trend)
+ those that use ansible are also considering Chef
+ first few weeks of Ansible vs Chef
  + half the room  used Ansible for a day, a handful used for a week
  + Ansible ramp up was 1/10 ramp up time of Chef
    + simple conditionals, simple loops
    + but can't write Ruby! will definitely hit a spot where this thing is hard to do in Ansible
  + agentless: great, but try doing it at scale for thousands of nodes!
+ hostname changes
  + how Chef handles limitations of Ansible
+ Comparing to Ansible Tower
+ Is there better documentation/training/use cases that could be had for Chef? 
  + Suggestion: getting started in 10 minutes?
  + Ansible and Terraform let you start quickly but you hit walls as you go along
  + w Chef, you don't hit those same rules but it takes longer
+ When people start w Ansible they used yaml files to codify things they want to do in SSH
  + Ansible role = Chef cookbook
  + Ansible  thinks that roles are an advanced topic
  + Chef cookbooks are first thing you touch, basic building block!
    + better dependency management, leverage nginx
+ learn.chef.io = free resource!
+ attributes
+ use Chef Zero on local workstation
+ Orchestration vs config mgt
+ Nathen's talks
  + chef-apply
  + no templates
  + chef-client evalute resources
+ chef generate cookbook, repo
+ yaml vs ruby
  + what about a yaml to ruby program?
  + is yaml easier? no, people are just scared of programming
+ troubleshooting errors
+ progressive reveal for new users
+ dependencies - no berkshelf/policy files