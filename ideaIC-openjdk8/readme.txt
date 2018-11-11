# build image
docker build -t ideaic:2018.2.5 .

# run container
docker run -ti -d --name ideaic --rm -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix -v ~/data/docker-containers/idea-home:/home/user/ ideaic:2018.2.5

# start bash in running container
docker exec -it ideaic /bin/bash
