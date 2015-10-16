Environments vs Databags

Convention and derivation (or calculation) instead of configuration.

Q: data_bag real / write collisions? 

Validate that incoming data passes some kind of validation.
Example: have a template with field names, that validates the data bags fields exist / match type.

    Databags for orchestration
Oracle cluster definition.
DB describes a 2 node cluster. Nodes use data_bag for information sharing.


Takeaway: 
    * remove human input
    * validate input before transforming it into a DB
    * Ohai does not refresh mid chef run.
