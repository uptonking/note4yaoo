---
title: devops-docker-docs
tags: [docker, docs]
created: 2024-06-30T11:20:37.482Z
modified: 2024-06-30T11:20:53.755Z
---

# devops-docker-docs

# guide

# cli
- docker exec [OPTIONS] CONTAINER COMMAND [ARG...]
  - Execute a command in a running container
  - To easily get a debug shell into any container, use `docker debug`. Docker Debug is a replacement for debugging with `docker exec`. 
  - The command runs in the default working directory of the container.
  - The command must be an executable. A chained or a quoted command doesn't work.
  - If the container is paused, then the docker exec command fails with an error
  - -i, --interactive		Keep STDIN open even if not attached
  - -t, --tty		Allocate a pseudo-TTY

- 
- 
- 
- 

## cli-compose

- docker compose up [OPTIONS] [SERVICE...]
  - Builds, (re)creates, starts, and attaches to containers for a service.
  - Unless they are already running, this command also starts any linked services.
  - If there are existing containers for a service, and the service’s configuration or image was changed after the container’s creation,  `docker compose up` picks up the changes by stopping and recreating the containers (preserving mounted volumes).
  - If you want to force Compose to stop and recreate all containers, use the `--force-recreate` flag.

- docker compose down [OPTIONS] [SERVICES]
  - Stops containers and removes containers, networks, volumes, and images created by `up`.
  - Networks and volumes defined as external are never removed.
  - By default, the only things removed are:
    - Containers for services defined in the Compose file.
    - Networks defined in the networks section of the Compose file.
    - The default network, if one is used.
  - Anonymous volumes are not removed by default. However, as they don’t have a stable name, they are not automatically mounted by a subsequent `up`. 

- docker compose run [OPTIONS] SERVICE [COMMAND] [ARGS...]
  - Runs a one-time command on a service.
  - the command passed by `run` overrides the command defined in the service configuration
  - docker compose run command does not create any of the ports specified in the service configuration. This prevents port collisions with already-open ports. 

- docker compose start [SERVICE...]
  - Starts existing containers for a service
- docker compose stop [OPTIONS] [SERVICE...]
  - Stops running containers without removing them. They can be started again with docker compose start.

- docker compose exec [OPTIONS] SERVICE COMMAND [ARGS...]
  - Execute a command in a running container
  - This is the equivalent of `docker exec` targeting a Compose service.
  - Commands allocate a TTY by default, so you can use a command such as `docker compose exec web sh` to get an interactive prompt.

- 
- 
- 

# docs
- [Use the Docker command line | Docker Docs](https://docs.docker.com/engine/reference/commandline/cli/)
# more
