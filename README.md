# Running RQDA in linux using Docker

- A big thanks to [Fred Vanwin](https://github.com/FrdVnW/dockerqda) for creating and maintaining the docker container.
- The instructions were adapted from:
    - https://github.com/FrdVnW/dockerqda
    - https://hub.docker.com/r/frdvnw/dockerqda
- Also, thank you to [Ronggui Huang](https://github.com/Ronggui) for creating RQDA.


### Pulling the docker images
```
docker pull frdvnw/dockerqda
```

### Save the following commands as RunDockeRQDA.sh

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

### Exec the script for running the container initially 

```
./RunDockeRQDA.sh
```
### For subsequent running of the container
```
docker start -i whirl_wheels
```
