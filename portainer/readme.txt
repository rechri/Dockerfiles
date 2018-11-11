https://hub.docker.com/r/portainer/portainer/

docker run -d -p 9000:9000 --name portainer --restart always -v /var/run/docker.sock:/var/run/docker.sock -v /home/artisan/data/DockerAppsData/portainer:/data portainer/portainer
