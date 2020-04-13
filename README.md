## Docker

Simplify building, shipping and running apps.

Benefits:
- Acelerate developer onboarding
    - Set developer environment quickly and consistent
- Eliminate app conflicts
- Environment consistency
- Ship software faster

Tools:
- Docker toolbox (Win7 and 8)
- Docker CE (Win 10+ and Mac)
- 2020 is Docker Desktop

## Using Docker Tools

Docker Client, interact with Docker Daemon, work with images and turn them into containers.
Docker Daemon, engine that controls our containers.

- docker pull hello-world
    - download the hello-world image, layered file system
- docker images
    - list images
- docker run hello-world
    - runs the image
- docker ps
    - show running containers
- docker ps -a
    - show all containers
- docker rm 935
    - removes a container
- docker rmi fce
    - remover an image
- docker run -p 80:80 kitematic/hello-world-nginx
    - external : internal, in container
- docker stop 109
    - stops a container
- docker rm -v 03
    - removes a container and its volume

## Hooking Source Code into a Container

- Layered file system
    - Images and containers are built on top of this system, to promote reusability.
    - Containers have read/write layer.
    - Images are read only layers.
    - Example of that is a Ubuntu image, that may share his layers across multiple containers.

- Volume
    - Is a special type of folder in a container.
    - Can be shared and reused among containers.
    - Updates to image won't affect a data volume.
    - Are persisted even after the container is deleted.
    - Volume is inside a container, and when you write to a volume, it writes actually into ome special area that is defined on your Docker Host, and Docker takes care of it automatically.
    - docker run -p 8080:3000 -v /var/www node
        - Creates a volume automatically by Docker, inside a container
    - docker inspect mycontainer
        - Shows the configuration of the container, also with Source and Destination of the volume
    - docker run -p 8080:3000 -v $(pwd):/var/www node
        - Creates a volume, but set Source configuration to the current folder in the Host, the folder in which we'are running the commands.

- Demo, deploying a project in node container
    1. docker pull node (search for it in docker hub)
    2. docker run -p 8080:3000 -v $(pwd):/var/www -w "/var/www" node yarn start
        - $(pwd):/var/www, points to our current folder
        - -w "/var/www" node, set this as our working directory
        - yarn start, starts the application from working directory

## Dockerfile

Is a text file with build instructions, that runs through the docker client to generate a image.

- Into Node
    1. Creating a Dockerfile in /docker/express-hello-world/ExpressSite/Dockerfile
    2. docker build -f Dockerfile -t bugasmarcondes/node .
    3. docker run -d -p 8080:3000 bugasmarcondes/node