# Running RQDA in linux using Docker

- A big thanks to [Fred Vanwin](https://github.com/FrdVnW/dockerqda) for creating and maintaining the docker container.
- Also, thank you to [Ronggui Huang](https://github.com/Ronggui) for creating RQDA.
- The instructions were adapted from:
    - https://github.com/FrdVnW/dockerqda
    - https://hub.docker.com/r/frdvnw/dockerqda
- Kindly refer to the original instructions by [Fred Vanwin](https://hub.docker.com/r/frdvnw/dockerqda) for more information.


## Setup
- Download or clone the repository to your local drive.

### Edit the RunDockeRQDA.sh file

- in command for volume, replace **paste the location of the folder you want** to the location of the folder of your choice.
- This will be the folder were RQDA running in docker will be able to view the files in our system
- However while once RQDA runs the user as to navigate to /home/dockerqda/
- Since the volume command connects the folder of our choice to the folder dockerqda in the docker system

```
#!/bin/bash
XSOCK=/tmp/.X11-unix
XAUTH=/tmp/.docker.xauth
xauth nlist $DISPLAY | sed -e 's/^..../ffff/' | xauth -f $XAUTH nmerge -
sudo docker run -it --volume=$XSOCK:$XSOCK:rw \
     --volume=$XAUTH:$XAUTH:rw \
     --env="XAUTHORITY=${XAUTH}" \
     --env="DISPLAY" \
     --name whirl_wheels \
     --workdir=/root/ \
     --volume=paste the location of the folder you want:/home/dockerqda/ \
     frdvnw/dockerqda:latest
```

### Making the script executable
```
chmod +x RunDockeRQDA.sh
```


### Execute the script for running RDQA

- Pull the docker image.

```
docker pull frdvnw/dockerqda
```

- Exceute RunDockeRQDA.sh in terminal.

```
./RunDockeRQDA.sh
```
- R will open in the terminal. 
- From there lauch RDQA.

### For subsequent running of RQDA

- Just execute the ./RunDockeRQDA.sh script
