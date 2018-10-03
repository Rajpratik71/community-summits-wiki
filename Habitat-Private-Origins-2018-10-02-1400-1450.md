Chef Community Summit 2018
Erickson Conference Room
Oct 2nd, 2:00 - 2:50 pm

### Hab Auth Tokens in Production ###
Hab auth tokens created in Bldr are associated with the Bldr user profile that generated it. This is a convenient way to allow users to have API access to Bldr services from the `hab` command line. A drawback is it's the only way to generate a token. Tokens are required for more than just user development. Tokens are also required in deployed infrastructure so habitat supervisors have access to download packages from private origins. There are several drawbacks to this:
  
  1. A token created by a user is now being used to enable habitat in a live system. 
  2. Those tokens have the full API access to do anything in Bldr, associated with that user. This includes uploading packages and managing keys. Probably not something a system should have access to. 

These raise concerns about security. It would be more ideal if the deployed supervisors were using a service based account token. This would be possible today by using a different shared github account that was able to log into Habitat Bldr. It could be possible to explore the idea of allowing users to manage multiple tokens, labeled for their different usage / purpose. Similar to how you can create multiple key/secret credentials in AWS. 

The ability to provide policy or permission level access control to a token / habitat account does not exist today but the use case certainly warrants exploring. Service accounts should be limited to only allow downloading packages. It might also be reasonable to apply these permissions to team members too, allowing them access to retrieve builds for development purposes. 

### Hab Signing Keys with Teams ###
How do we manage and distribute keys across team members to sign packages?
If Bldr has a key, then it's possible that no human would need access to those keys. This is an ideal situation, and not an unreasonable one. However everyone's use case is different. 
We need a way to revoke or mark keys to manage which keys are valid and can be used. 

1. When you upload a package, it will attempt to upload the public key associated with the signing key
2. Not do that, but check to see if the public key is already published

How do we manage old keys when new keys are created?
The documentation is focused on the perspective on setting up a new origin with a new private/public signing keys. What happens when you are trying to 

Users who require keys to their origin should be able to download the key from bldr using the command line tools. 
1. download the secret key
2. download the public key at the same revision
3. do hab setup with the origin name
4. hab sees the keys and doesn't try to setup new keys

### Hab Auth Token in Studio ###
When using hab setup to set the auth token, it doesn't seem to get used when I enter the studio. This causes a problem when building a plan that depends on another package in a private origin. The workaround for this is to have the `HAB_AUTH_TOKEN` environment variable set. But from a user experience perspective, if `hab setup` asks for a token, it's reasonable for a user to expect that token is configured in a way that enables the user to enter the studio to do development / building. 

### Building feature branches ###
At the moment automatic hab bldr packages linked to github plans are only triggering off of master. So in order to create packages for feature branches pre-baseline testing. Maybe it would be possible or useful to find a way to map additional branches to different channels. 
How would you denote that this build is a non-master branch build? Habitat could add another metadata field, similar to the target metadata. 


### Gathering user feedback ###
The Habitat team needs to tap the internal teams in Chef who would be using private origins for their experience with the tools. This will help to make sure that habitat and bldr development doesn't have a blind spot since most of the team is really only experienced with using public origins. 