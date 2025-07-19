---
title: devops-docker-docs
tags: [docker, docs]
created: 2024-06-30T11:20:37.482Z
modified: 2024-06-30T11:20:53.755Z
---

# devops-docker-docs

# guide

# cli
- [Use the Docker command line | Docker Docs](https://docs.docker.com/engine/reference/commandline/cli/)

- 👉 docker exec [OPTIONS] CONTAINER COMMAND [ARG...]
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

- [Prune unused Docker objects | Docker Docs](https://docs.docker.com/engine/manage-resources/pruning/)
  - `docker system df`: 查看磁盘占用  
  - By default,  `docker image prune` only cleans up dangling images. 
  - A dangling image is one that isn't tagged, and isn't referenced by any container. 
  - When you stop a container, it isn't automatically removed unless you started it with the `--rm` flag.
  - A stopped container's writable layers still take up disk space.
  - Volumes are never removed automatically, because to do so could destroy data.
  - Docker networks don't take up much disk space, but they do create iptables rules, bridge network devices, and routing table entries.
  - The `docker system prune` command is a shortcut that prunes images, containers, and networks. Volumes aren't pruned by default

```shell
docker system prune
docker builder prune

docker container prune
# 👀
docker image prune
docker network prune
# 👀
docker volume prune
```

- 🗑️ docker system prune [OPTIONS]
  - Remove all unused containers, networks, images (both dangling and unused), and optionally, volumes.
  - By default, volumes aren't removed to prevent important data from being deleted
  - --volumes		Prune anonymous volumes

- docker builder prune
  - Remove build cache

- 
- 

## cli-compose

- `docker compose`: Define and run multi-container applications with Docker
  - You can supply multiple `-f` configuration files. 
  - When you supply multiple files, Compose combines them into a single configuration. Compose builds the configuration in the order you supply the files. 
  - Subsequent files override and add to their predecessors. any matching fields override the previous file. 
  - all paths in the files are relative to the first configuration file specified with -f. 
  - The `-f` flag is optional. If you don’t provide this flag on the command line, Compose traverses the working directory and its parent directories looking for a `compose.yaml` or `docker-compose.yaml` file.

- 👉 docker compose up [OPTIONS] [SERVICE...]
  - Builds, (re)creates, starts, and attaches to containers for a service.
  - Unless they are already running, this command also starts any linked services.
  - If there are existing containers for a service, and the service’s configuration or image was changed after the container’s creation,  `docker compose up` picks up the changes by stopping and recreating the containers (preserving mounted volumes).
  - If you want to force Compose to stop and recreate all containers, use the `--force-recreate` flag.

- 👉 docker compose down [OPTIONS] [SERVICES]
  - Stops containers and removes containers, networks, volumes, and images created by `up`.
  - Networks and volumes defined as external are never removed.
  - By default, the only things removed are:
    - Containers for services defined in the Compose file.
    - Networks defined in the networks section of the Compose file.
    - The default network, if one is used.
  - Anonymous volumes are not removed by default. However, as they don’t have a stable name, they are not automatically mounted by a subsequent `up`. 

- 👉 docker compose run [OPTIONS] SERVICE [COMMAND] [ARGS...] 下载并启动
  - Runs a one-time command on a service.
  - the command passed by `run` overrides the command defined in the service configuration
  - docker compose run command does not create any of the ports specified in the service configuration. This prevents port collisions with already-open ports. 

- 👉 docker compose start [SERVICE...]
  - Starts existing containers for a service
- docker compose stop [OPTIONS] [SERVICE...]
  - Stops running containers without removing them.

- 👉 docker compose exec [OPTIONS] SERVICE COMMAND [ARGS...]
  - Execute a command in a running container
  - This is the equivalent of `docker exec` targeting a Compose service.
  - Commands allocate a TTY by default, so you can use a command such as `docker compose exec web sh` to get an interactive prompt.

- 
- 
- 

# docs
- [Environment variables precedence | Docker Docs](https://docs.docker.com/compose/how-tos/environment-variables/envvars-precedence/)
  - When the same environment variable is set in multiple sources, Docker Compose follows a precedence rule to determine the value for that variable in your container's environment.
- The order of precedence (highest to lowest 👇) is 
  - Set using `docker compose run -e` in the CLI.
  - Set using just the `environment` attribute in the Compose file.
  - Use of the `env_file` attribute in the Compose file.
  - Set in a container image in the ENV directive. Having any ARG or ENV setting in a Dockerfile
# docs-compose/config
- A service is an abstract definition of a computing resource within an application which can be scaled or replaced independently from other components. 
  - A service definition contains the configuration that is applied to each service container.
  - Each service may also include a build section, which defines how to create the Docker image for the service

- `entrypoint` declares the default entrypoint for the service container. This overrides the `ENTRYPOINT` instruction from the service's `Dockerfile`.
  - See also `command` to set or override the default command to be executed by the entrypoint process.

- `image` specifies the image to start the container from, as `[<registry>/][<project>/]<image>[:<tag>|@<digest>]`.
  - If the image does not exist on the platform, Compose attempts to pull it based on the pull_policy.
  - `image` may be omitted from a Compose file as long as a `build` section is declared. 

- 
- 
- 

# docs-image-build
- when i run `docker compose -f compose.yaml up`, will it exec `build` config inside `compose.yaml` file?
  - Docker Compose will build the image only if the image doesn't already exist locally (or if you explicitly force a rebuild).
  - `docker compose build`: Runs the build instructions for all services that have a `build:` section in your Compose file, regardless of whether an image already exists.
  - If you’ve never built or pulled the image before, a plain `docker compose up` will automatically build it once, then start the container. Subsequent runs without `--build` will skip rebuilding.

- `build` can be either specified as a single string defining a context path, or as a detailed build definition.
  - In the former case, the whole path is used as a Docker context to execute a Docker build, looking for a canonical `Dockerfile` at the root of the directory. 
  - In the latter case, build arguments can be specified, including an alternate `Dockerfile` location

- `context` defines either a path to a directory containing a `Dockerfile`, or a URL to a Git repository.
  - If not set explicitly, context defaults to project directory (.).
- `dockerfile` sets an alternate Dockerfile. A relative path is resolved from the build context. 
  - `dockerfile` overrides the default Dockerfile. If you omit `dockerfile`, Docker Compose looks for a file named Dockerfile in the `context` directory.

- When building a Dockerfile with multiple build stages, use the `--target` option to specify an intermediate build stage by name as a final stage for the resulting image. The builder skips commands after the target stage.

- An `ENTRYPOINT` allows you to configure a container that will run as an executable.
  - The exec form(preferred): `ENTRYPOINT ["executable", "param1", "param2"]` ; 
  - The shell form: `ENTRYPOINT command param1 param2` ; 
  - The shell form of ENTRYPOINT prevents any CMD command line arguments from being used. It also starts your ENTRYPOINT as a subcommand of `/bin/sh -c`.
  - Command line arguments to `docker run <image>` will be appended after all elements in an exec form `ENTRYPOINT`, and will override all elements specified using `CMD`.

- Both `CMD` and `ENTRYPOINT` instructions define what command gets executed when running a container. 
  - Dockerfile should specify at least one of CMD or ENTRYPOINT commands.
  - ENTRYPOINT should be defined when using the container as an executable.
  - `CMD` should be used as a way of defining default arguments for an ENTRYPOINT command or for executing an ad-hoc command in a container.
  - `CMD` will be overridden when running the container with alternative arguments.

- 
- 
- 
- 
- 
- 
- 
- 

# more
