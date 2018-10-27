https://hub.docker.com/_/ghost/

docker pull ghost:2.2.4-alpine

docker run -d -p 2368:2368 --name ghost -v /home/artisan/data/DockerAppsData/ghost-blog:/var/lib/ghost/content ghost:2.2.4-alpine
