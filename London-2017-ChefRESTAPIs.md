## Chef's REST API's Use Cases and Challenges

#### In Attendance

Niu Solutions ltd
Oracle
Danske Bank
SAP
Barclays

#### Synopsis

The Chef Rest API's have some interesting use cases, but a little difficult to get up and running with. The goal we have at niu is to automate configuration of new environments in Chef so that a non technical member of staff can have some limited control over configuring the configuration for a new customer in our organisation. We've made some progress on this but spent a long time.

####  Key challenges

This is mostly due to the authentication mechanism and the documentation not providing enough detail on the authentication flow. The canonical headers and certificate auth system are fiddly. This may be easier when using the Ruby and Python libraries for signing the requests, but we were developing in C#.

The compliance scanner provides an auth mechanism closer to an OAuth flow which is easier to work with, Automate also seems to follow allong these lines as well.

#### Requests for Improvements
* The documentation could definately be improved, perhaps with an example of a generic authentication flow showing requests/responses with full headers.
* The auth process does not roll/expire authentication tokens, there is an API endpoint to roll a key but this requires you to handle this in your own client app rather than Chef forcing your token to expire. It would be more secure if the API did this for you.
* [RFC038](https://github.com/chef/chef-rfc/blob/master/rfc038-token-authentication.md) suggests that there was a plan to improve the chef server API auth mechanism, but this is currently on hold. It would be great if this could be implemented.

## Questions
#### Why not use knife?

Using the knife directly is a workable solution to avoid making API calls directly, but requires you to keep knife up to date with your API client. 

#### Using the API to manage run lists?

Probably better to use a tool like Terraform than trying to engineer a solution using the API.