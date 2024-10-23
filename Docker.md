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
    
<summary>What are containers?</summary>

1. A container is a standard unit of software that packages up code and all its dependencies, so the application runs quickly and reliably from one computing environment to another.
        
2. A Docker container image is a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system tools, system libraries and settings.

3. Containers are lightweight and contain everything needed to run the application, so you do not need to rely on what is currently installed on the host. You can easily share containers while you work, and be sure that everyone you share with gets the same container that works in the same way.
        
        
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

- <h3>Images:</h3>

   - Images are read-only templates containing instructions for creating a container. A Docker image creates containers to run on the Docker platform. Think of an image like a blueprint or snapshot of what will be in a container when it runs. Images are built as a series of layers. Layers are assembled on top of one another. 

    - Let's say we want to create a Docker image of a Hello World Java application. The first thing we need to think about is what does our application need. Firstly it is a Java application, so we will need a JVM. OK, this seems easy, but what does a JVM need to run? It needs an Operating System. Therefore, our Docker image will have an Operating System layer, a JVM, and then our Hello World application.

    - A major advantage of Docker is its large community. If we want to build an image, we can go to Docker Hub and search if the image we need is available.

- <h3>Containers:</h3>

    - A container is an instance of an image. Each container can be identified by its ID or by a unique name. Going back to our Java development analogy, we could say that a container is like an instance (*object*) of a class. So images is a class and container is an object or instance of that class.

    - Docker defines 7 states for a container:

        1. Created

        2. Restarting
        
        3. Running
        
        4. Removing
        
        5. Paused
        
        6. Exited
        
        7. Dead. 

    - A container is just an instance of the image, it doesn't need to be running all time.

- For an example, in docker if run command, **`docker run hello-world`**  

    1) **`docker`**: It is docker engine and used to run docker program. It tells to the operating system that you are running docker program.

    2) **`run`**: This sub-command is used to create and run a docker container.

    3) **`hello-world`**: It is a name of an image. You need to specify the name of an image which is to load into the container.


## Docker Hub/ Docker Registry

- We can consider Docker Hub as a service from Docker for locating and distributing containers for each image within the specified team. It can manage the sharing and storage of Docker image.

- Docker Hub is a hosted repository service provided by Docker for finding and sharing container images with your team.

## Installing Docker

- Here we are installing a docker on Windows host having Linux vm which is Ubuntu OS. Commands used is `curl -fsSL https://get.docker.com -o get-docker.sh` and `sudo sh get-docker.sh`. 

- The installation steps will vary for Windows and macOS.

## Running a Docker command

- Running an image from Docker Hub repository having name **whalesay**.

![](https://github.com/codophilic/LearnDocker/blob/main/Docker/3.PNG)

## Docker commands

- <h3>Run containers:</h3> 

    - Suppose if we run `docker run nginx`, this will run an instance of the nginx application from the docker host (*if it exists on the machine*) and if the image is not found then it will reach the docker hub to find the image, and it will pull that image down in the machine (*it happens for the first time*).

    ![](https://github.com/codophilic/LearnDocker/blob/main/Docker/4.PNG)

    - Run a container with provided name using command `docker run --name=container_name imagename`. 

- <h3>List command:</h3> 

    - **Containers:** Suppose if we run `docker ps` or `docker container ls ` it will list all running containers with some information about them like ID, using which image name, command, creation time etc. All containers get automatically a random ID and random name.

    ![](https://github.com/codophilic/LearnDocker/blob/main/Docker/5.PNG)

    - **Images:** Suppose we want to list images run command `docker images`.
    
    ![](https://github.com/codophilic/LearnDocker/blob/main/Docker/8.PNG)


- <h3>Stop Command:</h3>
    - Suppose if we want to stop a container, we need to have its ID or name e.g `docker stop sleepy_diffie` OR `docker stop container_ID`.

    ![](https://github.com/codophilic/LearnDocker/blob/main/Docker/6.PNG)

- <h3>Remove command:</h3> 

    - **Containers:** Suppose we want to remove containers permanently which takes up spaces we can run `docker rm ID`. We cannot remove running containers in docker.

    ![](https://github.com/codophilic/LearnDocker/blob/main/Docker/7.PNG)

    - **Images:** Suppose we want to remove an image permanently run command `docker rmi image_name`. Before deleting an image we need to be sure that no containers are running off to that image.

    ![](https://github.com/codophilic/LearnDocker/blob/main/Docker/9.PNG)
    ![](https://github.com/codophilic/LearnDocker/blob/main/Docker/10.PNG)

    - To remove all containers use command `docker rm $(docker ps -aq)`.

    - To remove all images `docker rmi $(docker images -q)`.

- <h3>Pull Command:</h3>

    - We can just pull the image to store it on the host and not run the container. Command is `docker pull imagename`.

    ![](https://github.com/codophilic/LearnDocker/blob/main/Docker/11.PNG)

- <h3>Containers lifespan:</h3> 

    - Containers are not meant to host an OS they are meant to run a specific task or process such as to host an instance of an image. Once the task is completed the container exits. 
    
    - A container only lives as long as the process inside it is alive. If the service inside the container is stopped or crash, then the container exits. You can refer the example whalesay image where the docker container after completion exited itself.

- <h3>Execute command:</h3>

    - Suppose we want to run execute some commands on running containers we can do it using command `docker exec container_name COMMAND`. 
    
    - Consider an example, when we run `docker run ubuntu`, the container gets exited immediately. We can use a `sleep` command over it. Basically a command sent to the container to override its image default command and execute with the command provided.

    ![](https://github.com/codophilic/LearnDocker/blob/main/Docker/12.PNG)

- <h3>Attach and Detach:</h3>

    - A container which uses an image that runs on CLI/ foreground like running a web server it called an **ATTACH** state. This makes difficult to add any inputs to the docker containers.

    ![](https://github.com/codophilic/LearnDocker/blob/main/Docker/13.PNG)
    
    - Docker provides to run such images in the background like a **DETACH** state. The container will  continue to run in the backend. 

    ![](https://github.com/codophilic/LearnDocker/blob/main/Docker/14.PNG)

    - In the Detach state the docker provides an ID which can be used to attach it again. It is always suggested to run a container in detach state.

    ![](https://github.com/codophilic/LearnDocker/blob/main/Docker/15.PNG)


- <h3>Get the image based on Tag:</h3>

    - Suppose we require a particular version of image to be run by the container, we run command `docker run imagename:versionNumber`. So the **`imagename:versionNumber`** is called **Tag**. If we don't specify tag docker will consider the latest tag from the docker hub.

    ![](https://github.com/codophilic/LearnDocker/blob/main/Docker/16.PNG)

- <h3>Providing STDIN:</h3> 

    - When an image is run by container and suppose the image requires some input, docker container simple execute the task without prompting for an input. Docker containers do not listen to STDIN even though you are attached to the terminal. 

    - Docker containers run in a non-interactive mode. 

    - So to provide the input to make the docker containers as an interactive mode use `docker run -i imagename`. But sometimes even providing **-i** as an interactive option it won't show the prompt (like any message which ask for an input e.g. Enter the username) because the due to **-i** it is attach on the OS terminal and not on the container terminal. So to get that prompt for questioning use **`-it`**. 

    ![](https://github.com/codophilic/LearnDocker/blob/main/Docker/17.PNG)


- <h3>Inspect Container:</h3> 

    - To get more details of a container or image run command `docker inspect container_ID/Imagename`. 

    ![](https://github.com/codophilic/LearnDocker/blob/main/Docker/22.PNG)

- <h3>Logs of a container:</h3>

    - Suppose we ran container in detach state, and we need to view logs of it so run command `docker logs ID_or_name`. 

    ![](https://github.com/codophilic/LearnDocker/blob/main/Docker/23.PNG)


- <h3>PORT Mapping:</h3> 

    - The underlying host where docker is installed is called a docker host or docker engine. 
    
    - Suppose we have web server application run on a docker container, we can see the web server but how other users can access that web application? Suppose that web application runs on PORT 5000, so I can access it using that port number but what IP must be use for accessing it by me?
    
    - Docker provides each container's an IP. Using that IP or using docker host IP only the host machine user can access it. Since containers host IP are only accessible from docker host machine (for me), so for other users we need to provide docker host IP with required particular port mapping for accessing our containerized web application. 

    - To get container IP `docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}container_name_or_id`.
    
    - Suppose we want users to access our web server using port 80 and my docker host IP is 192.168.1.5, so we can do it by running port mapping command `docker run -p ProvidedPort:DefaultPort image_name`. So we can map multiple port with the provided port of the container, but we cannot use the same mapped port again for other application. 

    ![](https://github.com/codophilic/LearnDocker/blob/main/Docker/18.PNG)
    ![](https://github.com/codophilic/LearnDocker/blob/main/Docker/19.PNG)
    ![](https://github.com/codophilic/LearnDocker/blob/main/Docker/20.jpg)

    - Considering below example here the exposed ports are 3456 and 80 and publish ports are 3456 and 38080.

    ![](https://github.com/codophilic/LearnDocker/blob/main/Docker/24.PNG)

- <h3>Volume Mapping:</h3>

    - Suppose we are running a mysql container and we added lost of data in that container. Suppose we stop or remove the container all the data inside that container gets destroyed. So to map those inside data of that container with outside container folder within the docker host run the command `docker run -v folderoutside:folderinsideContainer imagename`. 

    ![](https://github.com/codophilic/LearnDocker/blob/main/Docker/21.jpg)

- <h3> Run multiple parameters in docker command</h3>

    - To run multiple parameters in docker command we can reference this command `docker run -p 38282:8080 --name=blue-app -e APP_COLOR=blue -d kodekloud/simple-webapp`.


## Environment Variables

- Suppose there is a web-server application which uses a functionality for background color of the web page. The web-server application sets that functionality as an **environment variable** which state whenever we run that web-server application we can provide our own color to that environment variable and the web-page will have that background color. So here, we provide the value to that environment variable as **APP_COLOR**. 

![](https://github.com/codophilic/LearnDocker/blob/main/Docker/25.jpg)

- To provide that environment variable name use command `docker run -e ENVIRONMENT_VARIABLE_NAME=VALUE imagename`. 

![](https://github.com/codophilic/LearnDocker/blob/main/Docker/26.jpg)
![](https://github.com/codophilic/LearnDocker/blob/main/Docker/27.jpg)

- <h3>Inspect environment variable:</h3> 

    - Find all the environment variables of a running container using command `docker inspect CONTAINER_ID` which will have Config parameters which list all environment variables. 

    ![](https://github.com/codophilic/LearnDocker/blob/main/Docker/28.jpg)

## Docker Architecture


- Docker uses a client-server architecture. The Docker client talks to the Docker daemon, which does the heavy lifting of building, running, and distributing your Docker containers. The Docker client and daemon can run on the same system, or you can connect a Docker client to a remote Docker daemon. The Docker client and daemon communicate using a REST API, over UNIX sockets or a network interface. Another Docker client is Docker Compose, that lets you work with applications consisting of a set of containers.

![](https://github.com/codophilic/LearnDocker/blob/main/Docker/archi.JPG)

- <h3>The Docker daemon</h3>
    
    - The Docker daemon (dockerd) listens for Docker API requests and manages Docker objects such as images, containers, networks, and volumes. A daemon can also communicate with other daemons to manage Docker services.

- <h3>The Docker client</h3>

    - The Docker client (docker) is the primary way that many Docker users interact with Docker. When you use commands such as docker run, the client sends these commands to **dockerd**, which carries them out. The docker command uses the Docker API. The Docker client can communicate with more than one daemon.

- <h3>Docker registries</h3>

    - A Docker registry stores Docker images. Docker Hub is a public registry that anyone can use, and Docker is configured to look for images on Docker Hub by default. You can even run your own private registry.
    
    - When you use the docker pull or docker run commands, the required images are pulled from your configured registry. When you use the docker push command, your image is pushed to your configured registry.

- <h3> Docker objects </h3>

    - When you use Docker, you are creating and using images, containers, networks, volumes, plugins, and other objects.


## Docker Images

### Steps to create an Image 

- Here we are containerizing a simple web application based on flask.

- Before creating an image list down all requirements and steps for deploying an application.

![](https://github.com/codophilic/LearnDocker/blob/main/Docker/29.jpg)

- After listing down all the steps, create a file name **Dockerfile** which is our image. After writing the **Dockerfile** we need to build it and provide it a tag. So use command `docker build Dockerfile -t DockerHubUsername/provideImageName`. Syntax `docker build  -t ImageName:TagName directory`

- To make is available we need to push that build file. So run the command `docker push DockerHubUsername/provideImageName`.

![](https://github.com/codophilic/LearnDocker/blob/main/Docker/30.jpg)

- Check about image using `docker inspect imagename`.

- To check which OS does the downloaded images used run command `docker run imagename cat /etc/*release*`

- Suppose if latest version is huge we can use its previous version which has less size.

### Components of Dockerfile Image

- Dockerfile consists of two components 
    1. Instruction 
    2. Argument

- Instruction are **FROM** ,**RUN** ,**COPY** ,**ENTRYPOINT**. Each of them perform specific action while creating an image. 

![](https://github.com/codophilic/LearnDocker/blob/main/Docker/31.jpg)

- Arguments are the text provided by users. 

![](https://github.com/codophilic/LearnDocker/blob/main/Docker/32.jpg)

- Every **Dockerfile** will have an image based on OS, and it will always start **FROM** instruction. The **RUN** instructions tell docker to install all dependencies. The **COPY** instruction copies the local files to the docker image. So here we are copying all the files ***.*** to inside of image folder */opt/source-code*. The **ENTRYPOINT** instruction allow us to specify a command that will be run when the image is run by the container.

![](https://github.com/codophilic/LearnDocker/blob/main/Docker/33.jpg)

### Images Layered architecture

- When docker builds an image it creates multiple layers. Each line of instructions creates a new layer in the Docker image taking the changes of the previous layers.

- Each of the layers stores the changes from the previous layer, it is reflected in the size. We can see these layers and information by running the command `docker history DockerHubUsername/provideImageName`.

![](https://github.com/codophilic/LearnDocker/blob/main/Docker/34.jpg)

- We can see various steps involved when we run a docker build command.

![](https://github.com/codophilic/LearnDocker/blob/main/Docker/35.jpg)

- All the layers are cached and if we one layers fails all layers after it does not get executed. After fixing the failure layer, when we run the docker build command it will directly start from that layer where it fails. Even if we add a new layer in the **Dockerfile** it will not start all over again. Due to such processing of an images build take place at a faster rate. This is helpful when there is an update in the source code of an application.

![](https://github.com/codophilic/LearnDocker/blob/main/Docker/36.jpg)

- The layers of image are called docker image layers. We cannot edit these layers once the build is completed which is always in the **Read-mode**. When we run a container based off that particular image, docker creates a container layer on top of that image layers which is a **read-write** layer. This container layer stores all the data related to that particular container e.g. logs, temp files etc. The life of this container layer is as long as the container is alive. When the container is destroyed all the stored data changes gets destroyed.

![](https://github.com/codophilic/LearnDocker/blob/main/Docker/46.jpg)

- Suppose a code is used in the image and that image is used by multiple containers and if we want to modify that image for testing purpose it might affect all the containers. So to test our requirement with the source code file we can log into one container and modify that code file for that particular container only and check our testing. Docker creates copy of that source code file and present it in the container layer where we have read-write access. So the images is not affected.

![](https://github.com/codophilic/LearnDocker/blob/main/Docker/47.jpg)

- Now the source code file change is stored in the container layer, and it will be there as long as container is alive. So to persist our changes we can add volumes to the containers. [*Refer the storage section*](#docker-storage-system)


### CMD vs ENTRYPOINT

- Containers are mean to run an instance of a web server or application or database or compute or perform analysis. They are not mean to host an OS. Once the task is complete the containers exits it only lives as long as the process inside ID is alive. 

- Now if we see the actual image of UBUNTU, there is **CMD ["Bash"]** which is the command to run the container. Now BASH is not a process or a web server it's a terminal which listen the inputs from it and display the outputs. 

- So when we run `docker run ubuntu` the image search for BASH terminal which is not attached to the container by the docker and therefore the container exits. So here we can override that command by provide our own sets of command e.g. `docker run ubuntu sleep 5` so our CMD provided is **sleep 5** which overrides the **CMD["Bash"]** command.

![](https://github.com/codophilic/LearnDocker/blob/main/Docker/37.jpg)

- How to make it permanent lets say whenever we run the ubuntu image, it must execute the sleep command. So we create our own image e.g. **ubuntu-sleeper** and mentioned the command in it. To write the command we need to follow the syntax
**`CMD command command_parameters`** OR **`CMD ["command","command_parameters"]`**.

![](https://github.com/codophilic/LearnDocker/blob/main/Docker/38.jpg)

- Suppose we need to override our **ubuntu-sleeper** image with command sleep 10. But instead of again mentioning the sleep command can we provide the seconds time as an operand parameter? Providing custom time?. Here we can use the **ENTRYPOINT** instead of command.

![](https://github.com/codophilic/LearnDocker/blob/main/Docker/39.jpg)

- Suppose if the users don't provide the operand required to run the command we need to add our default operand. We need to use both **ENTRYPOINT** and **CMD**. So if user don't specify parameter in the ENTRYPOINT it will take the default parameter from cmd. Both must be in JSON format.

![](https://github.com/codophilic/LearnDocker/blob/main/Docker/40.jpg)

- So in **CMD** instruction, command line parameters passed will be overridden entirely whereas in case of **ENTRYPOINT** the command line parameters will get appended.

## Docker Network

- When we install docker, it creates 3 defaults networks automatically. 
    1. Bridge
    2. None
    3. Host

- If we want to attach any of the network specify it while running the docker command `docker run --network=network_name Imagename`.

![](https://github.com/codophilic/LearnDocker/blob/main/Docker/41.jpg)

- **Bridge is the default network** which gets attached to the containers. All the containers gets an internal IP which usually ranges 172.17.... series. The containers can access each other using this internal IP's.

- Host network is the network of the Docker Host. So whenever we want to access container externally we map this to the host network port. When we run a web server on a host port it will be automatically accessible on the host port, but we won't able to run multiple containers on the same port.

- With the none network, containers are not attached to any network and does not have any access to the external network or any other containers. They run in an isolated network.

![](https://github.com/codophilic/LearnDocker/blob/main/Docker/42.jpg)

- Docker creates one internal network bridge, so to have multiple internal network bridge using the command.

![](https://github.com/codophilic/LearnDocker/blob/main/Docker/43.jpg)

- By using the inspect command, we can check which type of network is assign to the container. **Command:  `docker network inspect bridge`**

![](https://github.com/codophilic/LearnDocker/blob/main/Docker/44.jpg)

- `docker network ls` command list all network on the host.

- Whenever the system gets reboot, it's not sure the container will have the same IP ID.


## Docker Storage system

- Docker stores the data on the local file system. When we install docker, it creates a folder structure */var/lib/Docker* (Linux), *C:\ProgramData\DockerDesktop* (Windows) and *~/Library/Containers/com.docker.docker/Data/vms/0/* (macOS).

- Under these there are multiple folders. Under this multiple folder's docker manages the file's system for images and containers. All the images are stored under image folders.

![](https://github.com/codophilic/LearnDocker/blob/main/Docker/45.JPG)

- Volumes are used to persist the data of the container. So first we need to create a volume for that container by running command `docker volume create volume_nameforthat_container`. This will create *volume_nameforthat_container* folder under *volume* folder. We need to mount this volume on the container by running the command `docker run -v volume_nameforthat_container:directory_of_image_wheredataispresent imagename`. These gets stored under the docker host. If we don't run the command `docker volume create volume_nameforthat_container` and run the command `docker run -v volume_nameforthat_container:directory_of_image_wheredataispresent imagename` it will automatically create the volume and mount it on that container. This is called volume mounting.

![](https://github.com/codophilic/LearnDocker/blob/main/Docker/48.jpg)

- Suppose we want to mount the data in an external directory under docker host by not creating volume under docker host, we can do this by running the command `docker run -v external_complete_directory_underdockerhost:directory_of_image_wheredataispresent imagename`. This is called Bind mounting. 

![](https://github.com/codophilic/LearnDocker/blob/main/Docker/49.jpg)

- The new way to mount the volumes on the container.

![](https://github.com/codophilic/LearnDocker/blob/main/Docker/50.jpg)

- Docker uses storage drivers to enable the layer architecture of images and performing mount operations. The common storage drivers are below. Storage driver depends on OS. Overlays2 for Ubuntu.

![](https://github.com/codophilic/LearnDocker/blob/main/Docker/51.jpg)

## Docker Compose

- When an application uses multiple images and those images needs to be connected with each other use a **docker-compose.yml** file to perform this. Using docker compose we can create a configuration file in YAML format and put together different services and provide options specific to this to run them. This is applicable on single docker host. 

![](https://github.com/codophilic/LearnDocker/blob/main/Docker/52.jpg)

- Considering a sample application - voting application. The voting-app is a simple application which provides user interface to vote which is developed in python. In memory DB, when the user makes selection the vote is stored in the Redis. The provided vote is process by worker which is an application written in .NET. The worker application takes the new vote and update the database which is in PostgreSQL. This SQL has tables which is simply the category. Finally, the result is displayed in result-app which is web application based on NodeJS. 

![](https://github.com/codophilic/LearnDocker/blob/main/Docker/53.jpg)

- Now all the images for the voting application are build now we are running each container separately. Now to link this application which each other we use a parameter `--link` (which will be deprecated).

![](https://github.com/codophilic/LearnDocker/blob/main/Docker/54.jpg)

- Link can be used to link multiple container. 

![](https://github.com/codophilic/LearnDocker/blob/main/Docker/55.jpg)

- So we can use all the command and create a docker-compose file. After writing the **docker-compose.yml** file we run the file using `docker-compose up`.

- To build an image we can use build key.

![](https://github.com/codophilic/LearnDocker/blob/main/Docker/56.jpg)

- Different version of docker compose file.

![](https://github.com/codophilic/LearnDocker/blob/main/Docker/57.jpg)

## Docker registry (Docker Hub)

- Whenever we run a docker command `docker run imagename` it first find if the image is present locally if not then pull that image from docker registry. 

- The complete naming format is like **imagename(Username)/Imagename(Repositoryname)**. If we don't provide username docker by default assume the repository name as username. 

![](https://github.com/codophilic/LearnDocker/blob/main/Docker/58.jpg)

- The registry repository can be public or private. To use an image of private repository first we need to log in using commands.

![](https://github.com/codophilic/LearnDocker/blob/main/Docker/59.jpg)

- In organization suppose we want to deploy the image by not making it private and not accessible to all. We can do this by using tag.

![](https://github.com/codophilic/LearnDocker/blob/main/Docker/60.jpg)


## Orchestration

- Container Orchestration is a solution which consists sets of tools and scripts that can help docker host containers to have multiple docker host that host 1000s of containers so even if one host fails the application will be still accessible due to other containers.

- Container Orchestration helps to deploy all the instance on multiple host using single command based on docker swarm. Due to Orchestration we can scale up or down the load and can increase or decrease the load based on the traffic.










