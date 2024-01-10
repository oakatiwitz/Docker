# L08-03

## Open a terminal and create a volume

    docker volume create myvol

## List the volumes

    docker volume ls

## Run a Nginx container that will use the volume
# -d : detach

    docker run -d --name voltest -v myvol:/app nginx:latest

## Connect to the instance

    docker exec -it voltest bash

## Let’s create a file in the volume using Nano

    apt-get update
    apt-get install nano

## Create a file in the app folder
    cd app
    nano test.txt

Type something, save the file and exit Nano using:

    CTRL-O
    CTRL-X

Detach from the instance:

    exit

## Stop and remove the container

    docker stop voltest
    docker rm voltest

## Run it again and see if the file still exists

    docker run -d --name voltest -v myvol:/app nginx:latest
    docker exec -it voltest bash
    cd app
    cat test.txt

## Cleanup

    docker stop voltest
    docker rm voltest
    docker volume rm myvol  # you cannot delete the volume if it is used.

Summary
    This exercise show that the volume is external from this container so if we delete the containter, the data is still stored in volume and then if we run the new instance that use the same volume, the new instance will contain the same data with the old instance that we already deleted.