# Docker

## What problem does Docker solve?

Most people use an operating system like Windows, MacOS or Linux.
Furthermore, some people have installed runtimes, libraries and databases like Python, NodeJS, Ruby, MySQL, PostgreSQL etc.

**Short**: We all have very different systems in use.

**Problem**: It is tedious to setup working environments, that fulfill all needed runtimes and dependencies to run a specific application.
Moreover, after working with this specific application, it is tedious to clean up the polluted environment.
A lot of orphaned runtimes and dependencies get accumulated.

**Solution**: Docker saves you the stress by isolating your application and its dependencies into a single self-contained unit that can reliably run anywhere.

## Important Terms

**Docker Image**: A docker image is like a recipe. An image is built from Dockerfile which is a text document that contains instructions on how docker should build an image.

**Docker Container**: A docker container is a cookie, built from the recipe (docker image).
In technical language, a docker container is as an instance of a docker image.

**Docker compose**: A working software is never an island, it will most likely depend on a bunch of other things like database, cache and even other services. It's best practice to have each of these in their respective container. With docker-compose, you can define a multi-container application in a single file which can be spun up in a single command.

## Commands

[Docker Documentation](https://docs.docker.com/)

- `docker images -a`: show all images (recipes)
- `docker ps -a`: show all containers (cookies built from recipes)
- `docker pull <imagename>`: download recipe from docker hub
- `docker search <searchterm>`: search docker hub for searchterm
- `docker run <imagename>`: run image to get a container (run recipe to bake cookie)
