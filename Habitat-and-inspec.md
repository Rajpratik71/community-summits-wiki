Adam Leff intro - story so far

"what if we were able to take an inspec profile, and ship it like any other habitat artifact?"

Separate from the application itself
Runs as a service, allowing continual compliance
`inspec habitat profile [create|upload]` -> "shits out a habitat artifact"
Runs inspec every 5 minutes, spits out JSON with its finding.
Interval is configurable (300 second default)
Plans for taking advantage of the event service so that the data can be subscribed to for real time insights. (future state)

Currently requires that each instance have the inspec sidecar running, as opposed to one inspec instance for a given ring. 

Unbounded vs. bounded events? Should these be open-ended, or purpose-driven in architecture?

Can it be tied to multi-instance workflows? i.e. pulling data from one service to seed into another service's inspec tests

Clarifying the definition of "application". Does component scanning add up to full estate scanning, also, does it overload things if there are potentially redundant tests running on each microservice?

health vs. compliance. Are both appropriate for inspec to handle? Invoking ruby to do simple health checks might be overkill when a single line of bash might suffice. 

re: healthchecks
things that are not being used now, but will likely be in the future
When upgrades happen, should the healthcheck be automatically run to determine the state of an instance post-update.

Talk of the ability to have arbitrary, user-definable messages for the health checks, as opposed to the default pre-canned descriptions for return codes.

Having a way for healthchecks to reference the last compliance run, rather than invoking inspec inline, could split the difference. If we want compliance failures to trigger an event (e.g. remove node from LB), we can have the health check take action on >0 failures on the last run. Would require the json being stored somewhere that can be referenced easily to provide an easy road to adoption.

health vs. monitoring
Ability to pull trend data more granular than simple healthy/unhealthy, and seeded into a system like nagios/zabbix

There may be *seeeeeecret* forthcoming features that fit in here somewhere. Remaining cagey for job-security reasons. :-) Inquisitive minds can take a look at hab source for development direction.

Try the inspec habitat profile stuff! Reach out to Adam Leff on Community Slack with feedback!