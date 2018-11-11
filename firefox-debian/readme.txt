# build image
docker build -t firefox:debian-stretch-slim .

# run container
docker run -it -d --rm --shm-size=512m -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix -v ~/data/docker-containers/firefox-home:/home/user/ -v ~/Downloads:/home/user/Downloads -v /run/user/1000/pulse:/run/user/1000/pulse -e PULSE_SERVER=unix:/run/user/1000/pulse/native --name firefox firefox:debian-stretch-slim

# --shm_size fixes the issue of crashing tabs. See: https://bugzilla.mozilla.org/show_bug.cgi?id=1338771#c10
# regarding pulseaudio setup see: https://github.com/jessfraz/dockerfiles/issues/38#issuecomment-247472914


# start bash in running container
docker exec -it firefox /bin/bash

# start bash with root user in running container
docker exec -u root -it firefox /bin/bash
