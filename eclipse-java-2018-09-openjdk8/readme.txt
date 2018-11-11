# build image
docker build -t eclipse-java:2018-09 .

# run container
docker run -ti -d --name eclipse-java --rm -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix -v ~/data/docker-containers/eclipse-java-home:/home/user/ eclipse-java:2018-09

# start bash in running container
docker exec -it eclipse-java /bin/bash
