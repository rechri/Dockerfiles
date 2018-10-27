docker build -t evolution:ubuntu .

docker run -ti -d --rm --name evolution -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix --device=/dev/dri:/dev/dri -v /usr/share/icons:/usr/share/icons:ro -v ~/data/DockerAppsData/evolution:/home/user/ evolution:ubuntu
