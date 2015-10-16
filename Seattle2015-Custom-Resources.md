Example Cookbooks using new 12.5 resource syntax:
    https://github.com/bflad/chef-docker
    https://github.com/chef-cookbooks/httpd
    
Documentation:
    https://docs.chef.io/custom_resources.html
    https://docs.chef.io/release/12-5/dsl_custom_resource.html

# Custom Resources
https://docs.chef.io/custom_resources.html

how to deprecate an LWRP: http://www.rubydoc.info/github/opscode/chef/Chef%2FLog.deprecation
https://github.com/chef/chef/blob/master/lib/chef/mixin/deprecation.rb

```
load_current_value do
  docker.get(name).command
end

property :name
property :command, string

Recipe:
```