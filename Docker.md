# Learn About Docker

## Why do we need Docker?

- Suppose there is a full stack application which uses different technologies like NodeJS, MongoDB, Nginx etc., which requires libraries, OS version (checking the compatibility where all these 
tech agrees to run on that OS) and other dependencies. 

- Apart from this suppose the application needs a new upgrade then again we need to check the compatibility of those components.

- Suppose there are different environments for an application testing, again we need to make sure those environments must have the required components and compatibility to host our applications.

- **Docker help to solve this problem by providing its own component called containers where all the components are placed in separate containers consisting there required libraries and dependencies. Only these containers were executed**

## What is Docker?

- Docker provides the ability to package and run an application in a loosely isolated environment called a container. The isolation and security allows you to run many containers simultaneously on a given host. 
<details>
    <summary><h3>What are containers?</h3></summary>
        <p>1. A container is a standard unit of software that packages up code and all its dependencies, so the application runs quickly and reliably from one computing environment to another.</p>
        <p>2. A Docker container image is a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system tools, system libraries and settings.
        </p>
        <p>3. Containers are lightweight and contain everything needed to run the application, so you do not need to rely on what is currently installed on the host. You can easily share containers while you work, and be sure that everyone you share with gets the same container that works in the same way.
        </p>
</details>


<a href="url"> <img src="https://github.com/codophilic/LearnDocker/blob/main/Docker/1.PNG" align="center" height="500" width="900" ></a>



- Docker is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure, so you can deliver software quickly. With Docker, you can manage your infrastructure in the same ways you manage your applications. 

- By taking advantage of Docker’s methodologies for shipping, testing, and deploying code quickly, you can significantly reduce the delay between writing code and running it in production.


## Basic concepts of Operating System 

- Every OS consists of two main common components
   1. **OS kernel**
   2. **Sets of software components** 

- For a Linux OS, the OS kernel which interacts with the underlying hardware is common for software components like Ubuntu, CentOS etc. These software components may have different user interface, file managers etc. 

- Docker containers share this underlying OS kernel. So let's say we have installed Docker on Ubuntu OS, docker can run any other type of software component of Linux OS on top of Ubuntu because they share same OS kernel which is Linux.

- We cannot run a windows based container on a Docker host with Linux kernel. For that we will require Docker hosted on Windows kernel.

- In windows, we have a subsystem of Linux where we can execute Linux operations (WSL). So a docker having Linux container can be run on Windows hosted docker.


## Comparing Virtual machines and Containers.

![](https://github.com/codophilic/LearnDocker/blob/main/Docker/2.PNG)

Containers  | VM
------------- | -------------
 In Docker the underlying hardware is shared in the system, on top of it the OS and then the Docker installed on that OS. Docker manages the containers and run with their libraries and dependencies. | In Virtual machines, there is a hypervisor (A hypervisor, also known as a virtual machine monitor or VMM, is software that creates and runs virtual machines (VMs). A hypervisor allows one host computer to support multiple guest VMs by virtually sharing its resources, such as memory and processing.) on top of the hardware and on them the VM are there. Each VM has its own OS inside it with its dependencies and libraries.
 In dockers, containers are lightweight which also makes boot up process faster. |  In VM, higher utilization of hardware takes place since there are multiple OS kernels. It also consumes higher disk space.
 Docker containers have less isolation and more resources are shared between the containers. | VM's have complete isolation from each other. Since VM's don't rely on the underlying OS or kernel, we can run different OS on same system. 

- ***Mostly Dockers and VM work together for an application. Dockers containers are hosted on VM's.***


## Images and Containers.

- <h3>Images:<h3>

   - Images are read-only templates containing instructions for creating a container. A Docker image creates containers to run on the Docker platform. Think of an image like a blueprint or snapshot of what will be in a container when it runs. Images are built as a series of layers. Layers are assembled on top of one another. 

    - Let's say we want to create a Docker image of a Hello World Java application. The first thing we need to think about is what does our application need. Firstly it is a Java application, so we will need a JVM. OK, this seems easy, but what does a JVM need to run? It needs an Operating System. Therefore, our Docker image will have an Operating System layer, a JVM, and then our Hello World application.

    - A major advantage of Docker is its large community. If we want to build an image, we can go to Docker Hub and search if the image we need is available.

- <h3>Containers:<h3>

    - A container is an instance of an image. Each container can be identified by its ID or by a unique name. Going back to our Java development analogy, we could say that a container is like an instance (*object*) of a class. So images is a class and container is an object or instance of that class.

    - Docker defines 7 states for a container:

        1. Created

        2. Restarting
        
        3. Running
        
        4. Removing
        
        5. Paused
        
        6. Exited
        
        7. Dead. 

    - This is important to know. Since a container is just an instance of the image, it doesn't need to be running all time.

- For an example, in docker if run command, **`docker run hello-world`**  

    1) **`docker`**: It is docker engine and used to run docker program. It tells to the operating system that you are running docker program.

    2) **`run`**: This subcommand is used to create and run a docker container.

    3) **`hello-world`**: It is a name of an image. You need to specify the name of an image which is to load into the container.


## Docker Hub/ Docker Registry

- We can consider Docker Hub as a service from Docker for locating and distributing containers for each image within the specified team. It can manage the sharing and storage of Docker image.

- Docker Hub is a hosted repository service provided by Docker for finding and sharing container images with your team.

## Installing Docker

- Here we are installing a docker on Windows host having Linux vm which is Ubuntu OS. Commands used is `curl -fsSL https://get.docker.com -o get-docker.sh` and `sudo sh get-docker.sh`. 

- The installation steps will vary for Windows and macOS.

## Running a Docker command

- Running an image from Docker Hub repository having name whalesay (3)

## Docker commands

- Run command: Suppose if we run `docker run nginx` , this will run an instance of the nginx application from the docker host if it exists on the machine and if the image is not found then it will reach the docker hub to find the image and it will pull that image down in the machine ( It happens for the first time ).

- List command: 

- A. Suppose if we run `docker ps` or `docker container ls `it will list all running containers with some information about them like ID, image name, command, creation time etc. Each containers gets automatically a random ID and random name. (5)

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

- Get the image based on Tag: Suppose if we require a particular of image to be run by the container we run command `docker run imagename:versionNumber`. So the `imagename:versionNumber` is called Tag. If we don't specifiy tag docker will consider the latest tag from the docker hub.(16)

- Providing STDIN: When we a image is run by container and suppose the image is requires input, docker container simple execute the task without prompting for an input. Docker containers does not listen to STDIN even though you are attached to the terminal. Docker containers runs in a non interactive mode. 
So to provide the input to make the docker containers as a interactive mode use `docker run -i imagename`. But even providing -i as an interactive option it won't show the prompt ( like any message which ask for an input e.g Enter the user name) because the due to -i it is attach on the OS terminal and not on the container terminal. So to get that prompt for questioning use `-it`. (17)


- Inspect Container: To get more details of a container run command `docker inspect ID_or_name`. (22)

- Logs of a container: Suppose we ran a detach container and we need to view logs of it so run command `docker logs ID_or_name`. (23)



- PORT Mapping: The underlying host where docker is installed is called a docker host or docker engine. Suppose we have web server application run on a docker container , we can see the web server but how other users can access my web application? Suppose my application runs on PORT 5000 so i can access it using that port number but what IP must be use for accessing it by me? Docker provides each containers IP so using that IP or using docker host IP. But containers host IP are only accessible from docker host machine (for me) for other users we need to provide docker host IP with required particular port mapping for accessing our containerized web application. 
To get container IP `docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' container_name_or_id
`
Suppose we want to users to access our web server using port 80 and my docker host ip is 192.168.1.5 so we can do it by running port mapping command `docker run -p 80:5000 image_name`. So we can map multiple port with the provided port of the container , but we cannot use the same mapped port again for other application. 

(18 19 20 24)

Exposed ports are 3456 and 80 and publish ports are 3456 and 38080.

- Volume Mapping: Suppose we are running a mysql container and we added lost of data in that container. Suppose we stop or remove the container all the data inside that container gets destroyed. So to map those inside data of that container with outside container folder within the docker host run the command `docker run -v folderoutside:folderinsideContainer imagename`. (21) 

- Run multiple parameters using this `docker run -p 38282:8080 --name=blue-app -e APP_COLOR=blue -d kodekloud/simple-webapp`.


## Environment Variables

- Suppose there is a web-server application which uses a functionality background color. The web-server application sets that functionality as an Environment variable which state whenever we run that web-server application we can provide our own color to that environment variable and the web-page will have that background color. So here we have set environment variable as **APP_COLOR**. (25)

- Once that application is dockerized to provide that environment variable name use command `docker run -e ENVIRONMENT_VARIABLE_NAME=VALUE imagename`. (26,27)

- Inspect environment variable: Find all the environment variables of a running container using command `docker inspect CONTAINER_ID` which will have Config parameters which list all environment variables. (28)

## Docker Architecture


- Docker uses a client-server architecture. The Docker client talks to the Docker daemon, which does the heavy lifting of building, running, and distributing your Docker containers. The Docker client and daemon can run on the same system, or you can connect a Docker client to a remote Docker daemon. The Docker client and daemon communicate using a REST API, over UNIX sockets or a network interface. Another Docker client is Docker Compose, that lets you work with applications consisting of a set of containers.

The Docker daemon
The Docker daemon (dockerd) listens for Docker API requests and manages Docker objects such as images, containers, networks, and volumes. A daemon can also communicate with other daemons to manage Docker services.

The Docker client
The Docker client (docker) is the primary way that many Docker users interact with Docker. When you use commands such as docker run, the client sends these commands to dockerd, which carries them out. The docker command uses the Docker API. The Docker client can communicate with more than one daemon.

Docker registries
A Docker registry stores Docker images. Docker Hub is a public registry that anyone can use, and Docker is configured to look for images on Docker Hub by default. You can even run your own private registry.

When you use the docker pull or docker run commands, the required images are pulled from your configured registry. When you use the docker push command, your image is pushed to your configured registry.

Docker objects
When you use Docker, you are creating and using images, containers, networks, volumes, plugins, and other objects.


## Docker Images

### Creating an Image of n application 

- Here we are containerize an application a simple web application based on flask.

- Before creating an image list down all requirements and steps for deploying an application. (29)

- After listing down all the steps create a file name **Dockerfile** which is our image. After writting the dockerfile we need to build it and provide it a tag. So use command `docker build Dockerfile -t DockerHubUsername/provideImageName`. Syntax `docker build  -t ImageName:TagName directory`

- To make is available we need to push that build file. So run the command `docker push DockerHubUsername/provideImageName`. (30)

- Check about image using `docker inspect imagename`.

- Check which OS does the downloaded images used docker run python:3.6 cat /etc/*release*

- suppose if a latest version is huge in size we can use its previous version which has less size.

### Components of Dockerfile

- Dockerfile consits of two components 1. Instruction and 2. Argument

- Instruction are **FROM , RUN , COPY , ENTRYPOINT** (31). Each of them perform specific action while creating an image. 

- Arguments are the (32) text provided by users. 

- Every dockerfile will have an image based on OS and it will always start **FROM** instruction. The **RUN** instructions tells docker to install all dependencies (33). The **COPY** instruction copies the local files to the docker image. So here we are copying all the files *.* to inside of image folder */opt/source-code*. The **ENTRYPOINT** instruction allow us to specify a command that will be run when the image is run by the container.

### Images Layered architecture

- When docker builds an image it creates multiple layers. Each line of instructions creates a new layer in the Docker image taking the changes of the previous layers.

- Each layers stores the changes from the previous layer, it is reflected in the size. We can see this layers and information by running the command `docker history DockerHubUsername/provideImageName`. (34)

- We can see various steps involved when we run a docker build command.(35)

- All the layers are cached and if we one layers fails all layers after it does not get executed. After fixing the failure layer, when we run the docker build command it will directly starts from that layer where it fails. Even if we add a new layer in the dockerfile it will not start all over again. (36) Due to this images are build at a faster rate. This is helpful when there is an update in the source code of an application.

- The layers of image are called docker image layers. We cannot edit these layers once the build is completed  which is always in the Read-mode. When we run a container based off that particular image, docker creates a container layer on top of that image layers which is a read-write layer. This container layer stores all the data related to that particular container e.g logs, temp files etc. The life of this container layer is as long as the container is alive. When the container is destroyed all the stored data changes gets destroyed. (46).

- Suppose a code is used in the image and that image is used by multiple containers and if we want to modify that image for testing purpose it might affect all the containers. So to test our requirement with the source code file we can logged into one container and modify that code file for that particular container only and check our testing. Docker creates copy of that source code file and present it in the container layer where we have read-write access. So the images is not affected. (47)

- Now the source code file change is stored in the container layer and it will be there as long as container is alive. So to persist our changes we can add volumes to the containers. *( Refer the storage section )*


### CMD vs ENTRYPOINT

- Containers are mean to an instance of a web servers or application or database or compute or perform analysis. They are not mean to host an OS. Once the task is complete the containers exits it only lives as long as the process inside ID is alive. Now if we see the the actual image of UBUNTU , there is CMD ["Bash"] which the command to run the container. Now BASH is not a process or a web server its a terminal which listen the inputs from it and display the outputs. So when we run `docker run ubuntu` the image search for BASH terminal which is not attach to the container by the docker and therefore the container exits. So here we can override that command by provide our own sets of command e.g `docker run ubuntu sleep 5` so our CMD provided is **sleep 5** which overides the CMD["Bash"] command. (37)

- How to make it permanent lets say whenever we run the ubuntu image , it must execute the sleep command. So we create our own image e.g **ubuntu-sleeper** and mentioned the command in it. (38) To write the command we need to follow the syntax
**`CMD command command_parameters`** OR **`CMD ["command","command_parameters"]`**.

- Suppose we need to override our **ubuntu-sleeper** image with command sleep 10. But instead of again mentioning the sleep command can we provide the seconds time parameter? providing custom time?. Here we can use the **ENTRYPOINT** instead of command. (39).

- Suppose if the users don't provide the operand required to run the command we need to add our default operand. We need to use both **ENTRYPOINT** and **CMD**. So if i don't specify parameter in the ENTRYPOINT it will take the default parameter from cmd (40). Both must be in JSON format.

- So in **CMD** instruction , command line parameters passed will be override entirely whereas in case of **ENTRYPOINT** the command line parameters will get appended.

## Network

- When we install docker, it creates 3 defaults networks automatically. Bridge,None and Host.

- If we want to attach any of the network specify it while running the docker command. (41)

- Bridge is the default network which gets attached to the containers. All the containers gets an internally IP which usually ranges 172.17.. series. The containers can access each other using this internal IP's.

- Host network is the network of the Docker Host. So whenever we want to access container externally we map this to the host network port. So when we run a web server on a host port it will be automatically accessible on the host port but we won't able to run multiple containers on the same port.

- With the none network , containers are not attach to any network and does not have any access to the external network or any other containers. They run in an isolated network.
(42)

- Docker crates one internal network bridge , so to have multiple internal network bridge using the command (43)

- By using the inspect command, we can check which type of network is assign to the container.(44)

- `docker network ls` command list all network on the host.

- We can inspect network also. `docker network inspect bridge`

- Whenever the system gets reboot , its not sure the container will have the same IP ID.

- `docker run --name alpine-2 --network none alpine`

## Docker Storage system

- Docker stores the data on the local file system. When we install docker , it creates a folder structure */var/lib/Docker* (Linux) , *C:\ProgramData\DockerDesktop* (Windows) and *~/Library/Containers/com.docker.docker/Data/vms/0/* (MacOS).

- Under these there are multiple folders. Under this multiple folders docker manages the files system for images and containers. All the images are stored under image folders.(45)

- Volumes are used to persist the data of the container. So first we need to create a volume for that container by running command `docker volume create volume_nameforthat_container`. This will create volume_nameforthat_container folder under volume folder. We need to mount this volume on the container by running the command `docker run -v volume_nameforthat_container:directory_of_image_wheredataispresent imagename`. These gets stored under the docker host. If we don't run the command `docker volume create volume_nameforthat_container` and run the command `docker run -v volume_nameforthat_container:directory_of_image_wheredataispresent imagename` it will automatically create the volume and mount it on that container. (48). This is called volume mounting.

- Suppose we want to mount the data in an external directory under docker host by not creating volume under docker host, we can do this by running the command `docker run -v external_complete_directory_underdockerhost:directory_of_image_wheredataispresent imagename`. This is called Bind mounting. (49)

- The new way to mount the volumes on the container.(50)

- Docker uses storage drivers to enable the layer architecture of images and perfoming mount operations. The common storage drivers are belows. Storage driver depends on OS. Overlays2 for Ubuntu. (51)

## Docker Compose

- When an application uses multiple images and those images needs to be connected with each other use use a docker-compose.yml file to perform this. Using docker compose we can create a configuration file in YAML format and put together different services and option specific to this to run them. This is applicable on single docker host. (52) 

- Sample application - voting appplication. The voting-app is a simple application which provides user interface to vote which is developed in python. In memory DB, when the user makes selection the vote is stored in the redis. The provided vote is process by worker which is an application written in .NET .The worker application takes the new vote and update the data base which is in PostgreSQL. This SQL has tables which is simply the category. Finally the result is displayed in result-app which is web application based on NodeJS. (53)

- Now all the images for the voting application are build now we are running each containers seperately. Now to link these application which each other we use a parameter `--link` (which will be deprecated). (54). Link can be use to link multiple container. (55 56) 

- So we can use all the command and create a docker-compose file. After writing the docker-compose.yml file we run the file using `docker-compose up`. (57)

- To build an image we can use build key. (58)

- Different version of docker compose file.(59)

## Docker registry (Docker Hub)

- Whenever we run a docker command `docker run imagename` it first find if the image is present locally if not then pull that image from docker registry. 

- The complete naming format is like **imagename(Username)/Imagename(Repositoryname)**. If we don't provide username docker by default assume the repository name as username. (60)

- The registry repository can be public or private. To use an image of private repository first we need to login using commands.(61)

- In organization suppose we want to deploy the image by not making it private and not accessible to all. We can do this by using tag. (62)


## Orchestration

- Container Orchestration is a solution which consists sets of tools and scripts that can help docker host containers to have multiple docker host that host 1000's of containers so even if one host fails the application will be still accessible due to other containers.

- Container Orchestration helps to deploy all the instance on multiple host using single command based on docker swarm. Due to Orchestration we can scale up or down the load and can increase or decrease the load based on the traffic.










