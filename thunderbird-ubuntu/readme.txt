docker build -t thunderbird:ubuntu .

docker run -ti --rm -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix -v ~/data/DockerAppsData/thunderbird:/home/user/ thunderbird:ubuntu


