Software development before and after docker
- What and why of docker.
  -   Docker is a virtualization software
  -   Makes developing and deploying applications easy
  -     
###### Docker vs Virtual machines.
- Overview:  OS is made up of Applications layer and Kernel layer
- Docker containers virtualize the OS Applications layer. Docker contains the Applications layer of the Operating System and the services and apps that are installed on top of that layer. Docker has no information of the kernel and the intention here is that docker will use the OS kernel of the targetted host.
- Virtual machines images on the other hand, contain both the OS application layer, and the kernel layer that would run as a part of it on a target host. 

Development process before docker 
------------------------------------
-  Each developer needs to configure and install all services directly on their OS
  -  Installation process different for each OS environment.
  -  Many steps involved ... so something can go wrong.
  -    

Development process after docker 
------------------------------------
- Docker exports its own environment
- Single docker command will start all dependencies including dependent services and configurations for the package.
- All of the above is acheived in a single command.
- Command is same for all OS &&.
- Command same for all services.\

  In Conclusion docker standardizes process of running any service on any local dev environment. Thereby making it easier and faster to setup the local development environment.

  ###### Deployment Process before containers
  - Developer will generate an artifact (package) with a set of instructions and hand over to Ops team.
  - Ops team thereafter will install and configure the application and services.  
   
   ###### Deployment Process after containers
  - Developer creates a package that includes code, dependencies and configuration i.e. this artifact, the docker artifact  includes everything the app needs.
  - All the information is encapsulated into docker artifact.
  - Ops team hereafter runs a docker command that will fetch and run the docker artifacts. So the only prerequisite is that docker runtime is running on the server.
 

Installing docker locally 
----------------------------
Docker is an improvement over virtual machines
 - Images vs containers.
    - Most of the popular containers are Linux based.
    - Docker was originally built for Linux.
    - More recently there is a Docker Desktop that runs on Windows and Mac.

            
 - public and private registries.
 - Create own image (dockerfile)

Installing docker on a centos based virtual machine.\
sudo dnf install podman.\ 

CLI of docker \
------------
###### Pull an Image:\

podman pull ubuntu:latest\

###### Run a Container:

podman run -it ubuntu:latest
###### List Running Containers:

###### podman ps
Stop a Container:

###### podman stop <container_id>

**Container Registry**: This is a repository where container images are stored. Popular registries include Docker Hub, Quay.io, and Google Container Registry.

**Image:** An image is a lightweight, standalone, and executable software package that includes everything needed to run a piece of software.

**Pull Command:** When you use the podman pull command, Podman contacts the specified container registry, downloads the image, and stores it locally on your machine. For example:

Resources 
==========
