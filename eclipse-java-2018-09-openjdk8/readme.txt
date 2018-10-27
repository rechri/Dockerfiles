docker build -t eclipse-java:2018-09 .

docker run -ti -d --name eclipse-java --rm -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix -v ~/data/eclipse-workspace:/home/user/eclipse-workspace/ eclipse-java:2018-09

