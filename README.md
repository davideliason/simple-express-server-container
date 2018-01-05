# Simple Express Server
## Using Docker Containers!!
### Woohoo!
#### [David Eliason](http://www.davethemaker.com)

# Intro
[tutorial](https://aws.amazon.com/getting-started/container-microservices-tutorial/module-two/)
container mostly on my own, solidify concepts around Docker containers and also blow off the cobwebs of working on the back-end as it's been a little while ;)

## Docker Cloud Simple Express Docker Image can be ran as a container by :
 $ docker run -p 49160:8080 davethemaker/simple-express-server-container:v1 and http://0.0.0.0:49160/ in browser.
 
## 10,000 foot overview:
At this point, creating a monolith app, microservices will be up at some other point. 

Build node.js/express/ code, keeping it simple without mongodb at this point. Create repo in ECR. ECR login -> build image of code, tag it -> push repo to ECR. Boom, that's sitting in the cloud.

Now, deploy that image. ECS = Elastic Container Service, will manage container(s) over EC2 cluster. Client -> LB -> Target Group -> Cluster of EC2 instances tnx to CloudFormation. 

Within ECS, config LB, Target Group, build cluster using YAML file, task that tells ECS how to use the container(s) with the EC2 instances.

[Docker Getting-started](https://docs.docker.com/get-started/part2/#introduction). Build container -> Services (how containers behave in production) -> Stack (interactino of all the services). I'm going to be following these concepts using this app.

## Notes [remove img & container](https://tecadmin.net/remove-docker-images-and-containers/#)
docker rmi ___ to remove image from local
docker rm ___ to remove container
docker images  // list local docker images
docker stop __container___  // stop

## Steps
1. [Container] build out simple express app, VCS in services folder
 - install npm modules/dependencies
 - remove node_modules so they don't get ported to container :)
 - ah, can use .dockerignore file instead (see below)
2. Build Dockerfile to create an image -> push to AWS ECR -> deploy just to test on a basic level.
 2.1 [build local docker instance first b4 ECR deploy](https://nodejs.org/en/docs/guides/nodejs-docker-webapp/)
	: $ docker login
	: $ docker run hello-world //successful
	: create Dockerfile + .dockerignore (node_modules, npm-debug.log)
	: run the build command to create Docker image
	  - $ docker build -t simple-simple-express-server-container-image .
	  - $ docker images  // see image id/repo/tag
	  - server's port is 8080
	  - $ docker run -p 49160:8080 -d [image name]  // -p tag maps my machine port 49160 to the container's published port 8080
	  - $ docker ps  // get app port (8080 mapped to 49160)
	  - curl -i localhost:49160 to get express server output, or
	  - http://0.0.0.0:49160  in browser
 2.2 Deploy Docker image to Docker cloud.
   - docker login
   - tag the image ex: docker tag simple-express-server-container my_username/simple-express-server-container:v1
   - publish the image: docker push my_username/simple-express-server-container:v1
   - IT WORKS: $ docker run -p 49160:8080 davethemaker/simple-express-server-container:v1 and http://0.0.0.0:49160/ in browser.
3. Take it to the next level by building a cluster: Build up AWS CloudFormation infrastructure config code within infrastructure folder. At this point, the only file outside those two folers is the README file
4. Oops, have to rm node_modules, add .gitignore
5. 