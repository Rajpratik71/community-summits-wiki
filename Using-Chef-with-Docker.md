Chef + Docker: How to use Chef and Docker together?

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