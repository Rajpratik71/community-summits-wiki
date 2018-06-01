Security and users want to know what changed where and when.  This has been difficult to keep up with at scale using Automate.
Use Chef reporting handlers, which run at the end for Chef Client run and always run (even when a failure occurs).
* Send the logs to any logging solution is needed.
* Splunk charges by logs sent.  In an isolated environment, the forwarder can forward to a heavy forwarder before sending to Splunk to do additional filtering.