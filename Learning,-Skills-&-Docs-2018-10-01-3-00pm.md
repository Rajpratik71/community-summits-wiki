- What document or training course could be added?
    * Policyfiles
    * Whitepapers with example implementations (why vs how)
    * 1-page overview of all Chef offerings  
    * Not prescriptive enough sometimes - patterned learning vs all available customizations
    * Design patterns and anti-patterns:
       * Recipes
       * Resources

- docs.chef.io is implementing docs as code
    * lowers friction to contribute
    * easier to contribute
    * automating as much as possible from comments in source - resource inspector
    * creating test harness for documentation 

- What kinds of guides?
    * custom resources
    * address documentation when something is pulled back into Chef from Community
    * event handlers
    * helper methods
    * documentation for intermediate developers, where reading the code is basically the best option
    * usage examples for resource properties 
    * using resource inspector 
    
- What's working well?
    * Chef Rally hands-on experience

- Suggestions
    * Balance of good narrative versus pure code comments
    * Foodcritic rule or changelog reference - how to discover deprecations

- Chatbot in Community Slack?
    * Can take up scrollback space
    * Can make new members feel less welcome
    * Could be a direct message chat
    * Conflicting information between bot and user?

- Resource Inspector
    * to generate community cookbook docs automatically
    * to generate updated documentation for Chef releases 
    * built-in IDE support
    * code completion
    * documentation snippet
    
- Versioning of documentation
   * how verbose is the right balance?
   * split up by Chef platform rather than all-in-one   
   * `introduced` flag into code to add to docs
