How to deploy a containerised version of the Anki sync server
==============================================================

# On a normal server
Docker will take care of starting the service on boot so you don't have to worry about that. You can setup the server with these commands:

    export DOCKER_USER=root
    export ANKI_SYNC_DATA_DIR=/etc/anki-sync-server
    export HOST_PORT=27701
    
    mkdir -p "$ANKI_SYNC_DATA_DIR"
    chown "$DOCKER_USER" "$ANKI_SYNC_DATA_DIR"
    chmod 700 "$ANKI_SYNC_DATA_DIR"
    
    docker run -itd \
       --mount type=bind,source="$ANKI_SYNC_DATA_DIR",target=/app/data \
       -p "$HOST_PORT":27701 \
       --name anki-container \
       --restart always \
       kuklinistvan/anki-sync-server:latest

or using `docker-compose`:

    version: "3"
    
    services:
        anki-sync-server:
            image: kuklinistvan/anki-sync-server:latest
            restart: always
            ports:
            - "27701:27701"
            volumes:
            - ./data:/app/data
            
# On a raspberry pi
This is really close to the installation on a normal server expect that another docker image is used (may work on other ARM CPU but not tested)
Docker will take care of starting the service on boot so you don't have to worry about that. You can setup the server with these commands:

    export DOCKER_USER=root
    export ANKI_SYNC_DATA_DIR=/etc/anki-sync-server
    export HOST_PORT=27701
    
    mkdir -p "$ANKI_SYNC_DATA_DIR"
    chown "$DOCKER_USER" "$ANKI_SYNC_DATA_DIR"
    chmod 700 "$ANKI_SYNC_DATA_DIR"
    
    docker run -itd \
       --mount type=bind,source="$ANKI_SYNC_DATA_DIR",target=/app/data \
       -p "$HOST_PORT":27701 \
       --name anki-container \
       --restart always \
       nathmo/anki-sync-server:initial

or using `docker-compose`:

    version: "3"
    
    services:
        anki-sync-server:
            image: nathmo/anki-sync-server:initial
            restart: always
            ports:
            - "27701:27701"
            volumes:
            - ./data:/app/data
            
# Troobleshooting

If you encounter some error by following thoses procedures and you find out how to fix please create a Push request adding how to solve the problem here.

## anki-sync-server_1 | standard_init_linux.go:211: exec user process caused "exec format error"
  This is likely due to the fact that you are trying to run a docker image on an architecture it was not inteded for.
  check the architecture of your CPU (likely X86 or ARM64) and check that you are using the appropriate docker image
  If this image do not existe you can create it followings thoses [instructions](https://ankicommunity.github.io/Tutorials/Index/CreatingDockerImage/)
