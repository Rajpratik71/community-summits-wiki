*Problems and (some) Solutions*

- One person has an issue with the Chef server when using chef-vault at over 4000 nodes
- One person runs an atypically large single server. Every change to their cookbooks are new cookbook versions and they have very large cookbooks.  After a couple of years they have 100s of versions and it was pretty slow because of the amount of data being sent back to the clients.  They solved it by reaping old versions of cookbooks.
- Depsolving issues with large number of cookbooks.
- One person needs the number of nodes that matches a search but not the actual data.  A trick they are using is to set rows=0 in the search query
- Partial search can help in some situations
- Whitelisting attributes can help a lot



*Possible Future Paths*

- Tooling to help with cookbook cleanup
- On AWS, single EBS backed instances can get you very far
- On AWS, using native AWS services can be good
