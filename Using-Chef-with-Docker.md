*Chef + Docker: How to use Chef and Docker together?*

- For testing with in the community team we using Docken to test with test kitchen.

-- We use Chef for provisioning, especially for on-prem. We are moving towards to the cloud and containers. I want to know how folks are using Chef + Docker.

- Running a Chef Client inside a docker container is not a good idea. You break the immunability by doing that, you're treating it like a lightweight VM.

-- I've viewed it in 2 different models. (Draws on whiteboard, timescale provisioning node x axis) Divergence of a baked image will happen after the pipeline. 

- Manual intervention is how you get that divergence. ie: humans altering something. Containerizing workloads should only apply if the function you are running works well in a containerized state. There is a reason why people are saying don't containerize stateful services.

-- Your app/API would be containerized with a non-containerized backend which makes it much more complex.

- You would want a scheduler and dynamic behavior with containerization. We havn't gotten to Chef side of things yet...but you end up adopting new practices as what you were doing before doesn't apply anymore.

-- We use docker and Chef in the community team. We quickly want an image, spin one up, take one down. It really saves us time. There's stuff that's baked into our image that makes it easy. We use for testing purposes - again docken. We do it for mySQL. If you think about the matrix of things we need to support for a community cookbook, this comes in handy.

- I was building windows VM, that has visualstudio to build .net app. Using Chef with it, had to run multiple converges as things failed. This was a better baked image. The amount to install this was around 1.5 hrs. 

-- What things should be baked in, in terms of compile time? What's the heavy weight thing? Like Windows boxes there are things you can pre-bake in, so it's slighty different. There are things that can totally be optimized.

- Do people use Chef to build the initial image? 

- I was using Packer and Terraform, to apps that stored state.

- The time should be in the pre-provisioning process, create the recipe to generate the image.

- This is the sweetspot to why Habitat was created. Baking an OS image is a really good pattern with config management, as there are configs that you want for your app. When you bake a docker container, it's focused on that application, it follows a different paradime than baking an OS image.

- If you it have already working, and you need the shortest step to create to image - you may need to rethink how this work is done. Again, Habitat.

-- Explain Habitat for me.

- Once you defined what your build looks like in Habitat, you create an artifact. You start with your app code, you compile it down, and you end up with an artifact, so that artifact can be run as a container somewhere. 

-- So it works for both baremetal and containers? hybrid?

- Your app when you build it, you can say "it needs a DB to start", when Habitat launches the app service it looks around the ring looking for that DB. You can run a demo env that are all docker containers on your laptop. 

- All the apps that get built out there, there is no standarization. Chef is awesome, the apps don't all think of states in a standarized why.

- and..you don't want app engs to all learn Chef, even deployment. I like the Habitat, package the app in a way that you would package anywhere. There are many different ways to deploy apps. 

-- Maybe it's not about Chef + Docker. 

- Habitat is not a scheduler. You'll need to figure out how to use a scheduler in this containerized world. You want something to be more dynamic. It goes against what Josh said, you have a single unified interface, the containers can be managed the same way - in the habitat way you can't be worried about the infra in that way.

- The scheduler is about workload placement. When I think about a workload that doesn't fit in a reg scheduler, they are tightly coupled to the gear (ie: your DB) - when you have a significant about traffic/load going into that thing, how often do you want it to be provisioned and rescheduled? You barely re-provision (in prod) as you need it to be static by design. The question is, what if I don't want to use containers, but the scheduling is containerized?

-- That infra piece that are designed to be static are not a candidate for containers. When you need to redeploy/reconfigure in a streamlined way.

- The diff between Habitat and Chef, Chef you build abstractions for all knobs, gear that needs to be provisioned...

-- so the answer is...look at Habitat? and Chef needs to figure out how to train the devops community.

- yes. When it's on the app side, habitat less code, abstraction makes more sense, installing a package + service but not dealing with configuration.

- Habitat guides you away from :( ways to do config. In your docker file you have to start from scratch :(. There's not a lot of visibility of what's inside of your package. You have a kernel, in your docker file you have to state what to install and built.

-- ...and then you end up with this large container...because you want to built and remove it because ultimately you just want the app.

- If you're running containers in prod - they have like a container in prod. When you have scheduler on top of this, you have schedules distributed all across your infra - no visibility, hard to manage. 

- You have visibility into the build service with Habitat. Cool stuff around automated rebuilding too.

-- What's the learning curve like? (Habitat)

- Do you know bash?

-- Yeah. so for a new pipeline, are you just scripting this out?

- Habitat has determinisitic build system, interface is similar to bash. You define what you need at build time and then create an artifact - you can just use a standard CI, you can just do the build in the CI. We have a build service is coming, if you have github repo and inside the repo you have a plan.sh, you can tell the build service is "this is a Sass offering" - based on the dependencies in the package, it'll grab that and build, and then build up the app into a docker container.

- When you dive in to Habitat, you'll see hab studio. This is what you would put into your build pipeline.

-- I have server and app, where does Chef end and Habitat starts?

- Chef infra automation, Habitat app automate. Define the packages and provision with any config mgmt tool you want. Habitat does nothing with infrastructure automation.

- Habitat package does not use your OS library. If you need to patch OpenSSL, that happens in the plan.sh.  We have 2 update strategies, all at once choreographed, and then a rolling update strategy. Leader, follower topology. It's not a 100% garaunteed right now, if it starts up then we mark as green(good).

- Is there communication between Chef and Habitat so you can query the Chef run?

- Habitat has an API to query, global state. you can hit both of the API endpoints.
 