Software development before and after docker
- What and why of docker.
  -   Docker is a virtualization software
  -   Makes developing and deploying applications easy
  -     
- Docker vs Virtual machines.

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
- Command same for all services.











Installing docker locally 
----------------------------
Docker is an improvement over virtual machines
 - Images vs containers.
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
