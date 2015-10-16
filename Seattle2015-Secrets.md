wwwwwSecret note taking for Secrets!

## What secrets?

"Anything that's radioactive"

So not something like "apache".  It doesn't matter.

## Is anyone using autoscaling (AS) groups or ... w/ chef vault?

Chef vault doesn't lend itself well to AS.

There's no 

chef "sensitive" masks all data from resource from output
santizes logs

make sure to set backups to 0


## Hashi w/ Chef integration?

@ Hack day on Friday

## Anything on the roadmap from Chef for managing secrets?

As far as we know, no.  Encrypted databags & Chef vault exist today.

Chef Vault w/ Autoscaling doesn't work due to bootstrap problem.


## Server identity problem

You need some way to identify the server (so far only done w/ IAM in AWS)

## So what are people in the room doing in the room today to manage secrets?

Chef Vault = few hands
Encrypted databags = few hands
Secrets in the clear = few hands

## Library cookbook that provides some method/DSL etension.  A string w/ crypt text that you're looking for & path.  But you need the key.

Encrypted databags does not support key rotation.  

Citadel (written by Noah K). For AWS to guide you through IAM roles, ec2 stuff, etc. works well and fine, but is 100% tied to AWS.

Hashicorp Vault - formally investigated and verified by outside party
No good Chef integration right now
Server Identity is still lacking here
>> It would be really cool if osmeone wrote a auth-back end for hashicorp vault

Keywiz - formally investigated and verified by outside party
No good Chef integration right now
Server Identity is still lacking here

Red October (could be used for this, but probaby not)

## Secrets through Chef

Nodes can edit their own run-lists, so you can't trust it.  If a node gets compromised and someone has access to the node directly.

## Has anyone tried to attack your security? Pen-test it?

If you can spin up a node and try to access secrets that it shouldn't have. 

## Identity management (vs. secrets) can be used for certs per server.