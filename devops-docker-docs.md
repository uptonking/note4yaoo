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

## 🛢️ [Volumes | Docker Docs](https://docs.docker.com/engine/storage/volumes/)

- By default all files created inside a container are stored on a writable container layer that sits on top of the read-only, immutable image layers.
  - Data written to the container layer doesn't persist when the container is destroyed. This means that it can be difficult to get the data out of the container if another process needs it.
  - The writable layer is unique per container. You can't easily extract the data from the writeable layer to the host, or to another container.

- No matter which type of mount you choose to use, the data looks the same from within the container. 
  - It is exposed as either a directory or an individual file in the container's filesystem.

- Volume mounts
  - Volume data is stored on the filesystem on the host, but in order to interact with the data in the volume, you must mount the volume to a container. 
  - Directly accessing or interacting with the volume data is unsupported
  - They retain data even after the containers using them are removed.
  - Since the storage location is managed on the daemon host, volumes provide the same raw file performance as accessing the host filesystem directly.
  - Volumes are ideal for performance-critical data processing and long-term storage needs.

- Bind mounts
  - Bind mounts create a direct link between a host system path and a container, allowing access to files or directories stored anywhere on the host. 
  - Since they aren't isolated by Docker, both non-Docker processes on the host and container processes can modify the mounted files simultaneously.
  - Use bind mounts when you need to be able to access files from both the container and the host.

- tmpfs mounts
  - A tmpfs mount stores files directly in the host machine's memory, ensuring the data is not written to disk. 
  - This storage is ephemeral: the data is lost when the container is stopped or restarted, or when the host is rebooted. 
  - tmpfs mounts do not persist data either on the Docker host or within the container's filesystem.
  - These mounts are suitable for scenarios requiring temporary, in-memory storage, such as caching intermediate data, handling sensitive information like credentials, or reducing disk I/O.

- Named pipes
  - Named pipes can be used for communication between the Docker host and a container. 
  - Common use case is to run a third-party tool inside of a container and connect to the Docker Engine API using a named pipe.

- Volumes are persistent data stores for containers, created and managed by Docker. 
  - When you create a volume, it's stored within a directory on the Docker host. When you mount the volume into a container, this directory is what's mounted into the container. 
  - This is similar to the way that bind mounts work, except that volumes are managed by Docker and are isolated from the core functionality of the host machine.
- While bind mounts are dependent on the directory structure and OS of the host machine, volumes are completely managed by Docker. 
  - Volumes are not a good choice if you need to access the files from the host, as the volume is completely managed by Docker. 
  - Use bind mounts if you need to access files or directories from both containers and the host.

- Unlike a bind mount, you can create and manage volumes outside the scope of any container.

- ❓ Volumes are often a better choice than writing data directly to a container, because a volume doesn't increase the size of the containers using it. 
- Using a volume is also faster; writing into a container's writable layer requires a storage driver to manage the filesystem. The storage driver provides a union filesystem, using the Linux kernel. This extra abstraction reduces performance as compared to using volumes, which write directly to the host filesystem.

- If you mount a non-empty volume into a directory in the container in which files or directories exist, the pre-existing files are obscured by the mount. 
- If you mount an empty volume into a directory in the container in which files or directories exist, these files or directories are propagated (copied) into the volume by default. 

- Just like named volumes, anonymous volumes persist even if you remove the container that uses them, except if you use the --rm flag when creating the container
  - Anonymous volumes are given a random name that's guaranteed to be unique within a given Docker host. 
  - Anonymous volumes aren't reused or shared between containers automatically.

- When you use a bind mount, a file or directory on the host machine is mounted from the host into a container. 
  - By contrast, when you use a volume, a new directory is created within Docker's storage directory on the host machine, and Docker manages that directory's contents.

- If you bind mount file or directory into a directory in the container in which files or directories exist, the pre-existing files are obscured by the mount. 
  - With containers, there's no straightforward way of removing a mount to reveal the obscured files again. Your best option is to recreate the container without the mount.
- If you bind-mount a directory into a non-empty directory on the container, the directory's existing contents are obscured by the bind mount. This can be beneficial, such as when you want to test a new version of your application without building a new image. 
  - However, it can also be surprising and this behavior differs from that of volumes.

- Bind mounts have write access to files on the host by default.
- Containers with bind mounts are strongly tied to the host.

- When you start a service and define a volume, each service container uses its own local volume. None of the containers can share this data if you use the `local` volume driver. 

- 
- 
- 
- 

# docs-compose/config
- A service is an abstract definition of a computing resource within an application which can be scaled or replaced independently from other components. 
  - A service definition contains the configuration that is applied to each service container.
  - Each service may also include a build section, which defines how to create the Docker image for the service

- `entrypoint` declares the default entrypoint for the service container. This overrides the `ENTRYPOINT` instruction from the service's `Dockerfile`.
  - See also `command` to set or override the default command to be executed by the entrypoint process.

- `image` specifies the image to start the container from, as `[<registry>/][<project>/]<image>[:<tag>|@<digest>]`.
  - If the image does not exist on the platform, Compose attempts to pull it based on the pull_policy.
  - `image` may be omitted from a Compose file as long as a `build` section is declared. 

- You can use `volumes` to define multiple types of mounts; volume, bind, tmpfs, or npipe.
  - The short syntax uses a single string with colon-separated values to specify a volume mount (`VOLUME:CONTAINER_PATH`), or an access mode (`VOLUME:CONTAINER_PATH:ACCESS_MODE`).
  - `VOLUME`: Can be either a host path on the platform hosting containers (bind mount) or a volume name.
  - Relative host paths are only supported by Compose that deploy to a local container runtime. This is because the relative path is resolved from the Compose file’s parent directory which is only applicable in the local case. When Compose deploys to a non-local platform it rejects Compose files which use relative host paths with an error. 

- 
- 
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
