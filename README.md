# multi-docker

This is a multi docker container application to demonstrate a real-world scenario.

The front-end which is based on *react* asks for an index of the Fibonacci number.
The backend server computes (with the help of *worker*) the corresponding Fibonacci number if not readily available in the memory, stores it (index and corresponding computed value) in the memory (*postgres* and *redis*) and then returns the corresponding value.
If the given index is already found in the memory, then it is returned directly without computing any further.

**docker-compose.yml** helps to build the nginx, client, server and worker services.
Based on what the user is intended, the corresponding URL access is diverted  (by nginx) either to api *server* (for computation by *worker*) or *client* (for front-end display).

**.travis.yml** uses the development docker files to build and test the corresponding services. If all tests are passed, then production ready docker images are generated and pushed into the docker hub which are further pulled by AWS Elastic Beanstalk to automatically deploy for the user access.


# AWS Production setup

In the production the architecture changes significantly.

*nginx*, *production files*, *server*, *worker* are hosted in Elastic Beanstalk (EB) instance.

*Postgres* is hosted in AWS Relational Database Service (RDS). 
This has multiple benefits: Automated backups and rollbacks; easy to scale; has built in logging and maintenance; probably, AWS RDS provides better security than we can provide. In future, we can migrate our application from AWS EB to some other service while still preserving the postgres services.

*Redis* is hosted in AWS ElastiCache (EC). 
This has multiple benefits: easy to scale; has built in logging and maintenance; probably, AWS EC provides better security than we can provide. In future, we can migrate our application from AWS EB to some other service while still preserving the redis services.

Successful deployment in AWS:
![successful_deployment](https://github.com/sandeep2995/multi-docker/assets/8388528/04779627-0e29-41e0-9e4b-d43f7b821f7f)


Successfully deployed APP in the Browser:
![deployed_app](https://github.com/sandeep2995/multi-docker/assets/8388528/3aa94280-9c83-4004-b0b4-96b45ff4a7d7)

