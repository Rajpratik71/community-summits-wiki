What's the right way to set up Chef HA in AWS?

The model Chef has now is not the model that people want.

The backend services will be reduced down from ~7 to 3.

Chef server architecture has moved to using stateless FE servers and decentralizing stateful services away from being local to the BE Chef server(s).  For example, in AWS you will be able to use S3, RDS, and Cloudsearch.

Commercial customers, please contact Megan Gleason -- Product Team at Chef -- for early access to HA for AWS Chef Server deployments.