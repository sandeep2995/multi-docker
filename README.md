# multi-docker

This is a multi docker container application to demonstrate a minimal real-world application setting.

The front-end which is based on *react* asks for an index of the Fibonacci number.
The backend server computes the corresponding Fibonacci number if not readily available in the memory, stores it (index and corresponding computed value) in the memory (postgres) and then returns the corresponding value.
If the given index is already found in the memory, then it is returned directly without computing any further.

**docker-compose.yml** helps to build the nginx, client, server and worker services.
Based on what the user is intended, the corresponding URL access is diverted  (by nginx) either to api server (for computation) or client (for front-end display).

**.travis.yml** uses the development docker files to build and test the corresponding services. If all tests are passed, then production ready docker images are generated and pushed into the docker hub which are further pulled by AWS Elastic Beanstalk to automatically deploy for the access in the cloud.
