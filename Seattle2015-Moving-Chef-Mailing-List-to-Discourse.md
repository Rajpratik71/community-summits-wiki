Chef Summit Seattle 2015
2:30pm - Medina
# Mailing Lists to Discourse

## The Fail
+ This would be a great post-mortem of what went wrong during the migration from mailing lists to Discourse, but it's still being addressed.
+ When this transition from Sympa to Discourse happened yesterday, it resulted in many people receiving many emails.
+ During the migration, people who have EVER participated in a thread on Sympa automatically had an account on Discourse with notifications enabled, even if they had unsubscribed in the past or forgotten about the lists.
+ People who only subscribed but not participated have not yet been migrated over.
+ This was addressed in last week's IRC meeting; most of the affected people were not in the IRC meeting (as there are 2000 people on the mailing list). There was no other announcement of the cut-over. We need to be proactive about announcements like this, especially around timing and announcement.
+ The timing was also bad, being the day before Summit.
+ All existing Sympa URLs and inbound email also failed, as the new DNS record is only a CNAME to S3.

## The Reaction
+ A Discourse employee disabled email notifications across all accounts while everything was sorted out.
+ Robin from Discourse is going to send the diff of subscribed people in Discourse and people subscribed on Sympa, but have never sent an email.
+ Noah (coderanger) was given admin rights by Nathen, and made Discourse much better already. 👍
+ Chef and Chef-Dev were not separate nor injesting properly; that has been fixed.
+ Nathen sent a personal email to everyone who complained and took action with some of them, including account anonymizing.

## Other Notes
+ Discourse was set up with most of the defaults, and it is more a forum than mailing list tool.
+ We are using is Discourse-as-a-Service.
+ The Discourse people have been helping out without even being asked and have been super awesome.
+ From headers are different in Discourse than Sympa.
+ Threading in Discourse is kind of weird.
+ Discourse doesn't support plain text emails.
+ There isn't an easy unsubscribe options // admins can anonymize a user, but that alters history.
+ We've moved our mailing list to not a mailing list (even if it was called a forum in places).
+ Discourse doesn't support plugins, but PRs are accepted.
+ There is now a welcome / FAQ thread pinned with a list of what needs to be fixed.
+ You can add posts as admin/moderators without emailing everyone by creating the post in Staff, waiting 5 minutes, and moving the message.

## Questions
Why was the cutover now?
+ We weren't ready last week
+ We wanted this done before Summit
+ __Next time, we won't do this during a busy time (specifically, right before a happy hour) and test a new platform more__

Are we going to add more "categories"?
+ Maybe later, but let's let the dust settle for now
+ There are "tags", but they don't interact like mailing lists

## Action Items:
+ ✔︎ [Noah] Add how to subscribe/unsubscribe from categories and subcategories
+ [Nathen] Write up "Discourse is not a mailing list and here's why and why that's OK"
+ ✔︎ [Robb] PR to chef-rfc to update mailing list linkage and new ML advocates
  + https://github.com/chef/chef-rfc/pull/152