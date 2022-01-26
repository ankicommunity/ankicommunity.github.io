# Compiling Docker images for foreign architectures

Sometimes you would like to run `anki-sync-server` on a Raspberry Pi with `ARM`
CPU, or on an older computer with `i686` CPU on the board.

When starting the Docker container instance, you may encounter a message
indicating an "exec format error".

This is likely due to the fact that you are trying to run a Docker image on an
architecture it is not compatible with. Check the architecture of your CPU and
check that you are using the appropriate Docker image.

!!! note "`lscpu`"

    On GNU/Linux distributions, you can usually check your CPU architecture
    with `lscpu`.

If this image does not exist, you can usually easily create it, following the
build instructions in the appropriate repository.


## Building a Docker image

Most of the time you can build the Docker image by entering the directory that 
contains the `Dockerfile` and execute the command:

    docker build -t container_name:tag .

For example:

    docker build -t my-arm-build-of_anki-sync-server .

!!! warning "Always check the repository for special instructions first"

    Sometimes there is already a script supplied that prepares the repository first.
    If the `README` mentions one, use that, and modify it before running, accordingly.

    For example, `docker-anki-sync-server` uses a separate `build.sh`, as it is mentioned in the `README`.

After creating the image, the result is going to be stored in the local Docker cache
under the name and tag you specified, ready for use.

## Publishing the image

If you wish to share your compiled image with others, the easiest way is to 
upload to DockerHub. After creating an account, you can attach your Docker 
installation to it with `docker login`.

Tag your existing image in the way you are going to upload it to DockerHub.
Tagging means creating another alias for the same image in your local
cache.

!!! note "Listing your images"

    You can list the images and their tags in your local cache using `docker image ls`.

For example, if your username on DockerHub is `yourdockerid`, and you wish 
to upload the image under your account, you need to tag it first,
then push it:

    docker tag my-arm-build-of_anki-sync-server yourdockerid/yourreponame:arm64
    docker tag my-arm-build-of_anki-sync-server yourdockerid/yourreponame:latest
    docker push yourdockerid/yourreponame:arm64
    docker push yourdockerid/yourreponame:latest

!!! note "Share your image with us"

    We are happy to include your build of the image under the unofficial builds,
    here in this portal.