Chef & Azure

Topic submitter:
Stuart Preston (https://github.com/stuartpreston)

Links:
  https://github.com/chef/chef-provisioning
  https://github.com/chef/chef-provisioning-azure (Azure Service Management driver for Chef Provisioning - machines/cloud services...)
  https://github.com/pendrica/chef-provisioning-azurerm (Azure Resource Management driver for Chef Provisioning)
  https://github.com/pendrica/kitchen-azurerm (Azure Resource Management driver for Test Kitchen)
  https://github.com/Azure/azure-quickstart-templates/tree/master/chef-extension-windows-vm

Resource manager relies on Azure resource manager for idempotence.

First set of resouces allows for basic interactions and provisioning with Azure via the resource manager.
This is done via a 'hand' generated .json file.

chef_extension client_type: 'ChefClient" ... 
documentation located here:
https://github.com/chef-partners/azure-chef-extension

Creating resource template .son
* install visual studio with azure plugin. 
* create a resource manually, and look at the 