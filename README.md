#### Docker 
* Its a containerization platform 
* Using docker we can Build ,ship,run our applications as a containers.


#### What is Docker Machine?
A tool that allow you to install docker engine on virtual hosts and these hosts can be managed by   docker-machine commands.

#### Container 
* container contains everything (Softwar + AppCode + Libraries + configurations Env ..etc , anything that can be installed on a server).which is required to run a application
- EXample : BaseImage(Ubuntu/tomcat/nodejs) + configurationes & Dependencies(softwares) + Application

#### Features of Docker
- Easy Configuration
- Improved Software Delivery
- Application Isolation
- Quick scaling of Systems
- Security Management
- Version control
- Software-defined Networking
- Improved Developer Productivity
- Operational Efficiencies
- Container are light weight 
- It requires less resources (Cpu,Memory).
- container are fast
- container are Isolated 
- container are portable

#### Containerization softwares/Runtime/Platforms
* Docker 
* container-D 
* PodMan
* Rocket(rkt)
* CRI-O


#### Docker Registry ?
* Registry is a central storage (server) where we can create reposities to store/maintainer docker images .
* Registry is  collection of one or more repostries
#####  Ex : 
* Nexus
* JFrog
* DockerHub
* ECR --  elstic container Registry
* GCR --  google container registry
* ACR --  Azur conatiner Registry

#### Docker Repositry ?
* Repositry is collection of one or more versions(tags) of your images of same application type.
    Example :  Docker Hub(Registry)

#### Docker Architecture
* Explain the main components of Docker.
* Docker Client 
    -   is CLI through which user send the command/ instructions to docker 
    -   It helps users to interact with Docker. The client offers a command-line interface (CLI), 
allowing users to give create, run, and stop application commands to a Docker daemon. The client can be on the same host as the daemon. 
    -   It can also connect to a daemon on a remote host. A client can interact with more than one daemon.
* Docker Daemon &  Docker Host: 
    -   Daemon will executed the commands sent by the user.
    -   command may be installing os or pull images from registry or running a container .,etc.
    -   It provides a complete environment to run applications. It is comprised of Docker daemon, containers, networks, storage, and images. 
* Docker Registry
    -   Registry is a central storage (server) where we can create reposities to store/maintainer docker images .
    -   This is the location where you can store and download Docker images. There are two types of registries, 
a public registry and a private registry. Docker Hub is the default location of docker images.


<img width="746" alt="image" src="https://github.com/user-attachments/assets/f779c3b3-6dd9-4741-a41a-c1ae9e7294af">

#### Docker File
* A DockerFile is a text document with all commands that need to be run to build an image. In simpler terms, a Dockerfile refers to the build instructions to build the image. The instructions will execute in the order in which they are written.
    - Dockerfile is a file, it will describe the steps in order to create an image
quickly.
    - The Docker daemon runs the instructions in the Dockerfile are processed
from the top down, so you should order them accordingly.
    - The Dockerfile is the source code of the Docker Image.

* FROM  -   Sets the Base image for subsequent instructions
    -   Example : FROM <registry/repo:tag>
    -   FROM  Tomcat:8.5
* MAINTAINER    -   Sets the author field of the the generated images
    -   Example : MAINTAINER Pavan
* COPY  -   Copy local files/directories from build context(servers) to image (on top of previous Layers)
    -   Example :  COPY <source> <destionation>
    -   COPY /etc/webapp.jar /urs/local/tomcat/webapps/webapp.jar
* ADD   -   using add also we can copy files to image ,and ADD can copy local files/folders and also it can add remote files (like https endpoints) to images
    -   Example : 
        -   ADD <source> <destionation>
        -   ADD <sourceurl> <destionationurl>

* We can executes commands or scripts using RUN ,CMD & ENTRYPOINT
*   RUN -    RUN instructions will be executed while creating an image on top of the previous layer.
    -   Example: RUN <Command>
        -   RUN mkdir -p /opt/tomcat
        -   RUN yum install git -y

* CMD   -   CMD instruction will be executed while container is running.Allowed only once (if many, then only the last one takes effect)
    -   Example : CMD sh startup.sh
        -   CMD ["/bin/bash"]
* ENTRYPOINT    -   Allows you to configure a container that will run as an executable
* ARG   -   Defines a variable that users can pass at buildtime to the builder using buildarg
    -   EXample : ARG imagetag:latest
        -   FROM centos:$imagetage
        -   docker build -t imageone --build-arg imagetag=centos7.9.01

* LABEL     -   Adds metadata to an image
* EXPOSE    -   Informs Docker that the container listens on the specified network ports at runtime.
* ENV       -   Sets an environment variable
* VOLUME    -   Creates a mount point and marks it as holding externally mounted volumes from native host or other containers
* USER      -   Sets the user name or UID to use when running an image
* WORKDIR   -   Sets the working directory for any RUN, CMD, ENTRYPOINT, COPY, and ADD commands
* ONBUILD   -   Adds an instruction to be executed later, when the image is used as the base for another build

*   Dockerfile 
    - Example
    ``` bash
        # syntax=docker/dockerfile:1
        FROM node:18-alpine
        WORKDIR /app
        COPY . .
        RUN yarn install --production
        CMD ["node", "src/index.js"]
        EXPOSE 3000
    ```

#### Docker Commands
* Login commands :
    ``` bash
        docker login --username <Username> --passwd <password> url
        docker login -u deflow -p 
        docker login -u admin -p admin123 172.31.90.102:8083  #  In case of nexus
        docker login -u admin -p admin123 nexus.tcs.com       #  In case of nexus(domain name)
        docker login -u admin -p admin123 146866.dkr.ecr.ap-south-1.amazonaws.com # In case of Aws ECR
    ```

* Docker Image commands:
    ``` bash
        docker images -a    # List Docker Images on Computer
        docker build --tag=<IMAGE TAG NAME> --force-rm=true . # Build Docker Image 
        docker build -t <imageTag> <Buildcontext>  # To build Image
        docker build -t deflow/maven-app:1 .       # To build Image with docker file
        docker push <imagename/tag>                # TO push image into repo
        docker pull <imagename/tag>                # TO pull image from repo
        docker tag <imagesID> <registry/repo:tag>  # TO tag a image 
        # examples
        docker tag <imagesID> deflow/maven-app:laste        
        docker tag <imagesID> deflow/maven-app:laste1
        docker tag <imagesID> deflow/maven-app:laste2
        docker rmi <IMAGE ID HERE>                  # Remove Docker Image
        docker rmi -f <IMAGE ID HERE>               # Remove Docker Image
        docker rmi $(docker images -f dangling=true) # Remove All Docker Images on Computer
        docker images -f dangling=true               # to see untag images
        docker image inspect <ImageID/name>          # Information about image
        docker inspect --format '{{.state.status}}' <containerName> # inspect with particular format
        docker history  <imageID/name>               # to see layers of images
        docker rmi $(docker images -a)               # To delete all images 
        docker rmi -f $(docker images -a -f dangling=true)   # TO delete dangling images
        docker search <imagename>                     # it will search in registry
        docker save <imageName> -0 <fileName>.tar     # to save image 
        docker load -i <fileName>.tar                 # to load image
    ```


#### What is the use of the docker save and docker load commands?
    - A Docker image can be exported as an archive via the docker save command. For example:
    ``` bash
        docker save -o <container-export-path>.tar <container-name>
    ```
    - The exported Docker image can then be imported to another Docker host via the docker load command:
    ```bash
        docker load -i <container-path>.tar
    ```
* Note that this does not export data from any containers that were based on the image, just the image itself.


#### Describe the lifecycle of Docker Container?
*    The most important stages are:
    - Created: This is the state where the container has just been created new but not started yet.
    - Running: In this state, the container would be running with all its associated processes.
    - Paused : This state happens when the running container has been paused.
    - Stopped: This state happens when the running container has been stopped.
    - Deleted: In this, the container is in a dead state.

* Docker containers commands:
    ```bash
        docker ps –all                   # List Currently Running Docker Containers
        docker start <CONTAINER ID HERE> # Start Docker Container
        docker stop <CONTAINER ID HERE>  # Stop Running Docker Container
        docker rm <CONTAINER ID HERE>    # Delete Docker Container
        # Note: To delete a running Docker container, you will need to first stop it. 
        # Execute the docker stop <CONTAINER ID> command to first stop running docker container.
        For example:
        docker build --tag=albums-microservice --force-rm=true .
        docker run -d <IMAGE NAME>       # Run Docker Image in Docker Container
        # Where -d is used to detach the process so you can continue working with a terminal window and execute other commands.
        docker logs <CONTAINER ID HERE>                      ----> Check Docker Container Logs
        docker logs ceaf9e1ebef5                             ----> Check Docker Container Logs
        docker inspect <CONTAINER ID HERE>                   ----> Inspect Docker Container
        docker exec -it <CONTAINER ID HERE> <COMMAND TO RUN> ----> Execute Commands in Docker Container
            For example:
            docker exec -it 67e36143717b ls
            docker exec -it 67e36143717b bash
            docker run <CONTAINER ID> -e "<ENVIRONMENT VARIABLE NAME>=<VALUE>" # Pass Environment Variables
            # For example:
            docker run ceaf9e1ebef5 -e "SPRING_PROFILES_ACTIVE=dev" -e "server.port=8080"
    ```

