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
