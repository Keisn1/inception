---
author: Kay Freyer
title: Readme
---

# General Guidelines

- [ ] must be completed on a virtual machine
- [ ] all files need to be under srcs folder
- [ ] Makefile located at root of directory
  - [ ] must set up the entire application
  - [ ] has to build Docker images using `docker-compose.yml`

# Mandatory Part

- [ ] each image must have the same name as its corresponding service
- [ ] each service has to run in a dedicated container
- [ ] each container must be built either from **penultimate stable
  version** Alpine or Debian
  - one step behind the most recent stable release
- [ ] write one Dockerfile per service
  - [ ] Dockerfiles must be called in your docker-compose.yml by your
    Makefile
  - [ ] means, build your Docker images yourself
  - [ ] no Dockerhub (Alpine/Debian excluded)
- [ ] containers must restart automatically in case of crash

## Containers

### NGINX

- [ ] TLSv1.3 or TLSv1.2

### WordPress

- [ ] with php-fpm only (must be installed and configured)
- [ ] without NGINX
- [ ] 2 users
  - [ ] administrator
    - [ ] must not contain any form of 'admin' or 'administrator'
  - [ ] another user

### MariaDB

- [ ] without NGINX

### Volume 1

- available under /home/kfreyer/data of the host machine
- [ ] contains WordPress database

### Volume 2

- available under /home/kfreyer/data of the host machine
- [ ] contains WordPress files

### docker-network

- [ ] establishes connection between the containers
- [ ] configure domain name to point to the local IP address
  (kfreyer.login.fr)

## Exclamation points

- [ ] must not use commands that create infinite loops as a way to keep
  the process running
- [ ] no Hacky solutions like `tail -f`, `bash`, `sleep infinity`, and
  `while true`
  - without a long-running command specified in the Dockerfile, a
    container will exit/shutdown immediately after starting
  - configure a proper entrypoint
- [ ] read up on how daemons work to run services in a container
  properly
- [ ] no `network: host` – a configuration that gives the container
  access to the host's networking stack.
- [ ] no `--link` or `links:` – legacy options for connecting
  containers.
- [ ] must have a `network` line in the `docker-compose.yml`
- [ ] passwords not present in Dockerfiles
- [ ] .env and secrets
  - [Chat on Secrets and
    .env](https://42born2code.slack.com/archives/CN9RHKQHW/p1745060462370869)
  - [ ] use .env to store environment variables
  - [ ] use Docker secrets to store any confidential information
- [ ] Nginx container is sole entrypoint into your infrastructure
  - [ ] port 443
  - [ ] TLSv1.3

## Best practices

- [ ] Using a proper init system or handling child processes to manage
  PID 1 characteristics.
  - [tini](https://github.com/krallin/tini)
  - [dumb init](https://github.com/Yelp/dumb-init)
- [ ] Following multi-stage builds for smaller images.
- [ ] Specifying exact versions for dependencies.
- [ ] Minimizing the number of layers by combining commands where
  practical.
- [ ] Avoiding the use of root where possible for security reasons.
- [ ] Keeping the image smaller by cleaning up unnecessary packages.

## Directory structure

# Bonus

- you may open more ports to suit your needs
- [ ] setup `redis cache` for WordPress Website
- [ ] setup `FTP server` container pointing to the Volume of WordPress
  website
- [ ] create a simple static website in the language of your choice
- [ ] Setup `Adminer`
- [ ] Setup Service of your choice. Need to justify it during evaluation
