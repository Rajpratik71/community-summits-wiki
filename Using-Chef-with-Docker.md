Chef + Docker: How to use Chef and Docker together?

- For testing with in the community team we using Docken to test with test kitchen.

-- We use Chef for provisioning, especially for on-prem. We are moving towards to the cloud and containers. I want to know how folks are using Chef + Docker.

- Running a Chef Client inside a docker container is not a good idea. You break the immunability by doing that, you're treating it like a lightweight VM.

-- I've viewed it in 2 different models 