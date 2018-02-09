Markus Grobelin, Julian, Christoph, Dominik

chris-rock: what is a report to you? everyone has a different idea of what that means.

Markus:
usually periodic audits are just about that auditor look at a whole pile of documents & only if something "appears" wrong will they start digging into it.
example: manually create a big Excel sheet and put a manager's signature on it, done! :-)

hmmm... rather than filling in stupid Excel sheets day-to-day then they can do some real work.

InSpec - easy to get started, but what do you do with the output. you don't want to show the code but merely the results. for example the graphs and things in Chef Automate. higher-level people don't have Wi-Fi say on the train, they like to read paper documents and annotate them, just look into it later.

Markus' company does genome research & capture information about it. e.g. that genome analysis was correct. and need to keep that history for a very long time, say ten years. the consumers of these outputs aren't digital & don't have access to our network.

Chris - how would you distribute these data to your consumers of it?
Markus - what I would like is to run these daily tests that is the snapshot of state. personally I like the exporters -- thanks Jared Quick? -- there's an HTML exporter but its output is ugly. (Chris - it's inherited from RSpec so yeah...) but it's a great start.

It would be nice for the report to have our logo on top, the date.
(Chris shows off Chef Automate node report)
Markus - this is great but it can't be a website. Also it's too technical for these guys/girls (auditors).
Chris - but it's a technical test. (more demo)

Markus - there won't be levels of criticality for us. it's black or white. so thus it's too much info for their needs. the base assumption is that everything is fine otherwise they will come to visit us :-)

Markus - you mentioned this is exportable in some way
Chris - yes, JSON and CSV

Dom - what exporter are you looking for? because you made this noise...
Markus - HTML or PDF. and non-technical.

HIPAA care more about lab environments, not care about processing part.
some other auditors care more about processing.

Dom - if you get an HTML would you still want the PDF?
Markus - no.
Dom - vice versa?
Markus - no. one is enough.

Here in Germany, EMRs are printed out at your doctor and if you change doctors they're sent by mail. So that is the status quo and the environment you need to think of.

10TB of genome data generated per day from Illumina machines that basically take photos of people, etc. from US. they run Windows 7 ... ok a bit outdated, but we must test that certain things are on those machines, and some things are not on those machines. we wanted to put certain things on these machines like Nagios agents, etc. and normally this voids your warranty but we have enough good customers that they allowed us.

Dom - can you manage these machines by installing s/w on them?
Markus - yes but we try not to.
Dom - and you can do this remotely?
Markus - we are starting to install RDP. so that we don't have to go to the lab because you know, it's a clean room, etc.

Chris - are you already running reports? how do you do it?
Markus - yeah we do it via Jenkins - using JUnit XML integration from InSpec.