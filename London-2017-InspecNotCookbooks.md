# Inspec Profiles in(stead of) Restrictive Cookbooks

Thoughts or experience on cookbook governance. 

Proposal: Set well-defined rules that cookbooks must comply with and let the people write what they want. Shift the focus to the profile instead of the cookbook.

e.x. If there are 10 httpd cookbooks, that's fine (even if it doesn't make sense) as long as they comply.

## Discussion

* Who writes the profiles?
  * Concern that security / audit teams aren't technical enough to write inspec profiles, even though it's simple
  * Security teams don't know the application specifics - cross-cluster collaboration is necessary. Security / audit own the product and carry it forward.
  * regardless of technical ability of security teams, they must approve the policies

* How do you convince people or incentivise them to contribute to a community-focused model?

* How do you enforce that cookbook developers comply with the required profiles?
  * Only a single automated process can upload to the chef server
  * The automated process needs to determine the necessary profiles based on the library cookbook(s) being consumed
  * Chef-guard(open sourced) to check compliance on `knife upload`
  * Do you NEED to use Chef Automate - can you use Splunk instead? - Cost of the Chef vs the cost of Splunk or custom development

* Create a custom ohai attribute which can be queried and reported on, for example when auditing production

* Secubus (open source)

...Discussion shifted back toward how to visualise the data, which was another open space.