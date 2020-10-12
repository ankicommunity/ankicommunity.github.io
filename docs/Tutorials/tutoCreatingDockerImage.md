How to create a docker image on a new device / architecture
===========================================================

# Origin
This explanation is based on [this ticket](https://github.com/ankicommunity/docker-anki-sync-server/issues/9)

# Architectures
you may be aware that CPU come in different flavour.
there are two parameters to take into account that are the Architecture and the number of bit 
the two main architecture are X86 comonly found in intel CPU (desktop computer, server, etc) and ARM (found in raspberry pi aswell as other SBC and most phones)
most x86 CPU todays are 64 bits.
when it come to ARM 32 and 64 bits are still quite common. (older raspbbery pi where 32 bits, from the 3B+ (with a 64 bit OS) are now 64 bit)

# Instructions
    git clone https://github.com/ankicommunity/docker-anki-sync-server
    cd docker-anki-sync-server/Docker
    ./build.sh
You've have now made a docker image
You may want to create a container from the docker image (a container is kinda like an object instance of it's class)
to do so : 
    docker run --publish=27701:27701 --restart=always --name=anki-container --mount=type=bind,source=/mnt/anki/data,target=/app/data anki-sync-server:tsudoko-ankisyncd-2.1.0-plus-2bfccf7f
(add any docker options that may server you and set the path where you need it)
You shoud have something like that that appeared

    Creating new configuration file: ankisyncd.conf. Creating new authentication database: auth.db. Creating collections directory: collections. Updating database schema Successfully updated table 'auth' No session DB found at the configured 'session_db_path' path. Starting tsudoko's anki-sync-server [2020-10-06 10:43:50,853]:INFO:ankisyncd:ankisyncd [unknown version] (https://github.com/tsudoko/anki-sync-ser ver) [2020-10-06 10:43:51,110]:INFO:ankisyncd:Loaded config from /app/anki-sync-server/ankisyncd.conf [2020-10-06 10:43:51,113]:INFO:ankisyncd.users:Found auth_db_path in config, using SqliteUserManager for auth [2020-10-06 10:43:51,119]:INFO:ankisyncd.sessions:Found session_db_path in config, using SqliteSessionManager for auth [2020-10-06 10:43:51,126]:INFO:ankisyncd:Serving HTTP on 0.0.0.0 port 27701... [2020-10-06 10:43:51,613]:INFO:ankisyncd.http:127.0.0.1 "GET / HTTP/1.1" 200 16

    docker ps
give you the id of the running container
    docker exec -it dde248e9bc6e /bin/sh
give you a shell inside a given docker dde248e9bc6e being the container id.
run
    ./ankisyncctl.py adduser yourusername
to create an user on your docker instance
You need to create a free dockerhub account (you just need a valid email) to publish your container such that other dont have to redo it

    docker commit --author="you@you.com" --message=" the platform and a comment" --pause anki-container yourdockerid/yourreponame:latest
this is analogue to a git commit
    docker login # login to dockerhub such that you can push it to the platform
    docker push yourdockerid/yourreponame:latest # this is analogue to a git push, it send the docker image to  dockerhub
Dont forget to make a pull request to add the instruction for your platform (under [How to deploy a containerised version of the Anki sync server](https://ankicommunity.github.io/Tutorials/Index/DockerDeploy/)

# Troobleshooting
if you happen to have any issue with thoses explanations and you do find a way to solve it dont hesitate to make a push request with your issue here.
