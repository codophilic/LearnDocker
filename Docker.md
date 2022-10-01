# Learn About Docker

## Why do we need Docker?

- Suppose there is an full stack application which uses different technologies like NodeJS, MongoDB, Nginx etc, which requires libraries , OS version ( checking the compatiblitiy which all tech agrees to run on that OS ) and other dependencies. 

- Apart from this if the application needs a new upgradation then again we need to check the compatiblity of those components.

- Suppose there are different environments for an application testing , again we need to make sure those environments must have the required components and compatiblity to host our applications.

- **So Docker help to solve these problem with the containers where all the components are placed in seperate containers consisting there required libraries and dependecies and those containers were executed**


## Basic concepts of Operating System 

- Every OS consits of two main common components , an **OS kernel and sets of software components** . So e.g for a Linux OS, the OS kernel which interacts with the underlying hardware is common for software components like Ubuntu,CentOS etc. These software components may have different user interfac, file managers etc. 

- The Docket containers share this underlying OS kernel.

- So let's say we have installed Docker on Ubuntu OS. So Docker can run any other type of Linux OS on top of Ubuntu because they share same OS kernel which is linux.

- So we cannot run a windows based container on a Docker host with Linux kernel. For that we will required Docker hosted on windows kernel.

- In windows we have a subsystem of linux where we can execute linux operations (WSL). So a linux container can be run on windows hosted docker.


## What are containers?

- A container is a standard unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another. 

- A Docker container image is a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system tools, system libraries and settings. (1)

## What is Docker?

- Docker provides the ability to package and run an application in a loosely isolated environment called a container. The isolation and security allows you to run many containers simultaneously on a given host. 

- Containers are lightweight and contain everything needed to run the application, so you do not need to rely on what is currently installed on the host. You can easily share containers while you work, and be sure that everyone you share with gets the same container that works in the same way.

- Docker is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly. With Docker, you can manage your infrastructure in the same ways you manage your applications. 

- By taking advantage of Docker’s methodologies for shipping, testing, and deploying code quickly, you can significantly reduce the delay between writing code and running it in production.


## Comparing Virtual machines and Containers.

- Incase of docker we have the underlying hardware, on top of it the OS and then the Docker installed on that OS. Docker manages the containers and run with their libraries and dependencies. Incase of Virtual machines there is a hypervisor (A hypervisor, also known as a virtual machine monitor or VMM, is software that creates and runs virtual machines (VMs). A hypervisor allows one host computer to support multiple guest VMs by virtually sharing its resources, such as memory and processing. )on top of the hardware and on them the VM are there. Each VM has its own OS inside it with its dependencies and libraries.

- Incase of VM, higher utilization of hardware takes place since there are multiple OS kernels. It also consume higher disk space. Whereas dockers containers are light weight which also makes boot up process faster.

- Docker containers has less isolation and more resources are shared between the containers whereas VM's have complete isolation from each other. Since VM's don't rely on the underlying OS or kernel, we can run different OS. (2)

- Moslty Dockers and VM work together for an application. Dockers containers are hosted on VM's.


## Images and Containers.

- Images are read-only templates containing instructions for creating a container. A Docker image creates containers to run on the Docker platform.

- Think of an image like a blueprint or snapshot of what will be in a container when it runs.

- Images are built as a series of layers. Layers are assembled on top of one another. 

-Let's say we want to create a Docker image of a Hello World Java application. The first thing we need to think about is what does our application need.

- To start, it is a Java application, so we will need a JVM. OK, this seems easy, but what does a JVM need to run? It needs an Operating System. Therefore, our Docker image will have an Operating System layer, a JVM, and our Hello World application.

- A major advantage of Docker is its large community. If we want to build on to an image, we can go to Docker Hub and search if the image we need is available.

- A container is an instance of an image. Each container can be identified by its ID. Going back to our Java development analogy, we could say that a container is like an instance of a class. So images is a class and container is an object or instance of that class.

- Docker defines seven states for a container: created, restarting, running, removing, paused, exited, and dead. This is important to know. Since a container is just an instance of the image, it doesn't need to be running.

- E.g In docker if run command, docker run hello-world  

1) docker: It is docker engine and used to run docker program. It tells to the operating system that you are running docker program.

2) run: This subcommand is used to create and run a docker container.

3) hello-world: It is a name of an image. You need to specify the name of an image which is to load into the container.


## Docker Hub

- We can consider Docker Hub as a service from Docker for locating and distributing containers for each image within the specified team. It can manage the sharing and storage of Docker image.

- Docker Hub is a hosted repository service provided by Docker for finding and sharing container images with your team.

## Installing Docker

- Here we are installing a docker on windows host having linux vm which is Ubuntu OS. Commands used were curl -fsSL https://get.docker.com -o get-docker.sh , sudo sh get-docker.sh 

- The installation steps will vary for windows and MacOS.

## Running a Docker command

- Running an image from Docker Hub repository having name whalesay (3)

## Docker commands

- Run command: Suppose if we run `docker run nginx` , this will run an instance of the nginx application from the docker host if it exists on the machine and if the image is not found then it will reach the docker hub to find the image and it will pull that image down in the machine ( It happens for the first time ).

- List command: 

- A. Suppose if we run `docker ps` it will list all running containers with some information about them like ID, image name, command, creation time etc. Each containers gets automatically a random ID and random name. (5)

- B. Suppose we want to list images  run command `docker images`. (8)

- Stop Command: Suppose if we want to stop a container we need to have its ID or name e.g `docker stop sleepy_diffie`.(6)

- Remove command: 

- A Suppose we want to remove containers permanently which takes up spaces we can run `docker rm ID` e.g `docker rm sleepy_diffie`. We cannot remove running containers in docker. (7)

- B. Suppose we want to remove an image permanently run command `docker rmi image_name`. Before deleting an image we need to be sure that no containers are running off to that inage .(9 10 )

- docker rm $(docker ps -aq) removes all containers.

- docker rmi $(docker images -q) removes all images

- Pull Command: We can just pull the image to store it on the host and not run the container. Command is `docker pull imagename`. (11)

- Containers lifespan: Containers are not meant to host an OS they are meant to run a specific task or process such as to host an instance of an image. Once the task is completed the container exits. A container only lives as long as the process inside it is alive. If the service inside the container is stopped or crash, then the container exits. You can refer the example whalesay image where the docker container after completion exited itself.

- Execute command: Suppose we want to run execute some commands on running containers we can do it using command `docker exec container_name COMMAND`. When we run `docker run ubuntu` it gets exited immedietly so we use a `sleep` command over it.  (12)

- Attach an Detach: Suppose when we run a container which uses an images that runs on CLI/ foreground like running a web server it called an attach state. This makes difficult to add any inputs to the docker containers.(13)
Docker provides to run such images in the background like a detach state. The container will continue to run in the backend. (14)
In the Detach state the docker provides an ID which can be use to attach it again.(15)

- Run a container with provided name: docker run -d --name name imagename




