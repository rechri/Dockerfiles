# Firefox on Debian

FROM debian:stretch-slim

MAINTAINER Reto Christen, CH-6300 Zug

ENV APP_PACKAGES firefox-esr
ENV USER_NAME user
ENV GID 1000
ENV UID 1000

RUN apt-get update && \
    apt-get install -y --no-install-recommends $APP_PACKAGES dbus dbus-x11 pulseaudio && \
    apt-get clean && \
    rm -rf /var/cache/* /var/log/apt/* /var/lib/apt/lists/* /var/lib/dpkg/info/* /tmp/*

RUN groupadd --gid $GID $USER_NAME && \
    useradd --uid $UID --gid $GID --create-home $USER_NAME && \
    usermod -a -G audio $USER_NAME

USER $USER_NAME

CMD ["/usr/bin/firefox-esr"]
