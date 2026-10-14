# DevOps Tools (Overview | High Level)

## CI/CD Pipeline (Build, Develop and Deploy)
A series of steps from app development stage, build stage then deployment stage

### Develop
What we commonly do, create applications.

### Build
For deployment purposes, some programming languages requires us to compile it to a certain format
* .bin
* .jar
* .exe

Normally, we do build commands and some parameters to compile our work and have it on a base/shell script.
* build.sh

To name a few, some build managers are Maven, Gradel etc. that as one of its features is to manage builds

### Deploy
Compiled | built app is put into an environment (staging or production environment)

To automate CI/CD pipeline process, there are options that are out in the market.
* Jenkins
* Github Actions
* Etc.

In short, CI/CD allows for continuous delivery and deployment. Basic flow is:
* Code is pushed to a git repository
* Code is built or compiled
* CI/CD process runs the tests
* Once code is **QA approved** and code is **merged**, deploys to production

With this in place, the process gets faster as minimal intervention is needed, hence **continuous integration and deployment**

## Containers and Dependency Management
Apps in order to run have a number of dependencies it requires
* run time libraries
* OS tools

For the case of machines (development, staging and production), there should be a consistent and mirror-like versions of these dependencies.
And managing versions manually could be way confusing and difficult

The solution to enforce uniformity is containerization, and Docker is the common choice.
A Dockerfile is commissioned to specify what dependencies are needed.
An **image** is then built with reference with the **Dockerfile**
Then this image can be used on containers on the test and or the production environments.
Containers are isolated instances, having their own dependencies and their own app build.
Now this happens on the **build** stage managed by a **build tool**

## Container orchestration
From a production perspective, imagine **horizontal scaling**, to serve the needs of an increasing demand for traffic and or processing power, we add in new servers.
Since we have this managed easily by means of an almighty **docker image** and **docker containers** running on each server instance. How do we then manage these containers?
What happens when one terminates, we need to have a mechanism to have it up and running again.
Or say the demand decreases and we may want to reduce the number of server instances.
With all that in mind and without ever manually doing it.

Container orchestration comes into play as a solution for this.
* Auto-scales containers
* **Kubernetes** is a popular choice for container orchestration

## Server Infrastructure Provisioning
Each time a new server is to be commissioned, it needs to be the same as the others.
Same OS version, same docker version installed etc etc.
Manually configuring this could be repetitive and prone to inconsistencies.
**Terraform** automates this process
* It enforces configurations, that if certain things are changed that are not on Terraform's configuration, it changes it back.
* It references manifest files as configuration. Which is written in something we could relate to, which is code format.
* Configuration written in code is called **Infrastructure as Code (IaC)**

What can **Terraform** configure?
* VPC
* Storage buckets

## Server Configuration
Once a server is provisioned, the installation of software and its configuration needs to be managed as well.
**Ansible** tackles this as much.
Similar to **Terraform**, configuration is **IaC** as well by means of a **YML playbook** file

## Monitoring
Since we spawned lots of server instances. We may want to monitor its health as well.
* CPU utilization
* Memory consumption
* Which processes are acting up

**Prometheus** aggregates these metrics which to be used by **Grafana** to display those data in graphical format
