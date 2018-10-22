# Firefox on Ubuntu

FROM ubuntu:18.10

ENV BROWSER_NAME firefox
ENV USER_NAME user
ENV GID 1000
ENV UID 1000

MAINTAINER Reto Christen, CH-6300 Zug

RUN apt-get update && \
    apt-get install -y --no-install-recommends $BROWSER_NAME dbus dbus-x11 pulseaudio && \
    apt-get clean && \
    rm -rf /var/cache/* /var/log/apt/* /var/lib/apt/lists/* /var/lib/dpkg/info/* /tmp/*

RUN groupadd --gid $GID $USER_NAME && \
    useradd --uid $UID --gid $GID --create-home $USER_NAME && \
    usermod -a -G audio $USER_NAME

USER $USER_NAME

# adding the export to .bashrc fixes a bug -> https://bugs.launchpad.net/ubuntu/+source/at-spi2-core/+bug/1193236
RUN echo 'export NO_AT_BRIDGE=1' >> /home/$USER_NAME/.bashrc

CMD ["/usr/bin/firefox"]
