# build image
docker build -t thunderbird:debian-stretch-slim .

# run container
docker run -ti -d --rm -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix -v ~/data/docker-containers/thunderbird-home:/home/user/ -v ~/Downloads:/home/user/Downloads --name thunderbird thunderbird:debian-stretch-slim

# start bash in running container
docker exec -it thunderbird /bin/bash

# start bash with root user in running container
docker exec -u root -it thunderbird /bin/bash
