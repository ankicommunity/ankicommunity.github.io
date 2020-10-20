# How to use our Docker images

Servers backed by Docker images have the advantage that:
    
* If they work on our machine, they will probably work on your machine
    * Docker makes us easier to ship working versions of the server
    * Docker makes you easier to configure the servers through the unified
      interface it provides


As of yet, the easiest and most reliable way to install `anki-sync-server` is
probably to use one of our Docker images.

**You can grab an image from [Supported
Projects](/Supported%20Projects/anki-sync-server/).**

## Installation of Docker

Please refer to the tutorial on the installation [Docker's
manual](https://docs.docker.com/get-docker/) to get started.

!!! note "It is quite easy to get started on Linux"

    On a GNU/Linux distribution you can usually find Docker in the default package
    manager. Install the appropriate package and activate the service.

From now on we're assuming that you have installed Docker successfully to your
machine.

## An example of installation `anki-sync-server`

!!! warning "This is a general quick tutorial for Docker"

    The images we provide usually have special instructions. Please refer
    to the `README` of the appropriate repository. We are going to set up an instance of `anki-sync-server` here, but you
    can apply the instructions to any image.


### One-time setup

If you only want to see the server in action the quickest way possible in an
ad-hoc manner, you can start an instance it right now.

1. Create a directory to persist the server data (such as your collections)
2. Start a temporary container

```
# substitute $PERSISTENCE_DIR and $DOCKER_IMAGE accordingly, for example:
# export PERSISTENCE_DIR=/home/kuklinistvan/anki-sync-server-persistence/
# export DOCKER_IMAGE=kuklinistvan/anki-sync-server:latest
```

!!! warning "Select your own image"

    Do not copy `DOCKER_IMAGE` from here, as this is just an example. Grab the
    identifier of the image you wish to use
    from [Supported Projects](/Supported%20Projects/anki-sync-server/).

```
docker run -it \
       --mount type=bind,source="$PERSISTENCE_DIR",target=/app/data \
       -p 27701:27701 \
       --name anki-container \
       --rm \
       $DOCKER_IMAGE
```

| Argument | Explanation |
|----------|-------------|
| `--mount type=bind,source="$PERSISTENCE_DIR",target=/app/data` | Mounts the persistence into the container, such that the instance can write data into it. |
| `-p 27701:27701` | Opens a port on all of the network interfaces of host machine. First number: port number on the host machine (feel free to change it), second: the port of the server that runs in the container (fixed, you don't need to worry about it). |
| `--rm` | Remove the container after the execution is done. Note that it does not remove the `$PERSISTENCE_DIR`. |
| `$DOCKER_IMAGE` | The unique identifier of the image. Get it from [Supported Projects](/Supported%20Projects/anki-sync-server/). |
| `--name` | An arbitrary name to reference the container instance later. |
| `-it` | Run in foreground (see the [Docker reference](https://docs.docker.com/engine/reference/run/) for the exact meaning) |


On Linux, you can interrupt this instance anytime by hitting Ctrl+C. You can
restart the server with the same command.

<!-- See below how you can point your desktop application to the server you've just created. -->

### Permanent server setup

If you are satisfied with the result you can make the service start at boot by
modifying some of the flags.

| Old flags | New flags | Comment |
|-----------| -------- | ------- |
| `-it`       | `-itd`     | Run in background ([Docker reference](https://docs.docker.com/engine/reference/run/)) |
| `--rm`    |          | Do not remove the container if it has crashed. This gives you a chance to inspect it after it has stopped if something has gone wrong. |
|           | `--restart always` | Restart the image automatically if it has stopped. ([Docker reference](https://docs.docker.com/engine/reference/run/#restart-policies---restart)) |
| 

The new version in the above example would look as follows:
    
    docker run -itd \
       --mount type=bind,source="$PERSISTENCE_DIR",target=/app/data \
       -p "$HOST_PORT":27701 \
       --name anki-container \
       --restart always \
       $DOCKER_IMAGE

As long as the Docker service starts at boot, you can set and forget the server
that way.

#### Permanent server setup using Docker-compose

Sometimes it is easier save the configuration and make it more readable with `docker-compose`.

In this setup, you would create an empty directory with a `docker-compose.yml` similar to the one below.
Please modify `<SUBSTITUTE_$DOCKER_IMAGE_HERE>` accordingly.

    version: "3"
    
    services:
        anki-container:
            image: kuklinistvan/anki-sync-server:latest
            container_name: anki-container
    
            restart: always
            ports:
            - "27701:27701"
            volumes:
            - data:/app/data
    
    volumes:
    data:


When you're done, open up a terminal in that directory and control the instance
with the commands below:

| Command | Explanation |
| ------- | ----------- |
| `docker compose up` | Run the configuration in the foreground (interrupt with Ctrl+C on Linux) |
| `docker compose up -d` | Run the configuration in the background. Set and forget. It is going to start at system boot from now on. |
| `docker compose stop` | Stop the server. |
| `docker compose down -v` | **Destroy** the instance **along with the persistent `data` directory**! This removes your collections! You may run this if you wish to start over or purge the server completely. |

Please refer to the [Docker guides](https://docs.docker.com/compose/) for a more
accurate reference of the commands and the arguments.

### Accessing the container - administering the server

The server has a command line administration interface, that you can access
from a shell in your container. Provided that you did not alter the `name`
attribute, your container should be named `anki-container`.

!!! note

    You can check the name of the container with `docker ps`.

You can access a shell in it while the container is running.

    docker exec -it anki-container sh

In the case of `anki-sync-server`, you can access the admin CLI:

    /app/anki-sync-server # ./ankisyncctl.py --help
    usage: ./ankisyncctl.py <command> [<args>]
    
    Commands:
    adduser <username> - add a new user
    deluser <username> - delete a user
    lsuser             - list users
    passwd <username>  - change password of a user



## Encryption

**Be warned** that if you don't use any additional proxies, your connection will
be unencrypted! That means if you use Anki to memorize your passwords they will
be leaked :) 

<sup>Please don't do that though, as Anki is not designed in mind for safely
handling risky data, such as passwords, in the first place.</sup>

Please refer to one of the solutions at the [Encryption](/Tutorials/Encryption%20with%20proxy/Apache/) section.


## Troobleshooting

??? note "Pull requests are welcome!"

    If you encounter an error which is not listed here but you think
    it would be worth mentioning the solution, we are happy to accept
    your pull request to [the repository of this portal](https://github.com/ankicommunity/ankicommunity.github.io).

### exec format error

  Please refer to [this guide](/Tutorials/Docker/Howto_Recompiling/).

