docker build -t firefox:ubuntu .

Minimal run config
docker run -it -d --rm --shm-size=512m -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix -v ~/data/DockerAppsData/firefox:/home/user/.mozilla/ -v ~/Downloads:/home/user/Downloads -v /run/user/1000/pulse:/run/user/1000/pulse -e PULSE_SERVER=unix:/run/user/1000/pulse/native --name firefox firefox:ubuntu

Full run config
docker run -it -d --rm --shm-size=512m -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix -v ~/data/DockerAppsData/firefox:/home/user/.mozilla/ -v ~/Downloads:/home/user/Downloads -v /var/run/dbus/:/var/run/dbus/ -v /run/user/1000/pulse:/run/user/1000/pulse -e PULSE_SERVER=unix:/run/user/1000/pulse/native --device=/dev/snd:/dev/snd --group-add $(getent group audio | cut -d: -f3) --name firefox firefox:ubuntu

# --shm_size fixes the issue of crashing tabs. See: https://bugzilla.mozilla.org/show_bug.cgi?id=1338771#c10
# regarding pulseaudio setup see: https://github.com/jessfraz/dockerfiles/issues/38#issuecomment-247472914













https://www.dinotools.de/2015/12/02/firefox-im-docker-container/

Firefox im Docker Container

Mit Docker ist es nicht nur möglich Server-Anwendungen in einem Container zu betreiben. So können auch Anwendungen mit einer GUI verwendet werden. Im folgenden Artikel wird gezeigt, wie dies am Beispiel des Browsers Firefox realisiert werden kann.

Zunächst wird ein neues Dockerfile erstellt.

Dabei muss beachtet werden, dass ein Nutzer mit der UID und GID 1000 verwendet wird. Diese sollten dem Nutzer entsprechen, der auf dem Hostsystem die Grafische Oberfläche gestartet hat.

FROM ubuntu:14.04

RUN apt-get update && \
        apt-get install -y firefox && \
        apt-get clean

RUN groupadd --gid 1000 user && \
        useradd --uid 1000 --gid 1000 --create-home user

USER user
CMD /usr/bin/firefox

Anschließend kann der Container gebaut und unter dem Tag ubuntu-firefox abgespeichert werden.

$ docker build -t ubuntu-firefox .

War der Vorgang erfolgreich, muss die Zugriffsberechtigung auf den laufenden X-Server erweitert werden. Dies geschieht mit folgendem Befehl.

$ xhost +local:
non-network local connections being added to access control list

Anschließend kann der Firefox im Container gestartet werden.

$ docker run -ti --rm -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix ubuntu-firefox


