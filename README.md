# Simple Express Server
## Using Docker Containers!!
### Woohoo!
#### [David Eliason](http://www.davethemaker.com)

# Intro
[tutorial](https://aws.amazon.com/getting-started/container-microservices-tutorial/module-two/)
container mostly on my own, solidify concepts around Docker containers and also blow off the cobwebs of working on the back-end as it's been a little while ;)

## 10,000 foot overview:
At this point, creating a monolith app, microservices will be up at some other point. 

Build node.js/express/ code, keeping it simple without mongodb at this point. Create repo in ECR. ECR login -> build image of code, tag it -> push repo to ECR. Boom, that's sitting in the cloud.

Now, deploy that image. ECS = Elastic Container Service, will manage container(s) over EC2 cluster. Client -> LB -> Target Group -> Cluster of EC2 instances. 

Within ECS, config LB, Target Group, build cluster using YAML file, task that tells ECS how to use the container(s) with the EC2 instances


## Steps
1. build out simple express app, VCS in services folder
 - install npm modules/dependencies
3. Build up AWS CloudFormation infrastructure config code within infrastructure folder. At this point, the only file outside those two folers is the README file
4. 