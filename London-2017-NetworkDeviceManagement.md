## Network Device Management

Discussed the existing [cisco-cookbook](https://supermarket.chef.io/cookbooks/cisco-cookbook) on chef supermarket, which is not widely used and not in active development anymore.

Target-cookbooks on the chef supermarket gives some control over F5 configuration. [Here](https://supermarket.chef.io/cookbooks/f5-bigip)

There is some upcoming activity to provide tooling for devices which provide API based configuration. Possibly from a proxy server which would run jobs on Chef's behalf and report the results back to Chef Server. This would cover a number of the cloud based network appliance providers.