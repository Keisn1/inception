# General Guidelines

  - \[ \] must be completed on a virtual machine
  - \[ \] all files need to be under srcs folder
  - \[ \] Makefile located at root of directory
      - \[ \] must set up the entire application
      - \[ \] has to build Docker images using `docker-compose.yml`

# Mandatory Part

  - \[ \] each image must have the same name as its corresponding
    service
  - \[ \] each service has to run in a dedicated container
  - \[ \] each container must be built either from **penultimate stable
    version** Alpine or Debian
      - one step behind the most recent stable release
  - \[ \] write one Dockerfile per service
      - \[ \] Dockerfiles must be called in your docker-compose.yml by
        your Makefile
      - \[ \] means, build your Docker images yourself
      - \[ \] no Dockerhub (Alpine/Debian excluded)
  - \[ \] containers must restart automatically in case of crash

## Container

### NGINX

  - \[ \] TLSv1.3 or TLSv1.2

### WordPress

  - \[ \] with php-fpm only (must be installed and configured)
  - \[ \] without NGINX

### MariaDB

  - \[ \] without NGINX

### Volume 1

  - \[ \] contains WordPress database

### Volume 2

  - \[ \] contains WordPress files

### docker-network

  - \[ \] establishes connection between the containers

## Extra information

  - \[ \] don't use 'tail -f' to run a service in a container
      - without a long-running command specified in the Dockerfile, a
        container will exit/shutdown immediately after starting
      - `tail -f /dev/null` is often used as a hacky solution
      - configure a proper entrypoint
  - \[ \] read up on how daemons work to run services in a container
    properly
