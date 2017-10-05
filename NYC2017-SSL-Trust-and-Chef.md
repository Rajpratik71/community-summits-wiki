# SSL Trust Bootstrap

How do we bootstrap the rest of our org's trust chain inside Chef?

Trusting things like Artifactory for gem installs with internal CA

First pass, ssl_verify none, done!

Best option is to build in trust roots when building hosts

This came up because of metadata.rb gems, can't install certs at compile time for that

Does work if using `knife bootstrap`, you can currently use the existing .chef/trusted_certs/ system

Maybe some day in the future, a trusted_certs/ un-segment


