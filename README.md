# Introduction
With this project we will be able to work on symfony 5 and postgres based project without
installing all the dependency that will help in our tasks, to do so we are going to use docker.
Using docker will help a lot but also it will bring some tricky situation that need to be handled.
I hope with this repo you're life as a symfony developer will be easier.

# Requirements
To be able to run the project you'll need docker to be installed, also configure your regular user account to be able to execute docker commands to prevent credential problems.

# Getting started
After installing and configuring docker clone this repo with the following command:
```
git clone https://github.com/zendyani/docker-symfony5-pgadmin-postgres.git
```

## Configuring the project
Your docker-compose.yaml use the file .env to provision informations like Posgress credential
Or pgAdmin creadential so you need to rename the env file to .env and make the neccessary modification.

## Files organisation
- "code" will contain your symfony project code.
- "data/postgres" will contain files concerning posgress container.
- "logs" will contain nginx access and error logs.
- "nginx" will contain nginx configuration files that will be mapped inside nginx container.
- "php-fpm" will contain the Dockerfile used to generate the image with all the requirements
of a modern symfony app and the php-fpm config file that will be used for the php-fpm container

# Work with symfony
After running docker-compose and all the container started successfully you'll be able to start coding your symfony project, to do so follown the next instructions:
## Init symfony project:
```
docker-compose run php-fpm symfony new .
```
This instruction will init your codebase inside code directory.

## Install a new composer package:
```
docker-compose run php-fpm symfony composer req package_name
```
Of course you can use directly compose instead of symfony binary like the following example:

```
docker-compose run php-fpm composer req package_name
```

## Run symfony commandline 

```
docker-compose run php-fpm symfony console make:....
```

As you can see it's always "docker-compose run php-fpm" followed by the command, if you're a docker beginner the first statement means run the command inside php-fpm container, "php-fpm" represent the name of the container used in docker-compose.yaml

# More docker commands

```
# List container created by docker-compose
docker-compose ps
# OR
docker ps

# connect to a container
docker-compose run container_name /bin/sh
# OR
docker exec -it container_name /bin/sh
```

# Reset container
start by removing data files
```
sudo rm -rf database/data/*
```
Rebuild containers
```
docker-compose up --build
```

# Help
[Docker cheatsheet](https://github.com/wsargent/docker-cheat-sheet)
[Php alpine image](https://github.com/codecasts/php-alpine)
[Docker for symfony](http://www.inanzzz.com/index.php/post/isb1/alpine-docker-setup-for-symfony-applications)

# License

This project is licensed under the MIT License - see the LICENSE.md file for details