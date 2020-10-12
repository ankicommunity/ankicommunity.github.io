
How to create an user on the anki sync server
==============================================================

# Creating users when anki sync server run directly on the os
just run
    ./ankisyncctl.py adduser yourusername
to list all the command, run 
    ./ankisyncctl.py --help

# Creating users when anki sync server is in a docker
Your server is running, the client try to connect to it and you're greeted with  "the password is not correct or the user don't exist" -> you need to create a user first
For this you need to access your container instance in order to use the server's ctl:


The first command give you a shell inside the docker container, once you are inside you run the second one (./ankisyncctl.py)
this tool allows you to create/delete/list/change password for a user.

if your container is not named anki-container you can get his id with

    # docker ps
    and use the docker id instead of the name in the following command .
    
Otherwise you can just run the followings commands 
    
    # docker exec -it anki-container /bin/sh
    
    /app/anki-sync-server # ./ankisyncctl.py --help
    

    usage: ./ankisyncctl.py <command> [<args>]
    
    Commands:
      adduser <username> - add a new user
      deluser <username> - delete a user
      lsuser             - list users
      passwd <username>  - change password of a user

     
    /app/anki-sync-server # ./ankisyncctl.py adduser kuklinistvan
    Enter password for kuklinistvan:

Done!

# Troobleshooting
If you encounter some error by following thoses procedures and you find out how to fix it please create a Push request adding how to solve the problem here.
